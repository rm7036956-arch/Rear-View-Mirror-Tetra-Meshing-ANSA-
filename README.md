# Rear-View Mirror: Tetrahedral Volume Meshing in ANSA

Surface and volume meshing of a car rear-view mirror assembly (housing, stem and ball-joint mount) using **BETA CAE ANSA v25.0.0**, with unstructured **Tetra Rapid** meshing for the solid volume.

## Objective
- Check and clean geometry errors in the imported IGES model
- Create a 2D tria mesh that meets the target quality criteria
- Create volumes and fill them with a tetrahedral mesh
- Keep surface quality good after volume meshing (no kinks or dips)

## Quality criteria
| Criterion | Value |
|---|---|
| Target / average length | 1 mm |
| Minimum length | 0.5 mm |
| Maximum length | 2 mm |
| Tet collapse (3D) | 0.2 |

## Workflow
1. **Import** the IGES geometry into ANSA
2. **Geometry cleanup**: topology, free edges, small faces, merging and simplifying macro faces
3. **Perimeter/length setup**: mesh parameters set to the criteria above
4. **2D mesh**: tria elements via Free / Spot Mesh macros; fixed length violations
5. **Volume definition**: closed shells defined as volumes
6. **3D mesh**: Tetra Rapid on all volumes
7. **Quality check**: tet collapse on 3D, min/max length on 2D; remeshed local failures
8. **Save** as `.ansa`

## Results
| Metric | Value |
|---|---|
| Shell (tria) elements | 72,512 |
| Solid (tetra) elements | 388,468 |
| Element type | TRIA3 / TETRA4 |
| Solver deck | NASTRAN |

## Challenges and fixes
- Small grooves on the housing edge needed local length control so the mesh followed the profile
- Failed elements near corners (min/max length) were fixed by remeshing macros
- Unmeshed macros and unchecked entities were cleaned before volume meshing
- Surface kinks after volume meshing were avoided by good 2D quality first

## Tools
ANSA v25.0.0 · IGES · Tetra Rapid · NASTRAN

## Repository structure
├── images/
├── report/Rearview_Mirror_Meshing_Report.pdf
├── ansa/Rearview_mirror_meshed.ansa
└── README.md

> Geometry files are provided by the course and not redistributed.
