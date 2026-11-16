# VI · After Hours content

The After Hours Android app reads `content.json` from this repo, at most every 6 hours.
Edit it on github.com and phones pick up the change the next time the app refreshes. No app update is needed.

Everything is validated in the app (`VI.cleanRemote` in `model.js`), and an invalid part is ignored on its own.
This file can only:

- `quiz`: **add** questions: `["Question?", ["A", "B", "C", "D"], correctIndex]`, where correctIndex is 0–3 and all four answers differ.
- `missions`: **replace** the daily challenge lists: `{"rides": ["a jet ski"], "goals": ["find the pier"]}`. Both lists need at least one entry.
- `locations`: **replace** region text: `{"id": "vice-city", "description": "…", "source": "https://www.rockstargames.com/…"}`.
  Valid ids are vice-city, leonida-keys, grassrivers, port-gellhorn, ambrosia, mount-kalaga.
- `news`: **replace** the offline fallback news (max 20): `{"title", "summary", "url", "date": "YYYY-MM-DD", "category"}`.
  Links must be on rockstargames.com, gtadb.org or one of the app's news sites.

It cannot change the news sources, links, feedback address, release date or anything else.
Keep `"version": 1`. Size limit 512 KB. Facts only from official sources; no leaks.

## Added in app 0.6.0

- `challenges`: **replace** the weekly challenge pool (at least 3): `{"id": "visit20", "title": "Visit 20 new landmarks", "type": "visit", "target": 20}`.
  Types: visit, visitNature, visitCity, daily, quiz, perfect, pins, bingoLine, collect, garage. Each week the app picks 3 and keeps them for that week.
- `bingo`: **replace** the weekly bingo squares (at least 16, max 60 characters each). Every Monday the app deals a new 16-square card from this list.
- `collectibles`: sets shown as a map layer with a 100% checklist:
  `{"id": "set-id", "name": "Set name", "items": [{"id": "item-id", "name": "Item name", "world": [x, y], "note": "where exactly"}]}`.
  `world` uses the same coordinates as GTADB landmarks; leave it out if the position is unknown. Ids: lowercase letters, digits, dashes.
- `garage`: vehicle categories for the garage checklist:
  `{"id": "sports", "name": "Sports cars", "items": [{"id": "vehicle-id", "name": "Vehicle name", "note": "optional"}]}`.

Do not rename ids after release: players' ticks are stored under `set-id:item-id`.
Only add collectibles and vehicles that are actually documented (with a source); never guess positions.
