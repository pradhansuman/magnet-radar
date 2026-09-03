# 🧲 MagnetRadar

A single-file web app that lists the **latest torrents** with **ready-to-copy magnet links**, plus in-browser streaming and downloads.

## Features

- 🎬 **Movies** — latest YTS additions; every quality variant (2160p / 1080p / 720p…) listed as its own torrent with its own magnet
- 📺 **TV Shows** — latest EZTV releases with official magnet URLs
- 🔍 **Search All** — full-text search across all categories (Torrents-CSV)
- ▶ **Play** — stream video in the browser via the WebTorrent engine (WebRTC peers)
- ⤓ **Downloads** — save individual files from a torrent, save the generated `.torrent`, or hand the magnet to your desktop client (qBittorrent, WebTorrent Desktop…)
- ⧉ **Copy magnet** / **Copy all magnets** — one row or the whole list
- Filters: quality, min seeds · sorting: newest / most seeded / largest · pagination · optional 60s auto-refresh · IMDb links

## Run it

No build step, no backend, no dependencies.

- **Locally:** double-click `index.html`. That's it.
- **Host it:** any static host works.
  - **Cloudflare Pages:** Workers & Pages → Create → Pages → *Connect to Git* → pick this repo → build command: *(none)*, output dir: `/` → Deploy
  - Or drag-and-drop the folder into Cloudflare Pages *Direct Upload*

## Data sources (public, CORS-enabled)

| Source | Used for |
|---|---|
| [YTS API](https://yts.mx/api) | Movies (hosts: `yts.gg` → `yts.mx` → `movies-api.accel.li` auto-fallback) |
| [EZTV API](https://eztvx.to/) | TV shows |
| [Torrents-CSV](https://torrents-csv.com/) | Cross-category search |

Everything runs client-side in your browser — nothing is proxied or logged. The WebTorrent streaming engine is lazy-loaded from jsDelivr on first ▶ Play.

## Browser streaming — honest limits

- Browsers speak only **WebTorrent (WebRTC)**. If a swarm has no browser peers, streaming can't start — the app tells you and suggests the magnet/Open route with a desktop client instead. This is a browser-protocol limit, not a bug.
- MP4 / WebM / M4V stream instantly (MediaSource). MKV / AVI and other containers download fully before playback.
- Since v3 of WebTorrent requires a Service Worker, this app pins [webtorrent@1.9.7](https://cdn.jsdelivr.net/npm/webtorrent@1.9.7/webtorrent.min.js), whose `file.appendTo` streaming works from both `file://` and hosted HTTPS.

## Legal

Share only what's legal to share: public-domain and open-source releases, Creative-Commons media, and your own files. Respect the law where you live.

## License

MIT
