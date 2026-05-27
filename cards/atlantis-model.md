# Atlantis Dolphin Model

The 3D dolphin geometry extracted from Silicon Graphics' 1993 OpenGL GLUT Atlantis demo (`dolphin.c`).

## Extraction

The original C file defines vertices as `static float P###[3]` arrays and normals as `N###[3]`, with geometry drawn via `glBegin(GL_POLYGON)` / `glVertex3fv` / `glEnd` blocks in functions `Dolphin001()` through `Dolphin016()`.

A Node.js script parsed the C source, fan-triangulated the polygons, and normalized coordinates to a ~2-unit bounding box centered at the origin.

## Geometry stats

- 211 triangles, 633 vertices (126 unique positions)
- Coordinate range: X ±0.38, Y ±0.24, Z ±1.0

## Double-sided fins

The pectoral fins (Dolphin010/011) and dorsal fin (Dolphin006) are drawn as two sets of triangles with reversed winding — front and back faces as separate geometry. Smooth normal computation must only average normals from compatible neighbors (face normal dot product > 0) to prevent cancellation that causes black patches.

## Swimming animation

From `DrawDolphin()`: vertices are grouped into 8 segments plus a "chomp" group. Each segment's Y coordinates are displaced by `amplitude * sin(htail + phaseOffset)`:

| Segment | Vertices | Amplitude | Phase | Body region |
|---------|----------|-----------|-------|-------------|
| seg0 | P044-P051 | 1.0× | 0° | Mid-body |
| seg1 | P036-P043 | 2.0× | 4° | Rear-mid |
| seg2 | P028-P035 | 3.0× | 6° | Rear |
| seg3 | P091-P095 | 1.0× | 0° | Dorsal fin |
| seg4 | P020-P027 | 4.0× | 10° | Front-rear |
| seg5 | P012-P019 | 4.5× | 15° | Near-tail |
| seg6 | P009-P010 | 5.0× | 20° | Tail base |
| seg7 | P001,P011,P068-P074 | 6.0× | 30° | Tail tip |
| chomp | P097-P121 | fixed | — | Mouth |

Amplitude increases toward the tail, with progressive phase offset creating a traveling wave.

## Material

`MeshPhysicalMaterial` with vertex colors (countershading: darker blue-gray top, lighter belly), clearcoat for a wet/glossy look, and `side: DoubleSide` for the fin geometry.
