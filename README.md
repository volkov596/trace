# TRACE

Browser tool for turning accelerometer data into deflection traces. Reads GoPro telemetry or CSV. No backend, no install, nothing uploaded.

**Current version: v1.3.0**

## Features

- **GoPro import** — extracts accelerometer telemetry (GPMF) straight from MP4, HERO5 and later
- **CSV import** — auto-detects separator, decimal comma, header rows, and time units (s / ms / µs)
- **Double integration** — acceleration → velocity → displacement, time-domain or frequency-domain
- **Zero-phase high-pass filter** — Butterworth, forward-backward, with a cutoff indicator and "set from peak"
- **Dominant frequency** — Welch spectrum with interpolated peak, shown live
- **Readout** — amplitude (√2·RMS), peak displacement with time, dominant frequency for the visible range
- **Event window** — trim to the crossing or event by slider, typed times, or plot zoom
- **Warnings** — flags windows that start or end mid-vibration, short windows, data gaps, and skipped rows
- **Video sync** — plays the GoPro clip beside the traces with a moving playhead, frame step, and sync offset
- **Graph navigation** — pan, stretch the time axis, pinch or Ctrl+wheel zoom; every sample drawn when zoomed
- **Built-in test signal** — known 12 mm, 1.3 Hz answer for checking the pipeline
- **Export** — processed CSV and PNG of the plots

## How it works

- Single self-contained HTML file — vanilla JS, no framework, no build step
- Runs entirely in the browser; files are read locally and never leave the device
- Plotly loaded from CDN; GoPro parser loaded on first MP4 only

## Usage

1. Open the file in a browser (or use the hosted version)
2. Load a GoPro MP4, a CSV, or the test signal
3. Set the event window so it starts and ends with the structure at rest
4. Adjust the high-pass cutoff until the indicator is green
5. Read amplitude and frequency, export CSV or PNG

GoPro MP4 import needs the hosted version or a local server:

```
python -m http.server 8000
```

## Limits

- **Dynamic component only** — recovers oscillating deflection, not static or quasi-static settlement
- **Quiet margins required** — the window must start and end at rest; otherwise displacement is inflated 2–5×

See the guide (`trace-guide-v1.3.0.html`) for details.

## Compatibility

Works in current versions of Chrome, Edge, Safari, and Firefox on desktop and tablet. GoPro video playback depends on browser H.265 support (Firefox usually cannot play it; data is unaffected).

## Status

DSP core, CSV import, graph navigation, and video sync are tested against known signals and pass. Live GoPro MP4 import has not yet been tested with a real GoPro file.

## Privacy

All data stays on the device. No account, no upload, no tracking.
