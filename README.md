# SuperCoach Tracker

A simple browser-based tracker for your NRL SuperCoach squad. Tracks each player's purchase price, current price, value change, and points-per-dollar efficiency — both at current market rate and against what you actually paid.

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

## Adding your squad

For each of your 25 players, click **+ Add player** and fill in:

- **Name**
- **Purchase price** — what you paid. For original draft picks, this is the Round 1 starting price. For mid-season pickups, this is the price when you traded them in.
- **Current price** — today's market price (from the squad screenshot).
- **Season average** — from the squad screenshot.
- **Round acquired** — `0` for original draft picks, or the round number you traded them in.
- **Original price average** *(optional)* — leave blank to derive from Purchase ÷ Magic Number, or fill in if you happen to know the player's actual average at the time you bought them.

Any field can be edited later by clicking it directly in the table.

## Trading

When you make a trade, click **Apply trade** (or the `trade` action on a player row). The outgoing player moves to the **Inactive list** with their final stats preserved; the incoming player joins the active squad with the round labelled.

If you trade the same player back in later, just add them again — they'll get a new ownership period with a new purchase price.

## Magic number

Used to derive Original Price Average from Purchase Price. SuperCoach NRL prices roughly equal `(player average) × magic number`. Default is `5,600`; adjust in Settings if needed.

## Backup and portability

- **Export JSON** saves your entire dataset to a file.
- **Import JSON** loads it back. Useful for moving between devices or browsers — there's no cloud sync.

## Roadmap

- Screenshot upload mode (vision API extraction of squad and trade screenshots)
- Round-by-round history snapshots for trend lines
- Hypothetical trade preview
