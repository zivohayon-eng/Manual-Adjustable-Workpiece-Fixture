# Project 2 - Final ANSYS Assembly Analysis

## Objective

This document records the final corrected finite-element analysis of `AssemReady`, a manually operated adjustable workpiece fixture / mini vise. The `ANSYS 2026 R1 Student` Static Structural study evaluates the complete assembly under the estimated clamping load and compares the global response with previous hand calculations and SOLIDWORKS SimulationXpress studies.

The assembly-level model adds load paths, component interaction, sliding interfaces, support behavior, and system deformation that cannot be represented by isolated single-part studies. It remains a preliminary engineering model and is not final validation of the manufactured product.

## Analysis Definition

| Parameter | Final model definition |
|---|---|
| Final assembly | `AssemReady` |
| Solver | `ANSYS 2026 R1 Student` - Static Structural / Mechanical |
| Imported geometry | Parasolid |
| Analysis geometry | `AssemReady_ANSYS_Simplified.x_t` |
| Applied clamping force | 1885 N |
| Mesh | 65,406 nodes; 33,417 elements |

Main assembly components are `Base_Plate`, two `Guide_Rod` components, `Fixed_Jaw_New`, `Fixed Jaw`, `MovingPart`, `NonMovingPart`, `Lead Screw`, `Wheel`, and `Handle`. Some imported ANSYS body labels differ from the original SOLIDWORKS file names; for example, `Base` and `Fixed Jaw2` appear in the material assignments.

## Model Preparation

The original modeled M10x1.5 thread on `Lead Screw` caused meshing problems. The thread feature was therefore suppressed temporarily in SOLIDWORKS, and the assembly was re-exported as the simplified Parasolid file `AssemReady_ANSYS_Simplified.x_t`.

This change reduced geometric complexity and produced faster, more stable meshing. It also means that thread-root stress concentrations, local thread contact, and individual thread stresses are not represented. The study therefore evaluates global assembly behavior. The smooth screw is slightly less conservative for local screw stress than the real threaded geometry. The separate hand calculation based on the approximately 58 mm^2 M10 tensile-stress area is more representative of the actual threaded section.

## Materials

| Imported body / component | Assigned material |
|---|---|
| `Lead Screw` | AISI 1045 Steel, cold drawn |
| `Guide_Rod` (2x) | AISI 1045 Steel, cold drawn |
| `MovingPart` | AISI 1020 Steel, Cold Rolled |
| `NonMovingPart` | AISI 1020 Steel, Cold Rolled |
| `Fixed Jaw` | AISI 1020 Steel, Cold Rolled |
| `Fixed Jaw2` | AISI 1020 Steel, Cold Rolled |
| `Base` | AISI 1020 Steel, Cold Rolled |
| `Wheel` | AISI 1020 Steel, Cold Rolled |
| `Handle` | AISI 1020 Steel, Cold Rolled |

The ANSYS project material data use approximately `E = 205 GPa` and `nu = 0.29` for both steels. The selected AISI 1045 cold-drawn dataset uses a tensile yield strength of approximately `530 MPa` and ultimate tensile strength of approximately `625 MPa`. The selected AISI 1020 cold-rolled dataset uses a tensile yield strength of `350 MPa`. Material properties depend on grade condition and dataset; they must be confirmed against the intended stock and supplier specification before release for manufacture.

## Contacts

Automatic import initially generated Bonded contacts. Contacts that would incorrectly glue sliding components were changed manually.

| Interface | Final contact representation | Engineering purpose |
|---|---|---|
| `Guide_Rod` to `MovingPart` - rod 1 | Frictionless | Transfers normal contact while allowing axial sliding. |
| `Guide_Rod` to `MovingPart` - rod 2 | Frictionless | Transfers normal contact while allowing axial sliding. |
| `MovingPart` to `Base` | Frictionless | Allows sliding without artificial tangential locking. |
| `Lead Screw` to `MovingPart` | Bonded | Simplified representation of engaged M10x1.5 threads. |
| `Lead Screw` to `NonMovingPart` | Suppressed in final corrected model | Replaced by the final support representation. |

Bonding `Lead Screw` to `MovingPart` does not resolve thread contact or screw rotation. It is an idealized load-transfer connection used after suppressing the modeled thread.

## Boundary Conditions and Clamping Load

A Fixed Support was applied to the bottom face of the base. The 1885 N clamping force was applied to `MovingPart` along the `Lead Screw` axis in the clamping direction.

The load comes from the previous hand calculation:

- Hand force: `F_hand = 50 N`
- Wheel radius: `r = 30 mm = 0.03 m`
- Input torque: `T = F_hand r = 50 x 0.03 = 1.5 N*m`
- Assumed thread efficiency: `eta = 0.30`
- Lead: `p = 1.5 mm/rev = 0.0015 m/rev`
- Estimated clamping force: `F_clamp = eta(2 pi T)/p = 0.30(2 pi x 1.5)/0.0015 = 1885 N`, approximately `1.9 kN`

This force is an engineering estimate, not a measured physical clamping load.

## Mesh

The final mesh contains 65,406 nodes and 33,417 elements. The finite-element mesh divides the geometry into small elements in which ANSYS calculates displacement, strain, and stress numerically. Suppressing the modeled thread prevented very small thread features from creating an unnecessarily heavy or unstable mesh.

![Final assembly finite-element mesh.](../Images/Analysis/ANSYS/ANSYS_Assembly_Mesh.png)

**Figure 1.** Final assembly finite-element mesh.

## Initial Failed Solution

The first assembly solution was not accepted as a valid design result. A simple Displacement boundary condition was applied to the flat circular end face of `Lead Screw` with `X = 0`, `Y = Free`, and `Z = Free`.

That preliminary model reported:

| Preliminary result | Value |
|---|---:|
| Maximum equivalent stress | approximately 1.0002e10 Pa = 10,002 MPa |
| Minimum safety factor | approximately 0.034994 |
| Maximum deformation | approximately 0.936 mm |

The stress peak occurred around the `NonMovingPart` / `Lead Screw` support region. The result was rejected as non-physical because the 10 GPa stress was far beyond the material yield strengths, was highly localized, coincided with support/contact overlap warnings, and resulted from an artificial local constraint or numerical singularity.

> **The 10,002 MPa result was not used as a final design result and must not be interpreted as a real component stress.**

Recognizing and correcting a non-physical result is part of proper FEA practice; solver convergence alone does not establish physical validity.

## Cylindrical Support Attempt

A Cylindrical Support with `Radial = Fixed`, `Axial = Fixed`, and `Tangential = Free` was considered. ANSYS selected almost the entire smooth cylindrical outer surface of `Lead Screw`. Applying this support would have constrained the screw over nearly its full length and would not represent the real bearing/support region. The approach was therefore rejected before the final solution.

## Model Correction

The ordinary Displacement condition and the problematic support/contact definition were suppressed. The corrected model used Remote Displacement on the flat circular end face of `Lead Screw`. Its purpose was to prevent axial screw translation while avoiding an excessively rigid local constraint.

The mechanical assumption represented is: **the Lead Screw can rotate, but it cannot translate axially.** This remains an idealized support representation and does not explicitly model a bearing, collar, thrust washer, clearance, or friction.

## Final Results

| Final corrected result | Value | Location / interpretation |
|---|---:|---|
| Maximum equivalent von Mises stress | `1.3648e8 Pa = 136.48 MPa` | `Guide_Rod` |
| Average equivalent stress | `3.6025e6 Pa = 3.60 MPa` | Whole reported model average |
| Maximum total deformation | `1.0142e-4 m = 0.10142 mm` | `Handle` |
| Average total deformation | `3.129e-5 m = 0.03129 mm` | Whole reported model average |
| Minimum deformation | `0 m = 0 mm` | Fixed base |
| Minimum safety factor | `2.9438` | `MovingPart` |
| Maximum displayed safety factor | `15` | Stress Tool display cap, not necessarily the true maximum |

### Equivalent von Mises Stress

Equivalent von Mises stress converts a multiaxial stress state into one scalar value for comparison with ductile-material yield strength. The final maximum is 136.48 MPa on a `Guide_Rod`.

![Final equivalent von Mises stress distribution.](../Images/Analysis/ANSYS/ANSYS_Assembly_Equivalent_Stress.png)

**Figure 2.** Final equivalent von Mises stress distribution.

### Total Deformation

Total deformation is the displacement magnitude `U = sqrt(Ux^2 + Uy^2 + Uz^2)`. The maximum is 0.10142 mm at the `Handle`; the fixed base has zero displacement.

ANSYS initially displayed the shape using Auto Scale of approximately `1.3e+002`, visually magnifying displacement by about 130 times. The final plot uses `1.0 (True Scale)`. The plotted shape is a visualization aid; the numerical deformation is the physical result.

![Final total deformation displayed at true scale (1.0).](../Images/Analysis/ANSYS/ANSYS_Assembly_Total_Deformation_TrueScale.png)

**Figure 3.** Final total deformation displayed at true scale (1.0).

### Safety Factor

For the linear elastic static interpretation, safety factor is approximately `FoS = Yield Strength / Equivalent Stress`. The minimum value is 2.9438 on `MovingPart`. A value above 1 indicates that the local equivalent stress is below the assigned yield strength for this modeled load case.

![Final static safety-factor distribution.](../Images/Analysis/ANSYS/ANSYS_Assembly_Safety_Factor.png)

**Figure 4.** Final static safety-factor distribution.

The highest stress and lowest safety factor occur on different components without contradiction. `Guide_Rod` carries the highest local stress but uses stronger AISI 1045 steel. `MovingPart` uses lower-yield AISI 1020 steel. Safety factor depends on both local stress and the assigned yield strength.

## Comparison with Previous Analyses

| Evaluation | Guide-rod maximum stress |
|---|---:|
| Later hand-calculation cantilever approximation | approximately 144 MPa |
| SOLIDWORKS SimulationXpress | approximately 139 MPa |
| Final ANSYS full assembly | 136.48 MPa |

The similar order of magnitude is a useful sanity check, not exact validation. Boundary conditions, contact definitions, mesh assumptions, and geometric simplification differ. The 144 MPa comparison uses the later cantilever idealization; earlier preliminary project calculations used a different load/support assumption and should not be treated as the same case.

The standalone smooth `Lead Screw` SimulationXpress study reported approximately 25.4 MPa stress, 0.0164 mm deformation, and a factor of safety of approximately 20.8. The hand calculation using the real threaded tensile area reported approximately 32.5 MPa and a preliminary factor of safety of approximately 9.5 using a conservative 310 MPa yield assumption. These studies evaluate local screw behavior, whereas the ANSYS model evaluates the global assembly load path.

## Limitations

- Linear static behavior and the selected material datasets are assumed.
- The 1885 N load is calculated from assumed hand force and thread efficiency; it was not measured.
- The M10x1.5 thread geometry and local thread-root/contact stresses are omitted.
- `Lead Screw` to `MovingPart` is Bonded rather than modeled as threaded contact.
- Sliding interfaces are idealized as frictionless; clearances, tolerances, wear, and actual friction are omitted.
- Remote Displacement is an idealized axial support, not a detailed bearing/collar model.
- Mesh convergence and localized submodel refinement are not documented here.
- Manufacturing residual stress, preload history, nonlinear contact, plasticity, fatigue, impact, buckling, and physical test correlation are outside this study.

## Conclusions

After correcting the non-physical support model, the final ANSYS analysis predicts a maximum equivalent stress of 136.48 MPa, maximum total deformation of 0.10142 mm, and minimum safety factor of 2.9438 under the estimated 1885 N clamping load. These values indicate an acceptable preliminary static strength margin within the current assumptions.

The failed 10 GPa solution was correctly rejected, and the boundary conditions were revised to better represent a screw that rotates without axial translation. The result supports continued design development, but it does not fully validate the physical product. Final confidence requires refined contact/support modeling, mesh-convergence checks, verified material data, and physical testing.
