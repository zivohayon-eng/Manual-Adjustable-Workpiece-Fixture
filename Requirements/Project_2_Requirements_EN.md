# Project 2 — Adjustable Workpiece Fixture Requirements

## Project Objective

Design and document a manually operated adjustable workpiece fixture (mini vise) that clamps a workpiece between a fixed jaw and a translating jaw. The design shall demonstrate sound mechanical design, Design for Manufacturing and Assembly (DFM/DFA), controlled screw-driven motion, and portfolio-quality CAD documentation.

## Functional Requirements

- The fixture shall clamp and release a workpiece through manual rotation of the `Wheel` and `Handle`.
- The `Lead Screw` and `MovingPart` shall remain separate components and interact through an M10 × 1.5 threaded connection.
- Rotation of the `Lead Screw` shall produce linear motion of the `MovingPart`.
- The `MovingPart` shall travel along two `Guide_Rod` components without unintended rotation.
- `Fixed_Jaw_New` and `Fixed Jaw` shall provide the stationary clamping-side components defined by the final assembly design.
- `NonMovingPart` shall support the lead-screw mechanism while remaining stationary in `AssemReady`.
- The `Wheel` and `Handle` shall provide a practical manual input to the `Lead Screw`.
- The fixture shall mount through the `Base_Plate` while remaining stable during intended operation.

## Main Design Parameters

| Item | Requirement |
|---|---|
| `Base_Plate` | 200 × 80 × 10 mm |
| `Guide_Rod` | Two rods, Ø10 mm, nominal length 150 mm each |
| `Lead Screw` | M10 × 1.5 external thread; nominal overall length 140 mm |
| Lead-screw pitch | 1.5 mm |
| `MovingPart` | M10 × 1.5 internal threaded hole |
| Linear travel ratio | 1.5 mm of `MovingPart` travel per full `Lead Screw` revolution |
| `Wheel` | Nominal outside diameter Ø60 mm; nominal thickness 8 mm |
| `Handle` | M5 × 0.8 external thread; thread length 9 mm |

Dimensions not listed above remain TBD and shall be defined through further design development and verification.

## Mechanical Requirements

- The M10 × 1.5 external thread on the `Lead Screw` shall mate with the M10 × 1.5 internal thread in the `MovingPart`.
- The two `Guide_Rod` components shall be parallel and aligned with the intended travel direction of the `MovingPart`.
- The guide-rod interfaces shall permit smooth sliding motion while limiting transverse movement and jaw rotation.
- The `Lead Screw` shall rotate about its axis without unintended axial translation relative to `NonMovingPart`.
- The `Wheel` shall transmit manual torque to the `Lead Screw` without relative rotation at their connection.
- The `Handle` connection to the `Wheel` shall use its specified M5 × 0.8 external thread over a 9 mm thread length.
- Component materials, manufacturing tolerances, fits, surface finishes, allowable loads, and target clamping force are TBD.

## Assembly and Motion Requirements

- `AssemWheel_Handle_Good` shall contain the `Wheel` and `Handle` and preserve their intended relative motion and connection.
- `AssemReady` shall contain and correctly position all required fixture components: `Base_Plate`, two `Guide_Rod` instances, `Fixed_Jaw_New`, `Fixed Jaw`, `MovingPart`, `NonMovingPart`, `Lead Screw`, and `AssemWheel_Handle_Good`.
- The `Base_Plate`, stationary jaw components, guide rods, and `NonMovingPart` shall remain fixed relative to one another during operation.
- The `Wheel` and `Lead Screw` shall rotate together while remaining fixed in the axial direction.
- The `MovingPart` shall translate 1.5 mm for each complete revolution of the `Lead Screw`.
- The motion direction shall reverse when the direction of wheel rotation is reversed.
- Assembly mates shall allow the required rotation and translation without over-defining the assembly.
- The motion range shall be limited to prevent component disengagement and unintended interference; final travel limits are TBD.

## CAD and Drawing Requirements

- SolidWorks part, subassembly, and assembly files shall use the established component names exactly as listed in this document.
- Each manufactured component shall be modeled as a separate part with a clear, editable feature history.
- Repeated components, including `Guide_Rod`, shall use separate assembly instances of the same part file.
- Thread definitions shall match the specified M10 × 1.5 and M5 × 0.8 interfaces.
- `AssemReady` shall rebuild without mate errors and shall demonstrate the intended screw-driven motion.
- Production drawings shall include the dimensions, tolerances, materials, finishes, thread callouts, and manufacturing notes required to make and inspect each component. Values not yet selected shall be marked TBD.
- Assembly documentation shall include an exploded view, a bill of materials, item balloons, and relevant assembly notes.
- Public English documentation shall remain in the existing project folders. Hebrew study documentation shall remain under `Private_Hebrew/`.

## Simulation / Analysis Requirements

- Perform a basic structural assessment of the fixture under an applied clamping load of **TBD**.
- Evaluate stress and displacement in the primary load-bearing components, including the jaws, `Base_Plate`, `Guide_Rod` components, `Lead Screw`, and its supporting interfaces.
- Define materials, restraints, contacts, mesh settings, convergence checks, and load application before accepting simulation results; unresolved values shall be marked TBD.
- Check the `Lead Screw` and threaded interface for axial loading and assess the guide rods for bending and alignment effects.
- Compare simulation results with material limits and an appropriate factor of safety once the materials and design load are defined.
- Record assumptions, boundary conditions, limitations, and results in the project documentation.

## Acceptance Criteria

The design is accepted when all of the following conditions are met:

- All specified components are present and correctly identified in `AssemReady`.
- The assembly rebuilds without unresolved references or mate errors.
- Manual rotation of the `Wheel` rotates the `Lead Screw` without axial movement of the wheel-and-screw assembly.
- The `MovingPart` travels smoothly along both guide rods and moves 1.5 mm per full lead-screw revolution.
- Reversing wheel rotation reverses the direction of jaw travel.
- The moving and stationary components do not exhibit unintended interference throughout the defined travel range.
- All specified dimensions and thread interfaces match the requirements in this document.
- Manufacturing drawings, BOM, assembly documentation, and simulation records are complete; any design values still under development are explicitly marked TBD.
