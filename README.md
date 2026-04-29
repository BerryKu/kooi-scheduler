# Kooi Family Scheduler

A static single-page family availability calendar, hosted on GitHub Pages.

## How it works

The page fetches four `.ics` calendar files from the `/feeds/` directory in
this repository and renders a two-week availability grid. A GitHub Actions
workflow keeps those files up-to-date by downloading them from their source
URLs on a schedule.

## Calendar feeds

| File | Source |
|------|--------|
| `feeds/kooi-family.ics` | `webcal://p127-caldav.icloud.com/published/2/NTcxMTY4NTQ4NTcxMTY4NUwc29ymuumPBBLSLt2tLutpgn3SIKQqSpD9hidKI2ud` |
| `feeds/kooi-ohio.ics` | `webcal://p127-caldav.icloud.com/published/2/NTcxMTY4NTQ4NTcxMTY4NUwc29ymuumPBBLSLt2tLutqLKSt5Bzb6nhqLwHKvCAj_9vavH1LcgDvs6lFwmX4pT2mAJu2lj7LHEW8CT4rbqA` |
| `feeds/drem-soccer.ics` | `https://calendar.playmetrics.com/calendars/c610/t359149/p0/t08BC233F/f/calendar.ics` |
| `feeds/sofie-volleyball.ics` | `https://www.nextvolleyballclub.com/ical_feed?tags=8318994` |

> **Note:** `webcal://` URLs are fetched via `https://` (same host/path) by
> the workflow to avoid browser CORS limitations.

## Updating feed URLs

1. Open `.github/workflows/refresh-calendars.yml`.
2. Find the `curl` commands in the **Fetch calendar feeds** step.
3. Replace the URL for whichever feed has changed.
4. Commit and push — the next scheduled run (or a manual trigger) will pick
   up the new URL.

## Running the workflow manually

1. Go to the **Actions** tab in this repository.
2. Select **Refresh Calendars** from the left sidebar.
3. Click **Run workflow** → **Run workflow**.

The workflow also runs automatically every hour via a cron schedule.

## Local development

Open `index.html` directly in a browser **after** the feeds have been
committed to the repo (the page fetches `/feeds/*.ics` relative to the page
origin). For local testing you can serve the repo root with any static HTTP
server, for example:

```sh
npx serve .
```
