# Dolphin 3D Fun

A 3D dolphin that follows your mouse cursor, built as a transparent overlay on top of a demo landing page.

Click the 🐬 button in the top-left corner to release the dolphin.

## Features

- **Classic SGI Atlantis dolphin** — the 1993 Silicon Graphics OpenGL demo model, extracted and converted to Three.js
- **Smooth shading** — face-aware normal averaging that handles the model's double-sided fin geometry
- **Vehicle physics** — quaternion-based orientation with yaw/pitch steering, anisotropic drag, and bicycle lean into turns
- **Swimming animation** — authentic segment-based body undulation from the original `DrawDolphin()` function
- **Behavior states** — follows the mouse, circles when idle, then explores the page
- **Bubble particles** — rise from the blowhole with soft fade and grow effect

## Files

| File | Description |
|------|-------------|
| `index.html` | Landing page with dolphin overlay |
| `vehicle.js` | Vehicle physics module (orientation, steering, thrust, drag) |
| `dolphin.js` | Dolphin model construction, smooth normals, swimming animation |
| `dolphin-model.js` | Raw vertex/normal/segment data extracted from the SGI Atlantis `dolphin.c` |

## Usage

Serve the directory with any HTTP server:

```bash
python3 -m http.server 8787
open http://localhost:8787
```

Requires a modern browser with ES module and `importmap` support.

## Credits

- Dolphin model: Silicon Graphics, Inc. (1993) — from the [GLUT Atlantis demo](https://www.opengl.org/archives/resources/code/samples/glut_examples/examples/examples.html)
- Rendering: [Three.js](https://threejs.org/)
