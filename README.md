# WCESD#3 Street Recognition Trainer

A single-page study tool for memorizing the 120 streets in your response area, styled like a CAD dispatch terminal. No build step, no dependencies to install — it's one HTML file.

## Try it locally
Just double-click `index.html` — it opens in your browser.

## Put it on GitHub Pages
1. Create a new repo on GitHub (e.g. `street-trainer`).
2. Add `index.html` to the repo (drag-and-drop upload works fine, or `git add` / `git commit` / `git push` if you're using the command line).
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment," set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`. Save.
5. GitHub gives you a URL like `https://yourusername.github.io/street-trainer/` within a minute or two — that's your live quiz page.

## How it works
- **Mixed** — cycles randomly between all three quiz types (this is the default).
- **Flashcards** — shows a street, you self-grade "I know it" / "Still learning."
- **Multiple choice** — one real street plus three generated decoys (similar-sounding fakes built from real suffixes/numbers in your list) — good for training your eye to catch the difference between a real street and something that just sounds plausible.
- **Type it** — the street name is masked to its first letters; you type the full name.

Progress (mastered streets, streak, accuracy) is saved in your browser via `localStorage`, so it persists between visits on the same device/browser. Use "Reset progress" to start over.

## Editing the street list
The list lives in a single array near the top of the `<script>` block in `index.html`:

```js
const STREETS = [
  "Skylark Ln", "CR 118", ...
];
```

Add, remove, or fix entries there — everything else (decoys, masking, stats) adapts automatically.
