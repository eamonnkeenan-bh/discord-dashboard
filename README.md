# BetHero Discord Dashboard

A password-protected dashboard that visualizes Discord Server Insights data, hosted on GitHub Pages.

## Setup (one-time)

1. Create a new **public** GitHub repo (free GitHub Pages requires public repos).
2. Push all files from this folder to the repo root.
3. Go to **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → Save.
4. Your dashboard will be live at `https://<your-username>.github.io/<repo-name>/`.
5. The password to access it is already set in the code.

## Weekly upload workflow

1. Download the latest week's CSVs from the Discord Developer Portal (Server Insights).
2. Drop them into the `data/` folder in your repo. Don't delete old files — the dashboard merges and deduplicates automatically.
3. Commit and push. The GitHub Action will auto-update `manifest.json` to include the new files.
4. The dashboard refreshes within a minute or two once Pages deploys.

That's it. No database, no build step, no server.

## File naming

The dashboard identifies files by their name prefix (e.g. `guild-total-membership`, `popular-text-channels`).
The number suffix (`_2_`, `_3_`, etc.) is ignored, so it doesn't matter if Discord increments them.

Recognized prefixes:
- `guild-total-membership`
- `guild-joins-by-source`
- `guild-leavers`
- `guild-activation`
- `guild-communicators`
- `guild-message-activity`
- `guild-muters`
- `popular-text-channels`
- `new-members-by-discord-tenure`
- `participators-by-guild-tenure`
- `participators-by-platform`
- `participators-by-reg-country`

## If the manifest doesn't update automatically

If the GitHub Action doesn't fire (e.g. you uploaded via the GitHub web UI and it didn't trigger the push event), you can:
- Go to the **Actions** tab → **Update manifest** → **Run workflow** manually.
- Or edit `data/manifest.json` by hand — it's just a JSON array of filenames.

## Changing the password

Edit the `HASH` variable near the top of the `<script>` section in `index.html`.
