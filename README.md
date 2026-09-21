# Claude-Vision

A 3D, animated model of a beating human heart, built with [Three.js](https://threejs.org/).

![status](https://img.shields.io/badge/type-static%20web%20demo-blue)

## What it shows

- Four chambers (right/left atria, right/left ventricles) plus the great vessels
  (superior/inferior vena cava, pulmonary artery, pulmonary veins, aorta), laid
  out in standard anatomical-illustration orientation (as if facing a patient).
- A real cardiac-cycle animation: atrial systole &rarr; ventricular systole &rarr;
  diastole, with chambers visibly contracting and relaxing in sequence.
- Directional blood flow: particles travel deoxygenated blood (blue) from the
  vena cavae through the right heart to the pulmonary artery, and oxygenated
  blood (red) from the pulmonary veins through the left heart to the aorta,
  speeding up during ejection.
- Adjustable heart rate (40&ndash;180 bpm), play/pause, auto-rotate, toggleable
  chamber/vessel labels, toggleable blood flow, and a "cutaway" (semi-transparent)
  view.

This is a simplified, stylized teaching model, not a medically precise
reconstruction &mdash; chamber proportions and vessel paths are illustrative.

## Running it

Because the page loads Three.js as an ES module (vendored locally in
`vendor/three/`), it needs to be served over HTTP rather than opened directly
as a `file://` URL (browsers block local ES module imports under `file://`).

From the project root:

```bash
python3 -m http.server 8000
# then open http://localhost:8000/ in a browser
```

Any other static file server (`npx serve`, VS Code's Live Server, etc.) works
just as well. No build step or `npm install` is required &mdash; the only
dependency (Three.js) is already vendored in `vendor/three/`.

## Controls

- **Drag** to orbit, **scroll** to zoom, **right-drag** to pan.
- Use the panel (top-left) to change heart rate, pause/resume the beat, toggle
  auto-rotation, labels, blood flow, and cutaway mode.

## Files

- `index.html` &mdash; the entire app (markup, styles, and animation logic).
- `vendor/three/` &mdash; vendored Three.js build + `OrbitControls` addon (MIT licensed).
