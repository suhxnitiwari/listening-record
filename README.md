# The Record

**Four years of my Spotify, pressed into one LP.**

Every groove is a month, from May 2022 on the outside edge to today by the label. The groove's color is the artist who owned that month: Ariana Grande's 43 months are the black of the vinyl itself, and the 10 months someone else won show up in color. The record *is* the data.

- **Drop the needle:** pick up the tonearm and set it on any groove. The label becomes that month's album cover and its song plays.
- **Spin it:** turn the record by hand and the needle moves through time.
- **Play the whole side:** the needle walks inward month by month, four years in a few minutes.

## How it works

One static page, no build step. `data/record.json` holds each month's #1 artist, their share of the month, hours listened and the song on repeat, exported from [listening-history](https://github.com/suhxnitiwari/listening-history), where my Spotify export is cleaned in Python and modeled in PostgreSQL. The record is SVG: each ring's width follows that month's listening hours. Covers and previews come from Apple's iTunes Search API, straight from the browser.

To run it locally:

```bash
python3 -m http.server
```

Then open http://localhost:8000.

## Ownership

© 2026 Suhani Tiwari. **All rights reserved.** The code is public so you can see how I build, not so you can reuse it. See [LICENSE](LICENSE).
