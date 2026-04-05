# ascii-renderer

Convert any video into real-time ASCII art in the browser. No installs, no server — runs entirely client-side.

**[→ Open the app](https://stink-o.github.io/ascii-renderer/)**

---

```
@#S%?*+;:,.   @#S%?*+;:,.   @#S%?*+;:,.
%?*+;:,. @#   %?*+;:,. @#   %?*+;:,. @#
+;:,. @#S%?   +;:,. @#S%?   +;:,. @#S%?
```

---

## What it does

Drag in a video file and watch it render as a stream of ASCII characters, sampled directly from each frame. The output can be tweaked in real time and exported back to a `.webm` video using the browser's WebCodecs API — no quality loss from screen recording.

## Features

| Control | What it does |
|---|---|
| **cols** | Horizontal character resolution (40–200) |
| **size** | Font size — affects both grid density and glyph scale |
| **ramp** | Character set: `dense` · `sparse` · `blocks` · `braille` |
| **color** | Toggle between greyscale and per-character RGB |
| **rand** | Randomly swap characters for a glitchy, noisy look |
| **vary** | Randomly scale rows for an organic, warped feel |
| **bg** | Fill the text grid with a background color |
| **mask** | Add draggable circles or rectangles — text reflows around them |
| **export** | Encode the full video to `.webm` (AV1 → VP9 fallback) at native resolution |

## Export

The exporter runs faster than real-time by stepping through frames with `requestVideoFrameCallback`. Output is encoded with `VideoEncoder` using a quantizer of 20 (near-lossless for text edges) and muxed to WebM with [`webm-muxer`](https://github.com/Vanilagy/webm-muxer).

## Browser support

Requires a Chromium-based browser (Chrome 94+, Edge 94+) for WebCodecs export. Firefox can view and interact but cannot export.

## Running locally

```bash
npx serve .
```

Then open `http://localhost:3000`.

## Stack

- [`@chenglou/pretext`](https://github.com/chenglou/pretext) — fast canvas text layout with correct glyph metrics
- [`webm-muxer`](https://github.com/Vanilagy/webm-muxer) — pure-JS WebM muxer
- WebCodecs API (`VideoEncoder`, `VideoFrame`)
- No build step
