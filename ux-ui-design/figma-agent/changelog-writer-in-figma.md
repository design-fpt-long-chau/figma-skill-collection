---
name: changelog-writer-in-figma
description: Write or update a changelog entry in a Change Log Table/Body component — fills in title, description, date, time, and optionally appends meeting minutes to the description.
---

# Changelog Writer in Figma

Write or update a changelog entry inside a **Change Log Table/Body** component instance. The user provides a summary of what happened, and optionally includes meeting minutes for extra detail.

## When to use

- The user asks to add, edit, or update a changelog note in their Figma file.
- The user selects a **Change Log Table/Body** instance and asks to fill it in.

## Inputs

The user provides:

1. **Summary** (required) — a short description of the activity (e.g. "Họp transfer timeline, wireframe, plan với đội hệ thống vào lúc 9h30 sáng").
2. **Meeting minutes** (optional) — detailed notes from a meeting to append to the description.

## Steps

### 1. Identify the target node

If the user has selected a **Change Log Table/Body** instance, use that node. Otherwise, ask the user to select one.

### 2. Find text nodes inside the instance

Use `evaluate_script` to walk the instance's children and locate these text nodes by name:

| Node name | Purpose |
|---|---|
| `Title` | Short title of the changelog entry |
| `Type your description here...` (or existing description text) | Description / details |
| `22.09.2025` (or existing date) | Date metadata |
| `9:41 PM` (or existing time) | Time metadata |

Since node names may already have been edited, find all TEXT nodes and identify them by their position in the layer tree or their original name.

### 3. Update metadata

- Set the **date** node to today's date in `DD.MM.YYYY` format.
- Set the **time** node to the time mentioned by the user (e.g. `9:30 AM`). If no specific time is given, use the current time.

### 4. Update title

Generate a concise title from the user's summary (keep it short, 3-5 words).

### 5. Update description

Compose the description from the user's summary. Elaborate the summary into 1-2 clear sentences that explain what happened, who was involved, and what was discussed or decided.

**If meeting minutes are provided**, append them to the description using this format:

> [Summary sentence(s)]
>
> Chi tiết cuộc họp:
> - [Key point 1 from minutes]
> - [Key point 2 from minutes]
> - [Key point 3 from minutes]
> - ...

Extract and condense the meeting minutes into clear bullet points. Keep each point concise but informative. Include action items, decisions, and key takeaways.

### 6. Load fonts before editing

Always load all fonts used in each text node before modifying:

const segments = textNode.getStyledTextSegments(['fontName']);
await Promise.all(segments.map(s => figma.loadFontAsync(s.fontName)));

### 7. Confirm with user

After updating, ask the user to review the result and offer to adjust any part of the entry.
