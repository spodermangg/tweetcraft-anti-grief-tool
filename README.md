# TweetCraft Anti-Grief

A userscript for [TweetCraft](https://tweetcraft.jai.vin) that lets you snapshot a
region of the world and later revert grief — destroyed, changed, or added blocks,
including fire, water, and lava — back to the snapshot state. By @andrestube123 and @vibecodingonsol

**File:** `tweetcraft-anti-grief.user.js`

---

## Installation

This is a **userscript**, so you need a userscript manager installed in your
browser first. Tampermonkey is recommended.

### 1. Install a userscript manager

| Browser | Extension |
| ------- | --------- |
| Chrome / Edge / Brave / Opera | [Tampermonkey](https://www.tampermonkey.net/) |
| Firefox | [Tampermonkey](https://www.tampermonkey.net/) or [Greasemonkey](https://addons.mozilla.org/firefox/addon/greasemonkey/) |
| Safari | [Tampermonkey](https://www.tampermonkey.net/) or [Userscripts](https://apps.apple.com/app/userscripts/id1463298887) |

### 2. Install the script

**Option A — one-click (if published):** open the script's raw URL; Tampermonkey
will show an install page. Click **Install**.

**Option B — from a local file (default):**

1. Open the Tampermonkey dashboard (click its icon → **Dashboard**).
2. Go to the **Utilities** tab.
3. Under **Import from file**, choose `tweetcraft-anti-grief.user.js` and click
   **Import**. Review and confirm.
4. Alternatively, click **+** (Create a new script), delete the placeholder, and
   paste the entire contents of `tweetcraft-anti-grief.user.js`, then
   **File → Save** (`Ctrl`/`Cmd` + `S`).

### 3. Enable and verify

1. Make sure the script is **enabled** in the dashboard.
2. The `@match` rules cover `https://tweetcraft.jai.vin/r/*` and
   `https://tweetcraft.jai.vin/play/*`.
3. Open TweetCraft. The **🛡️ Anti-Grief** panel appears in the top-right corner.

> The script uses `@run-at document-start` and `@grant unsafeWindow`, so it can
> hook the game's WASM engine and network early. Keep these in the header.

### Updating

- **From a URL:** Tampermonkey auto-checks for updates, or use the dashboard's
  **Check for userscript updates**.
- **From a local file:** re-import the new file (Utilities → Import from file) or
  paste the new contents over the old script and save.

---

## Keybinds

| Key | Action |
| --- | ------ |
| `Shift+1` | Set Point 1 (P1) |
| `Shift+2` | Set Point 2 (P2) |

> Points can only be set while playing (pointer lock active) and the chat closed.
> Keybinds can be toggled off in **Options**.

---

## Selection

- Define the region using **two opposite corners**: P1 and P2.
- **Full height** (on by default) scans the whole column (`y = 1..127`) across the
  X/Z rectangle you selected.
- Turn **Full height** off to use the Y values of the two points instead.
- You can also type coordinates directly into the P1 / P2 fields in the panel.

---

## Snapshots

- **Scan & Save** records every non-air block in the region.
- Container blocks are **excluded** from snapshots so their contents are never
  overwritten or reverted: chests, trapped/Ender chests, furnaces, barrels,
  hoppers, dispensers, droppers, shulker boxes.
- Snapshot names are automatically versioned (`name`, then `name v1`, `name v2`, …).

---

## Large backups (external JSON)

- If a snapshot is too large for `localStorage`, it is kept as an **external JSON
  backup only**.
- The checkpoint entry stays in the list after a page refresh (shown with a
  `⚠ external JSON only` warning), but its block data lives in the exported file.
- To revert an external-only snapshot: **Import the exported JSON first**, then
  press Revert. Revert will otherwise prompt you to import the file.

---

## Export / Import

| Button | Action |
| ------ | ------ |
| **Export All JSON** | Download every stored snapshot in one file |
| **Import JSON** | Merge snapshots from an exported file |
| **Export** (per row) | Download a single snapshot |

Exported filenames use the checkpoint name plus a timestamp:

```
antigrief-<checkpoint-name>-YYYY-MM-DD_HH-MM-SS.json
```

Names are sanitized (spaces and special characters become `-`).

---

## Confirmations

- **Revert** — warns that *everything new since the snapshot will be gone*, and
  shows the snapshot name and date.
- **Update / Rescan** — warns that the snapshot will be overwritten.
- **Delete** — warns the snapshot will be permanently removed unless you have an
  exported JSON backup.

---

## Notes

- **Max region** is configurable (default `8,000,000` cells).
- Fluids and fire are handled specially on revert (dug, not overwritten).
- Floating blocks are auto-supported with temporary scaffolding when placing.
- Revert runs chunked and async with progress and a **Cancel** button.
