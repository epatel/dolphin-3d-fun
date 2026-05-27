# Coordinate System

Three.js world coordinates and dolphin model axis conventions, verified empirically from static renders.

## World axes (Three.js default)

- **+X** = screen right
- **+Y** = screen up
- **+Z** = toward camera (out of screen)
- Camera at `(0, 0, 10)` looking along `-Z`

## Model axes (Atlantis dolphin)

- **+Z** = nose (forward)
- **+Y** = dorsal fin (up)
- **+X** = right flank

## Initial orientation: `R_Y(+PI/2)`

Verified from `debug-static.html` image 2:

- Nose (+Z) → +X world (screen right)
- Dorsal (+Y) → +Y world (screen up)
- Right flank (+X) → -Z world (away from camera, viewer sees left profile)

## Rotation conventions (right-hand rule, local space via `quaternion.multiply`)

| Rotation | Effect | Use case |
|----------|--------|----------|
| `R_Y(+angle)` | Nose turns toward camera (+Z) | Yaw right (fish POV) |
| `R_Y(-angle)` | Nose turns away from camera (-Z) | Yaw left |
| `R_X(-angle)` | Nose pitches **up** (+Y) | Pitch toward target above |
| `R_X(+angle)` | Nose pitches **down** (-Y) | Pitch toward target below |
| `R_Z(-angle)` | Dorsal tilts right | Bank into right turn |

These signs were verified by rendering static test orientations and inspecting the actual images (see `archive/debug-static.html`).

## Frustum mapping

```
halfH = tan(fov/2) * cameraZ = tan(25°) * 10 ≈ 4.66
halfW = halfH * aspect ≈ 8.29  (at 16:9)
worldX = mouseNDC.x * halfW
worldY = mouseNDC.y * halfH
```
