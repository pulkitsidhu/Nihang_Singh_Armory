---name: update-sword
description: >
  Use this skill whenever the user wants to update an existing sword entry in the Nihang Singh Armory collection. It should show the current sword data, ask which fields to change, and allow the user to skip any field update.
---
# Update Sword Skill

## Overview

This skill updates an existing sword entry in `swords.json`. It reads the current entry, displays the existing fields to the user, and prompts for each field one by one. The user can keep the current value, change it, or skip updating that field.

## Step 1 — Identify the sword

- The user should provide a sword name or partial name to update.
- Read `swords.json` and find matching entries by case-insensitive partial match on the `name` field.
- If exactly one match is found: proceed.
- If multiple matches are found: show the matching entries and ask the user to choose one.
- If no match is found: tell the user `No sword found matching '{name}'. Here are the current entries:` and list all sword names.

## Step 2 — Show current data

Once the target entry is identified, show the user the current data in a clear format:

- `Position {order}`
- `Name: {name}`
- `Origin: {origin}`
- `Era: {era}`
- `Specs: {specs.join(', ')}`
- `Story: {story}`
- `Images: {images.join(', ')}`

Then ask: `Which fields would you like to update? You can keep the current value, change it, or skip any field.`

## Step 3 — Collect updates

Ask the user for each field in turn:

- `name`
- `origin`
- `era`
- `specs` (up to 4 values)
- `story`
- `images`

For each field, show the current value and allow the user to provide a new value or say `skip` / leave blank to keep the current value.

## Step 4 — Apply updates

- Update only the fields the user changed.
- For `specs`, normalize the response into an array of values.
- For `images`, normalize the response into an array of filenames.
- Keep the `id` the same unless the user explicitly requests an id change, but prefer preserving the existing `id` for consistency if not asked.

## Step 5 — Save changes

- Write the updated array back to `swords.json`.
- Keep order values unchanged unless the user explicitly asks to update the position.

## Step 6 — Confirm

Tell the user: `✓ {name} has been updated. Here is the new entry:` and repeat the updated entry data.
