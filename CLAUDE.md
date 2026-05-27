# Dolphin 3D Fun

A transparent Three.js overlay that renders an animated 3D dolphin (SGI Atlantis, 1993) following the mouse cursor on a demo landing page. Vanilla ES modules, Three.js from CDN, no build step.

## Serving

```bash
python3 -m http.server 8787
```

## Cards

- [architecture](cards/architecture.md) — module graph, rendering pipeline, per-frame data flow
- [coordinate-system](cards/coordinate-system.md) — world/model axes, rotation sign conventions (empirically verified), frustum mapping
- [vehicle-physics](cards/vehicle-physics.md) — quaternion steering, anisotropic drag, leveling spring, tuning parameters
- [atlantis-model](cards/atlantis-model.md) — SGI dolphin geometry extraction, double-sided fin normals, segment-based swimming animation
