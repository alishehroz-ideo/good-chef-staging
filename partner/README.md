# Partner asset test folder

Stand-in for what GameBull's `/context` endpoint will return. Drop replacement PNGs here and list
them in `manifest.json`; the game fetches the manifest at startup and applies each asset by key.

This folder lives **inside the deployed build**, not in `Assets/`. That means:

- It ships to GitHub Pages with every push, so the URLs are live immediately
- It does **not** bloat `WebGL.data` — Unity never sees these files
- It survives rebuilds (Unity only overwrites `Build/`, `TemplateData/` and `index.html`)

## Adding a test asset

1. Put the PNG in this folder
2. Add an entry to `manifest.json`:
   ```json
   { "key": "background", "url": "partner/background.png" }
   ```
3. Commit and push — no Unity rebuild needed

## Keys

| Key | Applies to | Requirements |
|---|---|---|
| `background` | Restaurant background | Any size; aspect should roughly match the original |
| `customer_boy`, `customer_girl_1`, … | Spine customer atlas | **Must be exactly 1528×1068 with the identical atlas layout** — repaint the original, never re-pack |
| `dish_*` | Individual dish sprites | Match the original's dimensions |
| `logo` | Splash / UI logo | Any size |

## Note on CORS

Assets here are same-origin, so the browser never performs a CORS check. GameBull will serve from a
different origin, where the server **must** send `Access-Control-Allow-Origin`. Test at least one
asset from an external URL before assuming the pipeline is production-ready.
