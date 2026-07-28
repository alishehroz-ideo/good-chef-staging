# Good Chef — Cooking Games · WebGL staging build

Mobile-landscape WebGL build of Good Chef, for staging/testing.

**Live:** https://alishehroz-ideo.github.io/good-chef-staging/
**Also on Netlify:** https://good-chef-staging.netlify.app

## Build

| | |
|---|---|
| Unity | 6000.4.3f1 |
| Template | `GoodChefMobile` (mobile landscape) |
| Compression | Brotli + JS decompression fallback (`.unityweb`) |
| Download | ~66 MB |

Scenes: `SampleScene` → `LoadData` → `GameMenu` → `GameMain`

## Notes

- **Landscape only.** Portrait shows a rotate prompt on touch devices. Tap *"Tap to play"* to go fullscreen and lock orientation — browsers require a user gesture for both.
- Device pixel ratio is capped to 1 on touch devices for framerate.
- Textures use a **WebGL-only** override at 512px with crunched compression. Default and Android import settings are untouched, so the mobile build is unaffected.
- Files are `.unityweb`, decompressed by Unity's loader in JavaScript. Do **not** configure the server to send `Content-Encoding: br` for them — the loader would then decompress already-decompressed data and the game would fail to start.

## Size history

| Change | Download |
|---|---|
| Uncompressed, default template | 186 MB |
| Brotli | 110 MB |
| Brotli + 512px crunched textures | **66 MB** |
