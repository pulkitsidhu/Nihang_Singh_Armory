---name: remove-sword
description: &gt;
  Use this skill whenever the user wants to remove, delete, or take down a sword
  from the Nihang Singh Armory website. Triggers include: "remove", "delete",
  "take down", "retire", or "get rid of" followed by a sword name or description.
  The user will provide the name or title of the piece to remove.
---
# Remove Sword Skill

## Overview

This skill removes a sword entry from the Nihang Singh Armory collection by name.
It updates swords.json, re-numbers remaining entries, and pushes to GitHub.

## Step 1 — Identify the sword

- The user will provide a name or partial name of the sword to remove
- Read swords.json and find the entry whose `name` field matches (case-insensitive, partial match is fine)
- If exactly one match is found: proceed to Step 2
- If multiple matches are found: show the user the matching entries and ask them to confirm which one
- If no match is found: tell the user "No sword found matching '{name}'. Here are the current entries:" and list all sword names

## Step 2 — Confirm before deleting

Always confirm before removing. Show:
"I found this entry:  Position {order}: {name} — {origin}, {era}
Are you sure you want to remove it from the collection? This cannot be undone."

Wait for explicit confirmation ("yes", "confirm", "remove it", etc.) before proceeding.

## Step 3 — Remove the entry

- Delete the matching entry from the swords.json array
- Re-number all remaining entries sequentially (order: 1, 2, 3…) to close the gap
- Write the updated array back to swords.json

## Step 4 — Handle images (optional)

Ask the user: "Would you like to also delete the image files for this piece from the images/ folder?"
- If yes: delete all image files listed in the entry's `images` array from the `images/` folder
- If no: leave the image files in place

## Step 5 — Commit and push to GitHub

Run these commands:

```
git add swords.json images
git commit -m "Remove sword: {name}"
git push origin main
```

## Step 6 — Confirm

Tell the user: "✓ {name} has been removed from the collection. The remaining {n} pieces have been re-numbered. Changes are live at nihangsingh.com."

---