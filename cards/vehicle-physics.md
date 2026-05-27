# Vehicle Physics

Quaternion-based 3D vehicle simulation in `vehicle.js`. No Euler angles.

## Orientation model

A persistent quaternion evolved incrementally each frame. Never reconstructed from scratch — avoids gimbal lock and singularities.

### Steering (local space)

Target direction is projected into the vehicle's local frame:
- `localX = toTarget · right` — lateral offset
- `localY = toTarget · up` — vertical offset
- `localZ = toTarget · forward` — distance ahead

Yaw and pitch are applied as local rotations via `quaternion.multiply()`:
- **Yaw**: `R_Y(+angle)` where angle ∝ `atan2(localX, localZ)` — turns nose toward target
- **Pitch**: `R_X(-angle)` where angle ∝ `atan2(localY, fwdDist)` — tilts nose toward target

### Leveling spring

Rolls the vehicle's local up toward world up, rotating only around the forward axis (no heading interference). The target up is offset by the yaw error to create a bicycle lean into turns.

### Thrust and drag

- Forward thrust proportional to distance to target (fast when far, slow when close)
- Anisotropic drag: low forward (1.5), high sideways (8.0), medium vertical (4.0)
- The dolphin moves mostly forward — high side drag prevents lateral sliding

## Tuning parameters

All configurable via constructor options:

| Param | Default | Effect |
|-------|---------|--------|
| `thrust` | 8.0 | Max forward force |
| `minThrust` | 0.1 | Idle forward force |
| `fwdDrag` | 2.0 | Forward deceleration |
| `sideDrag` | 8.0 | Sideways resistance |
| `yawRate` | 3.0 | Turn responsiveness |
| `pitchRate` | 2.0 | Pitch responsiveness |
| `levelSpring` | 4.0 | Upright correction strength |
| `bankFactor` | 0.4 | Lean into turns amount |
