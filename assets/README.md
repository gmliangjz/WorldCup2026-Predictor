# `assets/` — background music (optional)

The app has a background-music player, but **no audio is bundled** with this
repository — copyrighted tracks (e.g. official World Cup songs) must never be
committed to a public repo. They'd risk a DMCA takedown and bloat the page.

## On the live site: play your own music

Click the ▶ music button. If the site has no bundled tracks (the public one
doesn't), a prompt offers **Choose music** — pick one or more audio files from
your device and they play as a playlist (⏭ skips). The files are played
locally in your browser via object URLs: **nothing is uploaded**, and the
choice is forgotten when you close the tab.

## In your own copy: a default playlist

If you run the app yourself, you can drop audio files here, named exactly:

```
assets/music-1.mp3
assets/music-2.mp3
assets/music-3.mp3
assets/music-4.mp3
```

Use tracks you have the rights to (your own, royalty-free, or CC0). The player
loads them lazily (`<audio preload="none">`) — nothing is fetched until you
click the music button. When they're missing, the button falls back to the
"choose your own music" prompt above, and the rest of the app works fine.

## Why these are git-ignored

`.gitignore` excludes `assets/*.mp3` / `*.wav` / `*.m4a` / `*.ogg` so your local
tracks stay on your machine and never get pushed. This file (`README.md`) is the
only thing in `assets/` that's committed.
