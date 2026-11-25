# TRACE://ME

A cybersecurity awareness demo that runs in the browser. It shows visitors how much information a website can read from their device without asking, then explains that none of it was stored or sent anywhere.

## Description

The page opens with a retro terminal screen. After the visitor clicks to continue, it types out the information their browser exposes, section by section, then ends with a short message on staying safe online. An optional camera step takes a single photo, shows it briefly in pixelated form, and then discards it.

## What the Demo Displays

| Section | Information shown |
|---------|-------------------|
| Network | IP address, IP type (IPv4/IPv6), ISP, ASN |
| Location | Approximate location derived from the IP address |
| Device | Device type, OS, model, CPU architecture and cores, touch support, GPU, battery level and charging state, number of cameras and microphones |
| Screen | Resolution, dark mode, input type |
| Browser | Browser name, preferred languages |
| Visit | Local time, time zone, UTC offset, locale, referrer |
| Fingerprint | A short hash combining several browser properties, and the user agent string |

Values the browser does not report are left out rather than guessed.

## Camera Step

After the data is shown, the page asks for camera access through the browser's standard permission prompt. If the visitor allows it:

1. One frame is captured from the front camera.
2. The image is displayed as a pixelated photo that gradually sharpens.
3. The camera is turned off immediately after capture, and the image data is cleared from memory when the sequence ends.

If access is denied, the page shows "CAMERA BLOCKED. GOOD." and continues. The photo is never uploaded or saved. This step can be disabled (see Configuration).

## Privacy

- All information is read by the visitor's own browser and shown only on their screen.
- Nothing is stored, logged, or sent to the page owner.
- The only external requests are the IP and location lookups to [ipwho.is](https://ipwho.is/), with [ipify](https://www.ipify.org/) as a fallback, and the Press Start 2P font from Google Fonts.

## Getting Started

1. Clone or download this repository.
2. Place the sound file `ui-sci-fi-loading-numbers-scan-shimmer-tail-08.wav` in the same folder as `index.html`. Without it, the page still works but the typing sound is silent.
3. Open `index.html` in a browser, or serve the folder locally:

```bash
python -m http.server 8000
```

Then visit `http://localhost:8000`.

Camera access requires a secure context, so use `https://` (for example GitHub Pages) or `localhost`.

## Hosting on GitHub Pages

1. Go to **Settings → Pages**.
2. Under **Source**, choose your main branch and the root folder.
3. The demo will be available at `https://<your-username>.github.io/<your-repo>/`.

## Configuration

The options are at the top of the script in `index.html`:

| Option | Default | Effect |
|--------|---------|--------|
| `CAMERA_PRANK` | `true` | Set to `false` to remove the camera step |
| `GEO_ENABLED` | `true` | Set to `false` to skip the IP and location lookup |
| `SLOW` | `1` | Typing speed multiplier; higher values type more slowly |
| `TYPE_SOUND` | `ui-sci-fi-loading-...wav` | File name of the typing sound |

## Accessibility

- The start button can be activated with mouse, touch, or the Enter and Space keys.
- Motion effects are reduced when the visitor's system has "reduce motion" enabled.

## Browser Support

Works in modern browsers. Some details (battery status, device model, CPU architecture) are only available in certain browsers, such as Chromium-based ones, and are omitted when unavailable.

## Disclaimer

This project is intended for education and awareness only. It does not collect, transmit, or store personal data. Use it only to teach others about online privacy, and make sure people know what to expect before they take part.

## Tech Stack

- HTML, CSS, and vanilla JavaScript (no frameworks, no build step)
- Web Audio API and HTML audio for sound effects
- `getUserMedia` for the optional camera step

## License

Add your preferred license here (for example, MIT).
