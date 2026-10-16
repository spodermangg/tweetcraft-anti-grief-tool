// TweetCraft Anti-Grief README
// Generated: 2026-10-16
This file describes the anti-grief userscript: tweetcraft-anti-grief.user.js

Keybinds
- Shift+1: Set Point 1 (P1)
- Shift+2: Set Point 2 (P2)
- Must be in pointer lock + chat closed

Selection
- Define region using P1 + P2 (opposite corners). 
- "Full height" (default on): scans y=1..127 for the X/Z rectangle. 
- If off: uses the Y of the points.

Snapshot
- Scan & Save creates a snapshot of non-air blocks (excluding containers: chests, furnaces, barrels, hoppers, dispensers, droppers, shulker boxes, ender chest). 
- Containers are excluded so their contents are not overwritten/reverted.

Large backups
- If snapshot is too big for localStorage, it is saved as external JSON only. 
- The checkpoint entry remains (stub) after refresh. 
- To revert an external-only snapshot: Import the exported JSON first (or use Import JSON button), then Revert.

Export/Import
- Export All JSON / Import JSON in Options
- Per-snapshot "Export JSON" downloads named: antigrief-<checkpoint-name>-YYYY-MM-DD_HH-MM-SS.json
- Filenames are sanitized.

Warnings
- Revert: confirms "everything new since snapshot will be gone" + name/date
- Update/Rescan: confirms overwrite
- Delete: confirms with note about JSON backup

Notes
- Max region configurable (default 8,000,000). 
- Fluids/fire handled on revert. 
- Supports auto-scaffolding when placing floating blocks.
