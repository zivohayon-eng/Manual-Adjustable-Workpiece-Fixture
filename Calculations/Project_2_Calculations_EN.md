# Project 2 - Preliminary Engineering Calculations

## Document Purpose

This document records the preliminary calculations used to evaluate the screw-driven motion and basic structural behaviour of the manually operated adjustable workpiece fixture. The results support early design decisions and provide reference values for later SolidWorks Simulation studies.

All calculations represent the current design state. They do not replace final verification, detailed thread analysis, manufacturing tolerances, physical testing, or a validated finite element model.

## Current Design Data

| Parameter | Symbol | Value |
|---|---:|---:|
| `Lead Screw` thread | - | M10 × 1.5 |
| Lead-screw pitch / lead | `p` | 1.5 mm/rev |
| `Wheel` outside diameter | `D` | 60 mm |
| Handwheel radius | `r` | 30 mm = 0.03 m |
| Assumed hand force | `F_hand` | 50 N |
| Input torque | `T_in` | 1.5 N·m |
| Estimated clamping force | `F_clamp` | 1885 N ≈ 1.9 kN |
| `Lead Screw` tensile stress area | `A_t` | 58 mm² |
| `Lead Screw` axial stress | `σ_screw` | 32.5 MPa |
| `Guide_Rod` diameter | `d` | 10 mm |
| `Guide_Rod` nominal length | `L` | 150 mm |
| Assumed load per `Guide_Rod` | `P` | 94.25 N |
| `Guide_Rod` bending stress | `σ_rod` | 36 MPa |
| `Guide_Rod` maximum deflection | `δ_max` | 0.068 mm |
| Selected screw and guide-rod material | - | AISI 1045 Steel |
| Assumed yield strength | `S_y` | 310 MPa |

## Design Assumptions

> **Preliminary engineering assumptions - not measurements from the physical model**
>
> - Thread efficiency: **30%**
> - Lateral load on the guide rods: **10% of the estimated clamping force**
> - AISI 1045 yield strength: **310 MPa**
> - Hand force: **50 N**

These assumptions are used only for preliminary calculations. They will be compared against SolidWorks Simulation results and may be refined when better material data, supplier information, manufacturing data, or experimental measurements become available.

For the guide-rod calculation, each rod is represented as a simply supported beam with a transverse point load at midspan. A steel elastic modulus of `E = 200 GPa = 200,000 N/mm²` is used as a preliminary calculation value and shall be verified against the selected material specification.

## 1. Lead Screw Travel

**Purpose of the calculation**

Determine how far `MovingPart` travels for a specified number of `Lead Screw` revolutions.

**Given data**

- Lead-screw pitch / lead: `p = 1.5 mm/rev`
- Evaluation case: `N = 1 rev`

**Formula**

`x = p × N`

**Substitution**

`x = (1.5 mm/rev) × (1 rev)`

**Result**

`x = 1.5 mm`

The general motion relationship is `x = 1.5N mm`, where `N` is the number of full revolutions.

**Why the result is important**

The result defines the motion ratio of the mechanism and is required for assembly motion, jaw-position control, and verification of the Screw Mate in SolidWorks.

**Components affected**

`Lead Screw`, `MovingPart`, `Wheel`, `Handle`, `AssemWheel_Handle_Good`, and `AssemReady`.

## 2. Number of Revolutions

**Purpose of the calculation**

Determine the number of handwheel revolutions required to produce a specified linear movement of `MovingPart`.

**Given data**

- Lead-screw pitch / lead: `p = 1.5 mm/rev`
- Required jaw travel: `x_target = TBD mm`

**Formula**

`N = x_target / p`

**Substitution**

`N = x_target / (1.5 mm/rev)`

For a unit travel comparison:

`N / x_target = 1 / 1.5 = 0.667 rev/mm`

**Result**

`N = 0.667 × x_target` revolutions when `x_target` is entered in millimetres. The final total number of revolutions remains `TBD` until the usable jaw travel is defined. As a consistency check, 1.5 mm of travel requires one full revolution.

**Why the result is important**

This value indicates how much manual rotation is needed to open or close the fixture and helps evaluate operating speed and usability.

**Components affected**

`Lead Screw`, `MovingPart`, `Wheel`, `Handle`, `AssemWheel_Handle_Good`, and `AssemReady`.

## 3. Input Torque from the Handwheel

**Purpose of the calculation**

Estimate the torque applied to the `Lead Screw` when the assumed hand force acts at the outside radius of the `Wheel`.

**Given data**

- Assumed hand force: `F_hand = 50 N`
- Handwheel radius: `r = 30 mm = 0.03 m`

**Formula**

`T_in = F_hand × r`

**Substitution**

`T_in = 50 N × 0.03 m`

**Result**

`T_in = 1.5 N·m`

**Why the result is important**

Input torque is the mechanical input used to estimate clamping force and to assess the torque-carrying connections between the handle, wheel, and lead screw.

**Components affected**

`Handle`, `Wheel`, `Lead Screw`, and `AssemWheel_Handle_Good`.

## 4. Clamping Force from the Lead Screw

**Purpose of the calculation**

Estimate the axial clamping force produced by the lead screw from the available handwheel torque.

**Given data**

- Input torque: `T_in = 1.5 N·m`
- Assumed thread efficiency: `η = 0.30`
- Screw lead: `l = 1.5 mm/rev = 0.0015 m/rev`

**Formula**

Using a simplified power-screw energy relationship:

`F_clamp = (2π × η × T_in) / l`

**Substitution**

`F_clamp = (2π × 0.30 × 1.5 N·m) / 0.0015 m`

**Result**

`F_clamp = 1885 N ≈ 1.9 kN`

**Why the result is important**

The estimated force establishes the preliminary design load for the jaws, lead screw, guide rods, base plate, and support interfaces. The actual force may differ because thread geometry, collar friction, lubrication, alignment, deformation, and manufacturing tolerances are not yet fully defined.

**Components affected**

`Lead Screw`, `MovingPart`, `NonMovingPart`, `Guide_Rod`, `Fixed_Jaw_New`, `Fixed Jaw`, and `Base_Plate`.

## 5. Lead Screw Stress

**Purpose of the calculation**

Estimate the direct axial stress in the threaded section of the `Lead Screw` under the calculated clamping force.

**Given data**

- Axial force: `F_clamp = 1885 N`
- Tensile stress area: `A_t = 58 mm²`

**Formula**

`σ_screw = F_clamp / A_t`

**Substitution**

`σ_screw = 1885 N / 58 mm²`

**Result**

`σ_screw = 32.5 N/mm² = 32.5 MPa`

**Why the result is important**

The axial stress is used to assess the basic static strength of the screw and calculate its preliminary factor of safety. This simplified result does not include torsional stress, thread-root stress concentration, buckling, fatigue, or local bearing stress.

**Components affected**

`Lead Screw`, its threaded connection with `MovingPart`, and its support interface with `NonMovingPart`.

## 6. Guide Rod Bending and Deflection

**Purpose of the calculation**

Estimate bending stress and maximum deflection in each `Guide_Rod` under the assumed lateral portion of the clamping load.

**Given data**

- Estimated clamping force: `F_clamp = 1885 N`
- Assumed total lateral guide-rod load: `0.10 × F_clamp = 188.5 N`
- Two guide rods share the lateral load equally
- Load per rod: `P = 188.5 / 2 = 94.25 N`
- Rod diameter: `d = 10 mm`
- Nominal span: `L = 150 mm`
- Elastic modulus: `E = 200,000 N/mm²`
- Beam model: simply supported with a point load at midspan

**Formula**

Second moment of area:

`I = πd⁴ / 64`

Maximum bending moment:

`M_max = PL / 4`

Maximum bending stress:

`σ_rod = M_max(d/2) / I = 8PL / (πd³)`

Maximum midspan deflection:

`δ_max = PL³ / (48EI)`

**Substitution**

`I = π(10 mm)⁴ / 64 = 490.9 mm⁴`

`M_max = (94.25 N × 150 mm) / 4 = 3534.4 N·mm`

`σ_rod = [3534.4 N·mm × 5 mm] / 490.9 mm⁴ = 36.0 MPa`

`δ_max = [94.25 N × (150 mm)³] / [48 × 200,000 N/mm² × 490.9 mm⁴]`

**Result**

- Maximum bending stress per guide rod: `σ_rod ≈ 36 MPa`
- Maximum guide-rod deflection: `δ_max ≈ 0.068 mm`

**Why the result is important**

Bending stress checks preliminary rod strength, while deflection indicates whether rod flexibility could affect jaw alignment, sliding quality, or clamping accuracy. The result depends strongly on the assumed support and load arrangement and shall be compared with assembly-level simulation.

**Components affected**

Both `Guide_Rod` instances, `MovingPart`, the guide-rod mounting interfaces, `Fixed_Jaw_New`, `Fixed Jaw`, and `Base_Plate`.

## 7. Factor of Safety

**Purpose of the calculation**

Compare the calculated stresses with the assumed yield strength of AISI 1045 Steel and identify the lower preliminary static factor of safety.

**Given data**

- Assumed yield strength: `S_y = 310 MPa`
- Lead-screw axial stress: `σ_screw = 32.5 MPa`
- Guide-rod bending stress: `σ_rod = 36 MPa`

**Formula**

`FoS = S_y / σ`

**Substitution**

Lead screw:

`FoS_screw = 310 MPa / 32.5 MPa = 9.54`

Guide rod:

`FoS_rod = 310 MPa / 36 MPa = 8.61`

**Result**

- `Lead Screw` factor of safety: `FoS_screw ≈ 9.5`
- `Guide_Rod` factor of safety: `FoS_rod ≈ 8.6`
- Governing preliminary factor of safety: `8.6`, based on guide-rod bending

**Why the result is important**

The factors of safety provide an initial comparison between calculated static stresses and assumed material yield strength. They are not final approval values because combined loading, threads, stress concentrations, buckling, fatigue, contacts, tolerances, and real boundary conditions have not yet been fully evaluated.

**Components affected**

`Lead Screw`, both `Guide_Rod` instances, `MovingPart`, `NonMovingPart`, the jaw components, and `Base_Plate`.

## Calculation Summary

| Calculation | Preliminary result | Status / next verification |
|---|---:|---|
| Lead-screw travel | 1.5 mm/rev | Verify assembly motion in SolidWorks. |
| Revolutions required | 0.667 rev/mm × required travel | Total revolutions remain TBD until usable jaw travel is defined. |
| Handwheel input torque | 1.5 N·m | Based on assumed 50 N hand force. |
| Estimated clamping force | 1885 N ≈ 1.9 kN | Compare with SolidWorks Simulation and later physical testing. |
| Lead-screw axial stress | 32.5 MPa | Add combined and thread-specific checks in detailed design. |
| Guide-rod bending stress | 36 MPa | Verify load distribution and supports in simulation. |
| Guide-rod maximum deflection | 0.068 mm | Check effect on jaw alignment and sliding. |
| Lead-screw factor of safety | 9.5 | Preliminary static value. |
| Guide-rod factor of safety | 8.6 | Preliminary governing static value. |

## Limitations and Next Steps

- Confirm the usable jaw travel and calculate the final number of operating revolutions.
- Verify the selected AISI 1045 Steel grade, condition, elastic modulus, and certified yield strength.
- Refine thread efficiency using the final thread geometry, lubrication, and collar or bearing friction.
- Evaluate combined axial and torsional stress in the lead screw, thread-root stresses, thread stripping, buckling, and fatigue where applicable.
- Verify guide-rod constraints, load distribution, contacts, and deflection using SolidWorks Simulation.
- Compare analytical results with simulation and physical measurements, then update the calculations and design assumptions.

