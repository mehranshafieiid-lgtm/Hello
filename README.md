# SONORA — Sketch Edition

SONORA is a static music-player PWA. This edition keeps the existing audio playback, lyrics parsing, lyric export/import, GitHub music cache, full-screen lyrics and offline shell, while reorganizing the interface around the supplied desktop music-library sketch.

## Interface

- Top playback strip with previous / play / next, current track metadata, volume and app icon.
- Left navigation for Home, Songs, Playlists, Artists, Albums, Search, Lyrics, Saved, Lyric Maker and Settings.
- Playlist view with artwork, title, description, track count and a track table (song, artist, album, duration).
- Lower now-playing artwork / metadata panel beside the synchronized lyrics panel.
- Responsive layout for phones; the navigation becomes a compact bottom bar.

## Playlists, artists and albums

Artists and albums are grouped automatically from the audio-file metadata when available. Playlists can be created, renamed, deleted, and populated with the currently playing song or individual tracks from the Home table. Playlist membership and names are stored in this browser's local storage; the audio files themselves are not copied to GitHub.

## Persian AI translation without an API key

The **Translate to Persian** control beside the lyrics uses Transformers.js and the multilingual `Xenova/nllb-200-distilled-600M` model. Translation inference runs in the browser on the user's device; no Gemini key, API key, hosted inference endpoint or translation API is required. The model files are downloaded from Hugging Face the first time the feature is used and then cached by the browser. This is a large model (the first download can be several hundred MB or more depending on selected quantized assets), and translation speed depends on the phone/computer. Internet is required for the initial model download; after it is cached, inference can run locally. The model is optimized for multilingual translation, not lyric-specific creative adaptation.

## GitHub Pages

1. Upload the contents of this ZIP to the root of the repository (not the ZIP file itself).
2. In **Settings → Pages**, publish branch `main` from `/(root)`.
3. Wait for deployment and open the GitHub Pages URL.
4. In **Actions**, enable the `Sync SONORA music cache` workflow if GitHub asks.

The existing GitHub Music Cloud settings remain in Settings. The phone reads cached catalog data and artwork from the configured GitHub repository. A fine-grained token with Contents read/write permission is required only for queuing new cache requests. Never publish that token in the repository.

## Notes

- Audio files stay on the device and are never included in the lyric export ZIP or GitHub cache.
- Playlists currently stay local to each browser/device; they are not synchronized through GitHub.
- The on-device AI translation model is separate from lyric fetching. LyricsPlus / LRCLIB / iTunes cache behavior remains as in the previous build.
- The model download needs an internet connection the first time. WebGPU is attempted where available; WASM is used as fallback.


## Persian lyric translation

Persian translation uses the hosted MyMemory Translation API directly from the browser (`api.mymemory.translated.net`). No translation model is included in this repository, downloaded by GitHub Actions, or run on GitHub. No API key is required for anonymous use; the published anonymous quota is 5,000 characters per day. Translations are cached locally in the browser. MyMemory is a machine-translation API, not a generative AI/LLM service.
