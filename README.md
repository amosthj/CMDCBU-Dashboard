# CMCDBU Safety Dashboard

A one-page safety dashboard (WIR, AFR, ASR by project site) that reads all its figures from one Excel file: `data/safety-data.xlsx`.

Nothing is typed into the web page. To change any number, change the Excel file and upload it again. GitHub keeps every version you upload, so the full history is never lost.

## What's in this folder

| File | What it is |
|---|---|
| `index.html` | The dashboard page. You don't need to edit it. |
| `data/safety-data.xlsx` | **The data.** The only file you update. |
| `xlsx.full.min.js` | Lets the page read Excel files (SheetJS, Apache 2.0 licence, see `xlsx-LICENSE.txt`). |

## One-time setup (about 10 minutes)

1. Sign in to github.com and click **New repository**. Name it, for example, `safety-dashboard`.
2. On the new repository page, click **uploading an existing file**. Drag in everything from this folder, including the `data` folder. Click **Commit changes**.
3. Go to **Settings → Pages**. Under "Build and deployment", set Source to **Deploy from a branch**, Branch to **main** and folder to **/ (root)**. Click **Save**.
4. After a minute or two, the page shows the address of your dashboard, such as `https://<your-account>.github.io/safety-dashboard/`. Send that link to your bosses.

> On a free GitHub account the page and the Excel file are public: anyone with the link can see them. Use a company GitHub plan with private Pages, or leave out anything sensitive such as names.

## Monthly update

1. Download the current file: open `data/safety-data.xlsx` on GitHub and click the download button.
2. **Projects** sheet: one row per project with its START DATE. Fill in END DATE only when the project is completed.
3. **Monthly data** sheet: one row per project per month.
   - PROJECT: pick from the list.
   - MONTH: any date in that month, e.g. 1/11/2026.
   - MANPOWER: average workers on site.
   - HOURS WORKED: total man-hours for the month.
   - NO. OF ACCIDENTS and MAN-DAYS LOST: put 0 if none. ACCIDENT DATE only if there was one.
   - The grey columns (near misses, recordable incidents) are optional. Blank counts as 0.
4. Save the file. Keep the name exactly `safety-data.xlsx` and keep the column headings as they are.
5. On GitHub, open the `data` folder, then click **Add file → Upload files**. Drop in the file and click **Commit changes**. It replaces the old one.
6. Within a couple of minutes, reload the dashboard and the new figures appear.

### Correcting a mistake

Fix the figure in the Excel file and upload it again in the same way. The dashboard always shows the latest upload.

### If something looks wrong

A yellow box at the top of the dashboard lists any row it couldn't read, such as a word where a number should be, with the sheet and row number. Fix those rows and upload again.

## Getting an old version back

Open `data/safety-data.xlsx` on GitHub and click **History**. Every upload is listed with its date. Open one and click download to get that version.

## How the page works

- **Reporting period:** the 12 months ending with the latest month in the file.
- **Rolling rates for each month** use that month and the 11 before it:
  - WIR = reportable accidents ÷ average workers × 100,000
  - AFR = reportable accidents ÷ man-hours × 1,000,000
  - ASR = man-days lost ÷ man-hours × 1,000,000
- **Before a site starts:** months before its start date are not counted.
- **Sample data:** if the file has no figures filled in yet, the page shows sample data and says so at the top.
- **Incidents by type** is still sample data. There is no column for it yet.
- **Targets:** WIR 400, AFR 1.8, ASR 30. To change them, edit the `TARGETS` line near the top of the script in `index.html`, or ask Claude.
