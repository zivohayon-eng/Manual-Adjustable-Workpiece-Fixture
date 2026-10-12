# Project 2 — Bill of Materials

## Document Scope

This bill of materials defines the current component structure of the manually operated adjustable workpiece fixture. It distinguishes manufactured parts, the wheel-and-handle subassembly, and the final assembly. Quantities are stated per one completed `AssemReady`.

## Assembly Structure

- `AssemReady` is the final assembly and is not an individual manufactured part.
- `AssemWheel_Handle_Good` is one subassembly within `AssemReady`.
- `Wheel` and `Handle` are individual parts contained within `AssemWheel_Handle_Good`; their quantities are not additional to the subassembly quantity.
- All remaining listed parts are installed directly in `AssemReady`.

## Bill of Materials

| Item No. | Part / Assembly Name | Type | Quantity | Description | Main Specification | Manufacturing / Notes |
|---:|---|---|---:|---|---|---|
| A0 | `AssemReady` | Final assembly | 1 | Complete manually operated adjustable workpiece fixture. | Final assembly definition; overall performance requirements per project requirements document. | Not manufactured as a single part. Assembly process and final inspection plan: TBD. |
| 1 | `Base_Plate` | Individual part | 1 | Main structural base supporting and locating the fixture components. | 200 × 80 × 10 mm. | Material, tolerances, surface finish, and manufacturing method: TBD. |
| 2 | `Guide_Rod` | Individual part | 2 | Parallel rods that guide the linear motion of `MovingPart` and limit jaw rotation. | Ø10 mm; nominal length 150 mm each. | Material, fit, straightness, surface finish, and manufacturing method: TBD. |
| 3 | `Fixed_Jaw_New` | Individual part | 1 | Stationary-side jaw component used in the current assembly design. | Dimensions and interface details: TBD. | Confirm final function relative to `Fixed Jaw`; material and manufacturing method: TBD. |
| 4 | `Fixed Jaw` | Individual part | 1 | Additional stationary-side jaw component included in the current assembly structure. | Dimensions and interface details: TBD. | Confirm final function relative to `Fixed_Jaw_New`; material and manufacturing method: TBD. |
| 5 | `MovingPart` | Individual part | 1 | Translating jaw component that moves along the guide rods and engages the lead screw. | M10 × 1.5 internal threaded hole; 1.5 mm nominal travel per lead-screw revolution. | Guide-rod fits, remaining dimensions, material, tolerances, and manufacturing method: TBD. |
| 6 | `NonMovingPart` | Individual part | 1 | Stationary support for the lead-screw mechanism. | Lead-screw support interface and remaining dimensions: TBD. | Must support screw rotation while preventing unintended axial travel; material, bearing arrangement, and manufacturing method: TBD. |
| 7 | `Lead Screw` | Individual part | 1 | Manually driven screw that converts rotary input into linear motion of `MovingPart`. | M10 × 1.5 external thread; nominal overall length 140 mm; pitch 1.5 mm. | Axial retention details, material, tolerances, surface finish, and manufacturing method: TBD. |
| 8 | `AssemWheel_Handle_Good` | Subassembly | 1 | Manual input subassembly mounted to the lead screw. | Contains one `Wheel` and one `Handle`. | Assembly connection, retention method, and inspection requirements: TBD. |
| 8.1 | `Wheel` | Individual part — child of Item 8 | 1 | Handwheel used to apply manual torque to the lead screw. | Nominal outside diameter Ø60 mm; nominal thickness 8 mm. | Connection to `Lead Screw`, material, tolerances, finish, and manufacturing method: TBD. |
| 8.2 | `Handle` | Individual part — child of Item 8 | 1 | Rotating grip used to turn the wheel manually. | M5 × 0.8 external thread; thread length 9 mm. | Grip geometry, material, fit, retention, finish, and manufacturing method: TBD. |

## BOM Control Notes

- Component names shall match the SolidWorks files exactly.
- `Lead Screw` and `MovingPart` are separate components connected through the M10 × 1.5 threaded interface.
- One full revolution of `Lead Screw` produces 1.5 mm nominal linear travel of `MovingPart`.
- Materials, finishes, tolerances, standard hardware, purchased components, and manufacturing processes shall remain `TBD` until formally selected.
- Any future fasteners, washers, bearings, retaining rings, bushings, or other hardware shall be added as separate BOM items after their specifications and quantities are defined.
- BOM quantities and component hierarchy shall be verified against the released `AssemReady` SolidWorks assembly before drawing release or manufacturing.

## Current BOM Status

The component structure and listed quantities are defined for the current design state. Material selection, detailed manufacturing planning, hardware selection, tolerances, and release status remain `TBD`.
