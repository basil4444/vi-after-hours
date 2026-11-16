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
