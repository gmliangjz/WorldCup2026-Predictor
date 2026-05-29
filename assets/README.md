# `assets/` — local audio (optional)

The app has a background-music player, but **no audio is bundled** with this
repository — copyrighted tracks (e.g. official World Cup songs) must never be
committed to a public repo. They'd risk a DMCA takedown and bloat the page.

## To enable music locally

Drop your own audio files here, named exactly:

```
assets/music-1.mp3
assets/music-2.mp3
assets/music-3.mp3
assets/music-4.mp3
```

Use tracks you have the rights to (your own, royalty-free, or CC0). The player
loads them lazily (`<audio preload="none">`) — nothing is fetched until you
click the music button.

If no files are present, the music button simply shows a toast
("Add MP3 files to assets/ to enable music") and the rest of the app works fine.

## Why these are git-ignored

`.gitignore` excludes `assets/*.mp3` / `*.wav` / `*.m4a` / `*.ogg` so your local
tracks stay on your machine and never get pushed. This file (`README.md`) is the
only thing in `assets/` that's committed.
