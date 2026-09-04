# Chroma Labs — landing

Single-screen landing for Chroma Labs: a procedural living moss world rendered in Three.js, with the title and one line of copy floating above it.

## Run locally

Serve this folder over HTTP and open the root:

```bash
python3 -m http.server 4181 --bind 127.0.0.1 --directory .
```

Then visit http://127.0.0.1:4181/. There is no build step.

## Files

- `index.html` — the page: title, copy, links to the two products (Vora at https://chrom.ar/ for now, later https://vora.chrom.ar/; Yoku at https://yoku.chrom.ar/), scene credit, entrance and pointer parallax. Type is Bricolage Grotesque from Google Fonts.
- `scene/living-green.html` — the scene-only "Living Green" document (Sylva Living World, ThreeUI Community catalog, MIT), loaded in a full-viewport iframe. It reports the pointer position to the parent page so the copy can drift against it.
- `scene/three.min.js` — Three.js r149 runtime used by the scene.
- `LICENSES.md` — third-party notices.

## Deploy

The live site is the separate repository `base60s/chroma-labs`, served by GitHub Pages from its `main` branch root at
https://base60s.github.io/chroma-labs/. Its `main` is just this folder, published as its own commit. To redeploy after
committing changes here:

```bash
# from the yokulanding checkout that holds the chroma-labs folder
TREE=$(git rev-parse HEAD:chroma-labs)
COMMIT=$(git commit-tree "$TREE" -m "Deploy Chroma Labs landing")
git push https://github.com/base60s/chroma-labs.git "$COMMIT:refs/heads/main" --force
```

`.nojekyll` keeps Pages from running Jekyll over the folder.

## Notes

- The scene needs WebGL2. Without it the page keeps the fog-coloured ground and the copy still shows.
- With `prefers-reduced-motion`, the scene renders a single still frame, the copy appears without animation and there is no parallax.
- The moss is grown procedurally on load (about 130,000 instanced blades on desktop), so it can take a few seconds to appear on slower machines. The copy appears as soon as the scene document has loaded.
- Pointer events pass through the copy to the scene, so the moss keeps parting around the cursor even over the title. Only the credit link is clickable.
