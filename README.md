# Maison Vell — Runway Depth Lookbook

A single-file, full-viewport fashion page. Six models stand in one line that recedes into a blurred distance; drag, scroll or press the arrow keys to walk the line forward. The product rail and look number follow. It loops forever.

<img width="1918" height="893" alt="image" src="https://github.com/user-attachments/assets/0608fb8d-5a3f-47a8-a4c0-9a44ddbdc003" />


## Run

Open `index.html` in a browser. No build step, no libraries. It needs a network connection for the Google Fonts and the two image sheets.

## Controls

| Input | Action |
|---|---|
| Drag | Moves the line directly; release snaps to a whole look |
| Wheel | Moves the line; snaps 150 ms after the last event |
| Right / Down | Next look |
| Left / Up | Previous look |
| Click a model | Jump to that look |

Reduced-motion users get instant jumps instead of easing.

## How it works

- **One number drives everything.** `p` is the current look position; each model's depth is `wrap(i - p, 6)`. Models, product rail and look number are all computed from `p`.
- **Depth is a table.** Position, size, blur and opacity are interpolated from seven stops (depth -1 to 5): `KX`, `KF`, `KH`, `KB`, `KO`.
- **Sprite sheets.** All models come from one image and all products from another, cropped with nested `<svg viewBox>`.
- **Layers scale, they don't resize.** Models are laid out once at 1.2 × stage height and only `transform` changes; blur is divided by the scale.
- **Drag is direct, release snaps.** `p` chases `target` with an exponential ease.
- **The rail wraps.** Twelve cards on one looping track.

## Customising

All data lives at the top of the script in `index.html`:

- `MODELS` / `PIECES` — sheet URLs
- `LOOKS` — x-range of each model on the 960 × 540 sheet
- `ITEMS` — crop box, name and price of each product on the 960 × 720 sheet
- `KX`, `KF`, `KH`, `KB`, `KO` — the depth table

## Layout

Desktop sizes scale with `--u` (viewport-based unit). At 820px wide and below, `--u` is `1px`, the tabs and paragraph are hidden, and the product rail becomes a horizontal strip along the bottom.
