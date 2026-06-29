# PENUMBRA · Music Visualizer

A single-file, no-build, in-browser **music visualizer** with a hacker / eclipse aesthetic. Drop in a track (or capture a live stream), pick a visual, and it reacts to the real audio in real time — neon spectra, a 3D triangular-peaks terrain, code rain, aurora curtains, and an Unreal-Engine-style debug HUD with live BPM, key, and a beat timeline.

No install, no dependencies, no server — it's one `index.html`. Everything runs **100% locally**; nothing is uploaded.

### ▶ Demo

[![PENUMBRA Music Visualizer — demo](https://img.youtube.com/vi/qXSvnXlZAhg/hqdefault.jpg)](https://youtu.be/qXSvnXlZAhg)

*(click for the full demo video)*

---

## 🚀 How to use it (the dead-simple version)

**No coding. No installing. It's just one file you open in your web browser.**

### Step 1 — Get the file
- Scroll up, click **`index.html`** in the file list above.
- On that page, click the **download icon** (⬇, near the top-right — it may say *"Download raw file"*).
- Save it somewhere easy to find, like your **Desktop**.

> Prefer one download? Click the green **`<> Code`** button at the top of the repo → **Download ZIP** → unzip it → the file is inside.

### Step 2 — Open it
- **Double-click `index.html`.** It opens in your web browser. That's the whole app. Done.
- *(If it opens in a code editor instead, right-click it → **Open with** → **Chrome** or **Edge**.)*

### Step 3 — Play a song
- **Drag a music file** (an `.mp3`) from your computer **onto the window.** It starts playing and reacting immediately.
- Or click the **▶ Load Songs** button and pick your files.

### Step 4 — Make it look cool
- **Move your mouse** to show the controls at the bottom (they hide while it plays).
- Use the **dropdown menu** to pick a different visual.
- Click the colored **dots** to change colors; drag the **sliders** to change the feel.
- Click the **picture itself** to pause/play.

### 🎧 Want to visualize YouTube Music or Spotify instead of a file?
1. Start playing music in YouTube Music / Spotify in another browser tab.
2. In the visualizer, click the **🎙️ microphone button**.
3. A pop-up appears — pick the **tab that's playing music**, and **✅ check the box that says "Share tab audio,"** then click **Share**.
4. The visuals now react to whatever's playing in that tab.

> ⚠️ If the visuals look flat/dead while doing this, you forgot to check **"Share tab audio."** This part works best in **Chrome or Edge**.

### 🎥 Want to save a video of it?
- Click the **⏺ record button** to start, then click it again to stop. It saves a video file you can upload to YouTube.

### Button cheat-sheet (bottom bar)
| Button | What it does |
|---|---|
| **▶ / ⏸** | Play / pause (or just click the picture) |
| **🎲** | Auto mode — randomly cycles visuals for you |
| **🎙️** | Capture audio from another tab (YouTube Music, etc.) |
| **🔬** | Analyze the song's BPM & musical key |
| **⏺** | Record a video |
| **☰** | Open the playlist / queue |
| **🎬** | Add a background video or image |
| **⛶** | Fullscreen |

### If something's not working
- **Nothing on screen?** Load a song first, and make sure it's playing (click the picture).
- **No sound or no reaction?** Check your volume, and that the right song/tab is selected.
- **Use Chrome or Edge.** Some features (like tab-audio capture) don't work in other browsers.
- Everything runs **on your own computer** — no internet upload, nothing leaves your machine.

---

## Screenshots

| Triangular Peaks | Eclipse Core |
|---|---|
| ![Triangular Peaks](docs/01-triangular-peaks.png) | ![Eclipse Core](docs/02-eclipse-core.png) |

| Aurora Flow | Code Rain |
|---|---|
| ![Aurora](docs/03-aurora.png) | ![Code Rain](docs/04-code-rain.png) |

| Radial Spectrum | Particle Burst |
|---|---|
| ![Radial Spectrum](docs/05-radial-spectrum.png) | ![Particle Burst](docs/06-particle-burst.png) |

---

## Features

- **Real audio reactivity** — Web Audio `AnalyserNode` FFT drives every visual off the actual frequency/waveform data.
- **9 visualization modes** (see below), each with neon glow, trails, and the Penumbra palette.
- **Penumbra HUD overlay** — corona-bracket frame, header strip, a `void MEDIA::Playing("track")` now-playing readout with progress bar, live BASS/LVL meters, BPM, musical key, and a scrolling beat timeline.
- **Offline track analysis** — decodes the file and computes **BPM** (onset-envelope autocorrelation) and **musical key** (full-track chroma + Krumhansl-Schmuckler), **cached in `localStorage`** so each song is analyzed once.
- **Live audio capture** — visualize **streamed audio** (YouTube Music, Spotify web, anything) by capturing tab/system audio.
- **Playlist / queue** — load many tracks, drag-and-drop, auto-advance, prev/next.
- **Video recording** — capture the canvas + audio to a downloadable `.webm` (great for mix-video intros / now-playing scenes).
- **Auto / random mode** — shuffles visuals + settings on a timer, hands-free.
- **Backgrounds** — optionally composite visuals over a looping video or image (non-Penumbra modes).
- **Live controls** — reactivity, trails, color-shift speed, visualizer height, brightness, volume, 5 color themes.

## Visualization modes

**Penumbra**
- **Triangular Peaks** — a wide 3D perspective lattice of equilateral triangles (hex tiles) where the spectrum radiates from the center into a mountain of peaks, with vertical laser streaks and flowing color.
- **Eclipse Core** — the signature pulsing corona ring with the spectrum as corona spikes.
- **Code Rain** — Matrix-style falling C++/hex glyphs whose fall speed tracks the music.

**Spectrum**
- Radial Spectrum · Waveform · Mirror Bars · Pulse Rings · Tunnel Grid · Particle Burst · Aurora Flow

## Usage

1. Open `index.html` in a modern browser (Chrome/Edge recommended).
2. **Load tracks** (button or drag-and-drop MP3/WAV/OGG). Optionally load a background video/image.
3. Pick a visual from the dropdown, hit play, and tweak the sliders.
4. **Click the visualization** to play/pause. Mouse-away hides the controls.

### Visualizing streamed audio (YouTube Music, etc.)
Click **🎙️**, choose the tab playing audio, and **tick "Share tab audio."** The visualizer reacts to that stream live. (Offline BPM/key analysis only works on local files; streams show the live estimate. Tab-audio capture is a Chrome/Edge feature.)

### Recording
Click **⏺** to record the canvas + audio to a `.webm`. Click again to stop and download. YouTube accepts `.webm` directly.

### Keyboard
`Space` play/pause · `F` fullscreen · `H` toggle HUD · `←/→` seek ±5s

## Tech

- Pure HTML/CSS/JS in a **single file** — no build step, no frameworks, no dependencies.
- **Web Audio API** (`AnalyserNode`, `MediaElementSource`, `MediaStreamSource`, `MediaStreamDestination`) for analysis, capture, and recording.
- **Canvas 2D** with an offscreen FX layer composited via `lighten`/`screen` blends for the glow.
- A small in-file **FFT** powers the offline BPM/key analyzer.
- **JetBrains Mono** + the Penumbra palette (corona teal, void purple-black, vaporwave-Rider syntax colors).

## License

See repository license. Part of the **Penumbra** stream toolkit.
