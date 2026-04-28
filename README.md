# SuperCoach Tracker

A simple browser-based tracker for your NRL SuperCoach squad. Tracks each player's purchase price, current price, value change, and points-per-dollar efficiency — both at current market rate and against what you actually paid. Supports both manual entry and screenshot upload via the Anthropic API.

## What it does

For each of your 25 players, it shows:

| Column | Meaning |
|---|---|
| Player | Name. Originals have no badge; mid-season pickups show the round they were traded in (e.g. `R6`). |
| Purchase | What you paid. Italic = manually entered. |
| Current | Today's market price. |
| Value Δ | Current − Purchase (green = gained value, red = lost). |
| Season Avg | Points per game, season to date. |
| Orig Avg | Implied average from purchase price ÷ magic number. Editable if you want to set the player's *actual* average at time of purchase. |
| $/Pt | Current market efficiency: Current ÷ Season Avg. |
| Purch $/Pt | Your efficiency: Purchase ÷ Season Avg. Highlighted green when meaningfully better than current $/Pt — that's the "good buy" signal. |

A summary strip at the top shows total squad value, total value gained, and squad-wide average $/Point.

## Setup

1. Clone or download this repo.
2. Either open `index.html` directly in a browser, or push to GitHub and enable GitHub Pages (Settings → Pages → Source: `main` branch, root folder).
3. Your data lives in your browser's localStorage. **Use Export JSON regularly to back it up.**

## Adding your squad — manual entry

For each of your 25 players, click **+ Add player** and fill in:

- **Name**
- **Purchase price** — what you paid. For original draft picks, this is the Round 1 starting price. For mid-season pickups, this is the price when you traded them in.
- **Current price** — today's market price (from the squad screenshot).
- **Season average** — from the squad screenshot.
- **Round acquired** — `0` for original draft picks, or the round number you traded them in.
- **Original price average** *(optional)* — leave blank to derive from Purchase ÷ Magic Number, or fill in if you happen to know the player's actual average at the time you bought them.

Any field can be edited later by clicking it directly in the table.

## Adding your squad — screenshot upload

Once you've set an API key in Settings, you can click **Upload screenshots** to extract data from SuperCoach screenshots automatically.

1. **Get an Anthropic API key.** Go to [console.anthropic.com](https://console.anthropic.com), sign up, add some credit (US$5 lasts roughly a year of weekly uploads), and create a key. Set a monthly spend limit while you're there.
2. **Save the key in Settings.** It's stored only in this browser's localStorage. It's not part of JSON exports and is never sent to GitHub. Each device/browser needs its own copy of the key.
3. **Click Upload screenshots.** Drop in 1+ squad screenshots (the "Starting/Bench" view) and optionally a trade history screenshot. Click Extract data.
4. **Review the diff.** The app shows you what would change — new trades, stat updates, unmatched players. Tick the changes you want to apply, untick the ones you don't.
5. **Click Apply selected.** Done.

Manually-entered values are protected: if you've set a Current Price by hand, an upload won't silently overwrite it. The diff will show that the upload *would* change the value but it's locked, so you can choose whether to override.

The app uses Claude Sonnet 4.6, which costs roughly 5–10 cents per weekly upload. Your spend limit is your safety net.

## Trading

When you make a trade, click **Apply trade** (or the `trade` action on a player row). The outgoing player moves to the **Inactive list** with their final stats preserved; the incoming player joins the active squad with the round labelled.

If you trade the same player back in later, just add them again — they'll get a new ownership period with a new purchase price.

If you upload a trade screenshot, all the IN/OUT moves are extracted and shown in the diff for confirmation before applying.

## Magic number

Used to derive Original Price Average from Purchase Price. SuperCoach NRL prices roughly equal `(player average) × magic number`. Default is `5,600`; adjust in Settings if needed.

## Backup and portability

- **Export JSON** saves your entire dataset to a file. (The API key is *not* included.)
- **Import JSON** loads it back. Useful for moving between devices or browsers — there's no cloud sync.

## Privacy and security notes

- All squad data lives in your browser's localStorage. Nothing is sent anywhere unless you click Upload, which sends screenshots to Anthropic's API.
- Your API key is stored separately from your squad data and is never included in JSON exports.
- The app sends your API key only to `api.anthropic.com`. You can verify this in your browser's network tab.
- If you publish this app via GitHub Pages, **the source code is public but your data and key are not** — they live only in your browser.

## Roadmap

- Round-by-round history snapshots for trend lines
- Hypothetical trade preview ("what if I swapped X for Y")
- Optional cheaper extraction model (Haiku) toggle
