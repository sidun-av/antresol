# Antresol

**English** · [Русский](README.ru.md)

Antresol is a self-hosted home media server and a player app for iPhone, iPad and Mac. It organises and plays the films, TV shows, music, books, audiobooks and comics you keep on your own computer or NAS, in one clean, native library. No content is provided.

- Website: https://sidun-av.github.io/antresol/
- Install guide: https://sidun-av.github.io/antresol/install.html
- Support: https://sidun-av.github.io/antresol/support.html
- Privacy policy: https://sidun-av.github.io/antresol/privacy.html

## Features

- **Films and TV shows** — pick up where you left off, Picture in Picture, AirPlay, subtitles and audio tracks, quality that adapts to the network.
- **Music** — albums, artists, playlists, favourites and lyrics; background playback.
- **Books and comics** — EPUB, FB2, MOBI/AZW3 (DRM-free), PDF and CBZ, with themes, contents, search and bookmarks.
- **Audiobooks** — chapters, speed, sleep timer; the position syncs across devices.
- **Offline** — save a film, an album or a book to the device before a trip.
- **Family** — profiles with passwords and kid profiles with age limits.
- **Web app** — the same library in any browser, installable as a PWA.

## Install the server

The server is a single executable with the web interface built in. It needs `ffmpeg`.

### Docker (recommended)

```sh
docker run -d --name antresol --restart unless-stopped \
  -p 8420:8420 \
  -v /path/to/config:/config \
  -v /path/to/library:/media \
  -e VAULT_MEDIA_ROOT=/media \
  ghcr.io/sidun-av/antresol-server:latest
```

The image is built for `linux/amd64` and `linux/arm64` and includes `ffmpeg`.

### Ready-made binary

Download the archive for your system from [Releases](https://github.com/sidun-av/antresol/releases/latest) (Linux x86-64 and ARM64, macOS Apple Silicon and Intel), install `ffmpeg` and run:

```sh
VAULT_DATA_DIR=~/antresol/config VAULT_MEDIA_ROOT=~/antresol ./antresol-server
```

On macOS the binary is not signed yet: before the first run, execute `xattr -d com.apple.quarantine antresol-server`.

## First run

1. Open `http://<computer-address>:8420` in a browser and create the administrator.
2. Put your files into these folders inside `VAULT_MEDIA_ROOT` (with Docker, inside the folder you mount as `/media`, for example `/path/to/library/media/movies/`):

   | Folder | Contents |
   |---|---|
   | `media/movies/` | films, one folder per film |
   | `media/series/` | TV shows: `Title/Season 01/…S01E01…` |
   | `media/music/` | music: `Artist/Album/` |
   | `media/books/ebooks/` | EPUB, FB2, MOBI/AZW3 and PDF books |
   | `media/books/audiobooks/` | audiobooks, one folder per book |
   | `media/books/manga/` | comics and manga in CBZ |

3. Create profiles for your family. Give kid profiles an age limit.
4. Install the Antresol app on iPhone, iPad or Mac and enter the server address.

## Main settings

| Variable | Meaning |
|---|---|
| `VAULT_DATA_DIR` | the server's database and settings |
| `VAULT_MEDIA_ROOT` | the root of the library |
| `VAULT_LISTEN` | address and port, `:8420` by default |
| `VAULT_PUBLIC_URL` | the server's https address on the internet, if it has one |
| `VAULT_TMDB_KEY` | a The Movie Database key for posters and descriptions (optional) |

For access over the internet, use https through a reverse proxy or a VPN such as Tailscale.

## Privacy

The developer collects no data. The app talks only to the server address you enter; the server runs on your hardware and is controlled by you. Details: [privacy policy](https://sidun-av.github.io/antresol/privacy.html).

## Support

Questions and bug reports: [Issues](https://github.com/sidun-av/antresol/issues). We answer in English and Russian.

## Licence

See [LICENSE](LICENSE). Third-party licences: [THIRD_PARTY_LICENSES.md](THIRD_PARTY_LICENSES.md), also included in every release archive.

Only add media you have the rights to.
