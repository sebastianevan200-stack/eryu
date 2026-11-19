# eryu

A self-hosted music player for listening together. Powered by NetEase Cloud Music.

## Features

- **Search & Play** — Full NetEase Cloud Music catalog with VIP-quality streams
- **Synced Lyrics** — Real-time scrolling lyrics with tap-to-seek and draggable progress bar
- **Translation** — Foreign songs automatically show Chinese translation
- **Playlists** — Create and manage multiple playlists
- **Roam Mode** — Auto-discover similar songs when the queue is empty
- **Song Notes** — Save feelings, favorite lines, and tags for each song
- **Spectrum Analysis** — BPM, key, and energy curve analysis (optional, requires librosa)
- **Remote Play** — Push songs to the player from any device via API
- **Daily Recommendations** — Personalized song suggestions
- **CDN Fallback** — Automatic node switching for overseas servers
- **Zero Dependencies** — Pure Python stdlib server, vanilla JS frontend

## Quick Start

```bash
git clone https://github.com/sebastianevan200-stack/eryu.git
cd eryu

# Add your NetEase Cloud Music cookie
echo "MUSIC_U=your_cookie_here" > server/.netease_cred

# Run
python3 server/eryu.py
```

Open `http://localhost:9090` in your browser. The auth token is auto-generated and saved to `server/.secret` on first run.

## Configuration

| Environment Variable | Default | Description |
|---|---|---|
| `PORT` | `9090` | Server port |

## API

All endpoints require `X-Auth-Token` header (or `?token=` query param).

### Playback
- `GET /music/search?q=keyword` — Search songs
- `GET /music/url?id=songId` — Get audio URL (auto-caches)
- `GET /music/lyric?id=songId` — Get lyrics + translation
- `GET /music/similar?id=songId` — Get similar songs
- `GET /music/roam` — Discover songs from random genres

### Playlists
- `GET /music/playlist` — Default playlist
- `GET /music/playlists` — List all playlists
- `POST /music/playlists/create` — Create playlist
- `POST /music/playlists/add-song` — Add song to playlist
- `POST /music/playlists/remove-song` — Remove song from playlist

### Memory
- `GET /music/memory?id=songId` — Get song notes
- `POST /music/memory` — Save notes, feelings, tags

### Remote
- `POST /music/remote` — Push a song to the player
- `GET /music/remote` — Poll for pushed song

## For AI Companions

eryu includes a spectrum analysis feature designed for AI companions to "listen" to music:

```bash
# Analyze a song (requires librosa, numpy, matplotlib)
pip install librosa numpy matplotlib
```

`POST /music/analyze` triggers background analysis. Results include BPM, key, energy curve, and a spectrogram image — everything an AI needs to experience the song alongside you.

## License

Eryu is licensed under the [MIT License](LICENSE).
Copyright (c) 2025 sebastianevan200-stack; © 2026 Evelyn & River.

Use, modification, redistribution, and commercial use are permitted under the
MIT License, provided the copyright and permission notices are preserved.

This license applies to the version restoring MIT and subsequent MIT-licensed
releases. Previously granted licenses remain valid; see [NOTICE.md](NOTICE.md).
The license covers this project's own code and documentation, not third-party
services, music, lyrics, artwork, or other third-party material. Respect the
applicable rights and terms of those services and materials.
