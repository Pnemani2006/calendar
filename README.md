# Google Sheets Calendar

A single-page calendar that reads events from a Google Sheet. When the page opens, **today is highlighted** and today's events are shown in the side panel. Edit the sheet → the site updates (no redeploy).

## 1. Set up the Google Sheet

1. Create a new Google Sheet (or import `sheet-template.csv` via **File → Import**).
2. Row 1 must be headers. Only `Date` and `Title` are required:

   | Date | Time | Title | Location | Description | Link | Color | Image |
   |---|---|---|---|---|---|---|---|
   | 2026-11-02 | 9:00 AM | Team standup | Zoom | Weekly check-in | | moss | |
   | 2026-11-04 | All day | Field trip | | Bring lunch | | river | https://drive.google.com/file/d/…/view |

   - **Date**: `2026-11-02` or `11/2/2026` both work.
   - **Link**: optional URL; the event title becomes clickable.
   - **Color**: optional. Use a nature color name (great as a dropdown) or any hex code (`#2e9e5b` or `2e9e5b`).
     Names: `moss` `fern` `sage` `olive` `pine` `clay` `terracotta` `rust` `bark` `sunflower` `honey` `sky` `river` `ocean` `lavender` `berry` `blossom` `stone`.
     Plain `green`, `red`, `blue`, etc. also work and map to earthy shades.
   - **Image**: optional. Paste a Google Drive share link (set the file to "Anyone with the link → Viewer") or any direct image URL. It shows as a polaroid in the day panel.
   - Multiple events on the same day = multiple rows.
3. Share it: **Share → General access → Anyone with the link → Viewer**.
   *(Or use **File → Share → Publish to web → CSV** and use that link instead.)*

## 2. Connect it

Open `index.html` and paste your sheet's link into the config near the top:

```js
sheetUrl: "https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/edit#gid=0",
title: "My Calendar",
```

If you have multiple tabs, copy the link while viewing the tab you want (the `gid=` part picks the tab).

## 3. Host on GitHub Pages

1. Create a repo and upload `index.html` (the README/CSV are optional).
2. **Settings → Pages → Deploy from branch → `main` / root → Save**.
3. Your calendar will be at `https://<username>.github.io/<repo>/`.

## Embedding

```html
<iframe src="https://<username>.github.io/<repo>/" width="100%" height="800" style="border:0"></iframe>
```

## Linking to a specific day

- `https://.../?date=2026-12-25` opens on and highlights that day.
- No parameter = today.

## Making a color dropdown

Select the Color column → **Insert → Dropdown** → add options like `moss`, `sunflower`, `river`, `clay`, `berry`. The calendar reads the option text.

## Notes

- **Double-clicking `index.html` won't load the sheet.** Google only sends sheet data to pages served from a web address, so use the GitHub Pages URL (or a local server) to see live data.

- Changes to the sheet show up on refresh (Google can cache for a few minutes). The open page also re-pulls every 10 minutes (`refreshMinutes`).
- Collapses to little leaf dots on phones.
