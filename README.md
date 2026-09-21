# Claude-Vision

A 3D, animated model of a beating human heart, built with [Three.js](https://threejs.org/).

![status](https://img.shields.io/badge/type-static%20web%20demo-blue)

## What it shows

- A single, continuous muscle wall (epicardium) rather than four separate
  coloured balls: the chambers are modelled as overlapping "lobes" and
  blended into one organic shape with a metaball-style smooth-minimum SDF,
  triangulated with marching cubes so the surface has no seams, creases, or
  hidden holes at any viewing angle.
- Surface detail that reads as a real organ: a glossy, faintly mottled wet
  material (clearcoat + sheen), a darkened coronary sulcus where the atria
  meet the ventricles, epicardial fat deposits, and coronary vessels (LAD,
  great cardiac vein, RCA) running across the surface.
- The great vessels (superior/inferior vena cava, pulmonary artery, pulmonary
  veins, aorta), laid out in standard anatomical-illustration orientation (as
  if facing a patient), meeting the muscle wall flush rather than floating or
  poking through it.
- A real cardiac-cycle animation: atrial systole &rarr; ventricular systole &rarr;
  diastole. Each region of the shell contracts and relaxes locally (a
  per-vertex blend of "atria vs. ventricle"), not just a uniform full-model
  pulse.
- Directional blood flow: particles travel deoxygenated blood (blue) from the
  vena cavae through the right heart to the pulmonary artery, and oxygenated
  blood (red) from the pulmonary veins through the left heart to the aorta,
  speeding up during ejection.
- A "cutaway" toggle that makes the outer wall translucent, revealing the
  four internal chambers colour-coded by oxygenation.
- Adjustable heart rate (40&ndash;180 bpm), play/pause, auto-rotate, and toggleable
  chamber/vessel labels and blood flow.

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
- `vendor/three/` &mdash; vendored Three.js build plus the `OrbitControls`,
  `RoomEnvironment`, `BufferGeometryUtils` (vertex welding), and
  `MarchingCubes` (lookup tables only) addons, all MIT licensed.
