# ESP32 OLED Video Converter

A browser-based tool that converts any video file into a 1-bit animation you can play back on a 128×64 SSD1306 / SH1106 OLED display driven by an ESP32.

Everything runs client-side — no upload, no server, no install. Open `index.html` in a browser, drop in a video, tune the image, and export ready-to-flash Arduino code.

**[Live demo →](https://<your-username>.github.io/<your-repo-name>/)**

---

## Features

- **Drag-and-drop video upload** (.mp4, .mkv, .webm, etc.)
- **Trim range** — pick a start/end so you only convert the loop you actually want
- **5 dithering modes** — Solid Threshold, Bayer 8×8, Floyd–Steinberg, Atkinson, Halftone Dots
- **Scale modes** — Best Fit, Fill/Cover with panning, Stretch, or fully custom size & position
- **Image tuning** — brightness, contrast, gamma, B/W threshold, line/text thickness, invert
- **90° rotation** for portrait clips
- **Live 128×64 preview** as you adjust settings
- **Frame-by-frame thumbnail strip** after export, so you can sanity-check the result
- **Flash-size estimate** with a warning if the generated array is too large for a typical ESP32 partition
- **One-click copy or download** for both generated files

## Usage

1. Open `index.html` (locally or via the GitHub Pages link above).
2. **Upload & Trim** — load your video, optionally trim it, set FPS and scale mode.
3. **Tune Image** — pick a dithering method and adjust brightness/contrast/gamma/threshold until the live preview looks right on the simulated OLED.
4. **Export Code** — click *Extract Frames & Generate Code*. Copy or download the two generated files:
   - `VideoFrame.h` — the frame data as a `PROGMEM` byte array
   - `Main.ino` — the Arduino sketch that plays it back
5. In the Arduino IDE, create a sketch folder containing both files, install the **Adafruit GFX** and **Adafruit SSD1306** (or **Adafruit SH110X**) libraries, select your OLED driver at the top of `Main.ino`, and upload.

## Hardware

- ESP32 dev board
- SSD1306 or SH1106 OLED display, 128×64, I²C
- Wiring: `SDA`/`SCL` to your board's default I²C pins, `VCC`→3.3V, `GND`→GND

## Notes on flash size

Each frame is 1024 bytes (128×64 ÷ 8). A 10 fps, 5-second clip is ~50 KB; a full-length clip at high FPS can easily exceed what fits in `PROGMEM` on a typical ESP32 partition. Use the trim range and the on-screen size estimate to stay within budget, or lower the FPS.

## License

MIT — do whatever you like with it, attribution appreciated.
