# The Record

*Four years of my Spotify, pressed into one LP. Every groove is a month.*

**Live:** https://suhxnitiwari.github.io/listening-record/

## What it is

A turntable you can actually play. The record holds 53 grooves, one per month from May 2022 on the outside edge to today by the label. Each groove is colored by the artist who owned that month: Ariana Grande's 43 months are the black of the vinyl itself, and the 10 months someone else won show up in color. The record *is* the data.

- **Drop the needle:** pick up the tonearm and set it on any groove. The label turns into that month's album cover and the song I had on repeat starts playing.
- **Spin it:** turn the record by hand and the needle moves through time.
- **Play the whole side:** the needle walks inward month by month, four years in a few minutes.

## How it's built

- **Data pipeline.** `data/record.json` holds each month's #1 artist, their share of the month, hours listened and the song on repeat. It's exported from [listening-history](https://github.com/suhxnitiwari/listening-history), where my raw Spotify export is cleaned in Python and modeled in PostgreSQL.
- **The disc is generated SVG.** Rings are laid out from the outer edge inward, and each ring's width is proportional to the square root of that month's listening hours, so heavy months read as wider grooves without drowning out quiet ones.
- **A real tonearm.** The arm pivots from a fixed point, and the stylus position is solved with the law of cosines so the head always lands on the groove you chose. Pointer events are mapped into SVG coordinates with `getScreenCTM()`, and hit-testing finds the ring under the needle by radius.
- **Hand spinning.** Dragging the disc tracks the angle with `atan2`, unwraps it across the ±π boundary, and advances one groove for every quarter turn.
- **33⅓ rpm.** While a groove plays, a `requestAnimationFrame` loop turns the disc at 200°/s, which is exactly 33⅓ revolutions per minute.
- **No backend, no keys.** Album art and 30-second previews come from Apple's iTunes Search API via JSONP straight from the browser, with a per-song promise cache and a 6-second timeout fallback.

## Design choices

- The metaphor does the explaining. There's no chart axis or legend to learn: outside is the past, the label is now, and color means "not Ariana".
- Bodoni Moda headlines, Caveat handwritten notes beside the deck, JetBrains Mono for the liner-note details, and an SVG film-grain overlay so the page feels like a printed sleeve.
- A soft sheen gradient and faint highlight rings sit over the vinyl so it reads as a physical object, not a donut chart.

## Tech stack

HTML, CSS, vanilla JavaScript, SVG, iTunes Search API (JSONP). Data from Python + PostgreSQL in [listening-history](https://github.com/suhxnitiwari/listening-history).

## Run it locally

```bash
python3 -m http.server
```

Then open http://localhost:8000.

---

© 2026 Suhani Tiwari. **All rights reserved.** The code is public so you can see how I build, not so you can reuse it. See [LICENSE](LICENSE).

Built by [Suhani Tiwari](https://suhanitiwari.com).
