# π Typewriter

A LinkedIn cover photo generator that types live digits of π onto a canvas, pulled in real time from Google's [pi.delivery](https://pi.delivery) API.

The output is exactly **1584 × 396 px** — LinkedIn's recommended cover photo size — and can be downloaded as PNG with a single click. The entire project is one self-contained HTML file: no build step, no dependencies, no framework.

## Demo

Open `index.html` in any modern browser.

## What it does

- Types π digits into a fixed 1584 × 396 grid (LinkedIn cover photo size, pixel-exact)
- Walks through π sequentially starting at digit 0
- When the canvas fills, wraps to the top row and overwrites character by character
- Pulls fresh digits live from `api.pi.delivery` (Google's 100-trillion-digit π dataset)
- Falls back to a built-in 1000-digit cache if offline

## Controls

| Button | Effect |
| --- | --- |
| Download PNG | Exports the current frame as a 1584 × 396 PNG, ready to upload to LinkedIn |
| Restart | Clears the canvas and resumes typing from π₀ |
| Pause / Resume | Freezes the animation in place |
| Palette | Cycles through 5 themes (navy/purple/grey, cyan/violet, navy/mint, solar/ultraviolet, arctic/aurora) |
| Density | Cycles through sparse / medium / dense character grids |
| Speed | Cycles through slow / normal / fast typing rates |

## How it works

A vanilla 2D canvas driven by a `requestAnimationFrame` typewriter loop:

1. On setup, the character grid is computed so it fills 1584 × 396 exactly — no edge gaps.
2. Each frame paints N more π digits at the current `(row, col)` position.
3. The most recent character is highlighted in the accent color (the moving "cursor").
4. When the local buffer runs low (< 1500 digits ahead), the next 5000 digits of π are fetched sequentially from `api.pi.delivery` starting at `piBuffer.length`.

Total: ~290 lines of HTML, CSS, and JavaScript combined.

## Embed it on your own site

The whole animation is one `<canvas>` + one `<script>`. Copy both blocks into any page, size the canvas via CSS or its `width`/`height` attributes, and you're done.

## License

[MIT](LICENSE)

## Author

[Naya Fytali](https://nayafyt.com) · [github.com/nayafyt](https://github.com/nayafyt)
