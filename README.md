# Fleet Usage Report — MyGeotab Add-In

Shows how many of your fleet's vehicles were out (had at least one trip) each
day over a date range you pick. Includes a daily bar chart, a day-by-day
breakdown (with names of vehicles NOT out that day), and a per-vehicle
utilization ranking.

## How it works

- Uses the standard MyGeotab Add-In API (`api.call`) — no external services
  or API keys needed.
- Pulls your active `Device` list, then pulls `Trip` records for the chosen
  date range.
- A vehicle counts as "out" on a given day if it has at least one trip that
  *starts* that calendar day (using the browser's local time zone).

## Hosting it (same pattern as your other add-ins)

1. Create a new GitHub repo (e.g. `fleet-usage-addin`) and push `index.html`
   to it.
2. Enable GitHub Pages for the repo (Settings → Pages → deploy from `main`
   branch, root folder).
3. Your hosted URL will look like:
   `https://YOUR-GITHUB-USERNAME.github.io/fleet-usage-addin/index.html`

## Installing in MyGeotab

1. In MyGeotab, go to **Administration → System → System Settings → Add-Ins**.
2. Click **New Add-In**, choose **URL**, and paste in the JSON from
   `config.json` — but first edit the `"url"` field to match your actual
   GitHub Pages URL from step 3 above.
3. Save. The add-in will appear as "Fleet Usage Report" in the left-hand
   Activity menu.

## Notes / easy tweaks later

- Default range is the last 30 days; users can change it and click
  **Run Report**.
- `resultsLimit` on the Trip call is set to 50,000 — plenty of headroom for
  11 vehicles, but raise it if the fleet grows a lot.
- If you'd rather define "out" as "moved more than X miles" instead of "had
  any trip," that's a small change inside the `render()` function.
- The icon URL in `config.json` is a placeholder — swap for a Fleet Wolf
  logo/icon if you want it on-brand.
