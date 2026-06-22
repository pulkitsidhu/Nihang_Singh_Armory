---
name: add-sword
description: &gt;
  Use this skill whenever the user wants to add a new sword or weapon to the
  Nihang Singh Armory website. Triggers include: "add a new sword", "add a
  piece", "new item", "add to the collection", or any mention of adding a
  weapon with details. This skill guides Claude through collecting all required
  fields, placing the item at the correct position in the scroll order, updating
  swords.json, and committing the change to GitHub.
---
# Add Sword Skill

## Overview

This skill adds a new sword entry to the Nihang Singh Armory collection.
It collects all required data from the user conversationally, inserts the entry
at the correct scroll position, updates swords.json, and pushes to GitHub.

## Step 1 — Collect fields

Ask the user for the following, one at a time or all at once if they provide them upfront:

| Field   | Required | Description |
|----------|----------|--------------------------------------------------|
| name     | Yes      | Display title (e.g. "Mughal Talwar") |
| origin   | Yes      | Country or region (e.g. "India") |
| era      | Yes      | Date or century (e.g. "17th Century") |
| specs    | Yes      | Up to 4 bullet specs (material, length, condition, etc.) |
| story    | Yes      | 2–4 sentences of provenance and history |
| images   | Yes      | Ask user for the image filename(s) in the S3 bucket (e.g. `mughal-talwar-004-1.jpg`) |
| order    | Yes      | Which position in the scroll (1 = top). Ask: "Where should this appear in the collection? Enter a number — for example, 1 for the very top, or leave blank to add it at the end." |

## Step 2 — Handle scroll position

- Read the current swords.json
- If the user specifies an order number:
  - Shift all existing entries with order >= the requested position up by 1
  - Insert the new entry at the requested position
- If the user says "end" or leaves blank:
  - Set order = (current highest order + 1)
- Re-number all entries sequentially after insertion so order values are always 1, 2, 3… with no gaps

## Step 3 — Handle images

- Ask the user to provide the exact image filename(s) in the S3 bucket
- If the files are not uploaded yet, ask the user to upload each image to S3 using AWS CLI:

```bash
aws s3 cp {filename} s3://nihang-singh-armory/{filename}
```

- Confirm upload succeeded before proceeding (if upload was needed)
- Reference images in swords.json as full CloudFront URLs:

```
https://d31u72jjifwhxm.cloudfront.net/images/{filename}
```

- Naming convention: {slug}-{zero-padded-number}-{n}.jpg
  Example: mughal-talwar-004-1.jpg, mughal-talwar-004-2.jpg

## Step 4 — Generate the entry

Construct the JSON object:

```json
{
  "id": "{slugified-name}-{zero-padded-number}",
  "order": {position},
  "name": "{name}",
  "origin": "{origin}",
  "era": "{era}",
  "specs": ["{spec1}", "{spec2}", "{spec3}"],
  "story": "{story}",
  "images": ["{image1}", "{image2}"]
}
```

Step 5 — Update swords.json

Read the current swords.json

Insert or reorder as per Step 2

Write the updated array back to swords.json

Confirm the updated list to the user: show a numbered list of all sword names in their new order

Step 6 — Commit and push to GitHub

Run these commands:

```
git add swords.json images
git commit -m "Add sword: {name} at position {order}"
git push origin main
```

Step 7 — Confirm

Tell the user: "✓ {name} has been added to the collection at position {order}. It is now live at nihangsingh.com."

---