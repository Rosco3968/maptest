# WCESD#3 Street Recognition Trainer

A study tool for memorizing the 120 streets in your response area, styled like a CAD dispatch terminal. Two ways to train:

- **Find It On The Map** — the actual Hutto Fire Rescue / WCESD#3 map is loaded on the page. You get a street name and have to zoom/pan and click where it actually is.
- **Study Mode** — the original flashcards / multiple choice / type-it drills, for pure name memorization.

## Files
- `index.html` — the page
- `map.jpg` — the rasterized fire box map (rendered from your PDF)
- `streets-data.js` — click-target coordinates for the map game

All three need to stay in the same folder — the page loads the other two by relative path.

## Try it locally
Open `index.html` in your browser (works straight off disk, no server needed).

## Put it on GitHub Pages
1. Create a new repo on GitHub (e.g. `street-trainer`).
2. Add **all three files** — `index.html`, `map.jpg`, and `streets-data.js` — to the repo (drag-and-drop upload works fine, or `git add` / `git commit` / `git push` if you're using the command line).
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.
5. GitHub gives you a URL like `https://yourusername.github.io/street-trainer/` within a minute or two — that's your live quiz page.

## How "Find It On The Map" works
You're given a street name and have to click its actual location on the map. Zoom in/out with the +/− buttons, drag to pan (or just scroll on mobile). Green ring = correct, red X = miss (you get a rough "close / same neighborhood / way off" hint based on distance). "Hint" gives a general compass direction; "Reveal & next" shows you the answer and moves on.

All **120** streets from your list are playable:

- **111 of them** have click zones extracted directly from the original PDF's text layer — precise, pixel-accurate to where the label is actually printed.
- **9 of them** (Big Sandy Creek Dr, CR 131, Destiny Ln, Durango Downs Dr, Emory Crossing Blvd, Flora Blvd, Jacobs Well Dr, Redfish Ln, Rock Daisy Trl) aren't printed as labels anywhere on this particular map — they're too new, outside the label density ArcMap chose to render, or just outside this map's exact coverage boundary. For those, I geocoded the real street from public map data, then calibrated that against ~9 known label positions on this same map to estimate where they'd fall. Their click zones are marked with a blue ring instead of green and get a bigger margin for error, plus a note when they come up, since the position is an estimate rather than a confirmed label match.

If you'd rather those 9 be spot-on instead of estimated, the fix would be pulling a higher-resolution or more recent version of this map (some newer subdivisions may not have made it onto this print), or manually pinning them yourself if you know exactly where they are.

## How Study Mode works
- **Mixed** — cycles randomly between all three quiz types (default).
- **Flashcards** — shows a street, you self-grade "I know it" / "Still learning."
- **Multiple choice** — one real street plus three generated decoys (similar-sounding fakes built from real suffixes/numbers in your list) — trains your eye to catch the difference between a real street and something that just sounds plausible.
- **Type it** — the street name is masked to its first letters; you type the full name.

Progress in both modes is saved in your browser via `localStorage`, so it persists between visits on the same device/browser. Each mode has its own "Reset progress" button.

## Editing the street list
The list lives in a single array near the top of the `<script>` block in `index.html`:

```js
const STREETS = [
  "Skylark Ln", "CR 118", ...
];
```

Add, remove, or fix entries there — everything else (decoys, masking, stats) adapts automatically.
