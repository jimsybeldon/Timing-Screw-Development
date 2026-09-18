# Timing Screw Development

This project investigates how to create and manufacture a timing screw whose cutting geometry changes along a helical path. The repository contains SolidWorks 2026 source files, a STEP export, and planning notes for SolidWorks, Siemens NX, and Solid Edge.

## Why CAM is the better fit for this problem

CAD and CAM overlap, but they solve different problems:

- **CAD** defines a static design: parts, bodies, surfaces, assemblies, and nominal dimensions.
- **CAM** defines and evaluates a manufacturing process: a tool shape, its position, its orientation, and its motion through stock.

The difficult operation in this project is not simply making a helical solid. It is simulating a cutter that moves along a helix while its lead, radius, and orientation may change. A useful representation is:

```text
T(t) = R(t) · P(t)
```

where `P(t)` is the cutter position along the path and `R(t)` is its changing orientation. CAM packages are designed to evaluate this time-varying rigid-body motion directly. They can use a custom cutter, interpolate tool-axis changes, check collisions, and calculate the material removed without first requiring the entire swept envelope to exist as a conventional CAD solid.

For this timing-screw problem, CAM therefore has several practical advantages:

1. **General cutter motion**: tool-axis tilt, roll, yaw, and independent rotation can be controlled along a curve.
2. **Custom tool geometry**: the cutter can be represented as a form tool or arbitrary tool body instead of being reduced to a simple sketch profile.
3. **Swept-volume evaluation**: the system calculates the envelope created by the moving tool as part of toolpath or machine simulation.
4. **Manufacturing validation**: collision checking, gouge detection, residual-stock analysis, and machine simulation are built into the workflow.
5. **Direct production output**: the validated motion can be post-processed into machine-specific NC code.

This is a problem-specific superiority, not a claim that CAM replaces CAD. CAD is still valuable for the screw blank, tool definition, assembly layout, reference geometry, and communicating the final design. CAM becomes the stronger authority for the question: **what material does this moving cutter actually remove?**

## The CAD limitation observed here

The SolidWorks experiments show why a conventional solid sweep is a poor match for the complete operation. Solid Sweep has restrictive input requirements, including constraints on the tool body and the continuity of the path. A composite path made from constant-pitch, variable-pitch, and tapered helices may meet positionally while still introducing a lead, radial, or curvature discontinuity at a segment boundary.

CAD feature errors can consequently be generic or misleading. A failure reported as a tangent-continuity problem may also be caused by a discontinuous change in radius or curvature, or by the tool body not satisfying the solid-sweep rules. The fallback used in the project was to split the geometry into three single-helix parts and assemble the result.

CAM avoids making the complete result depend on one restrictive swept-solid feature. It can sample or continuously interpolate the tool motion, apply the cutter transform at each location, and validate the resulting process. The exact capabilities and terminology vary by package, so the tool body, path continuity, machine kinematics, and postprocessor still need verification.

## Recommended workflow

1. **Define the design in CAD**
   - Create the cylindrical screw blank.
   - Define the cutter and its axis.
   - Build the helical reference paths.
   - Check the transitions between constant pitch, variable pitch, and tapered regions.

2. **Move the manufacturing problem into CAM**
   - Import the blank and cutter geometry.
   - Define the tool as a custom or form tool where required.
   - Create a curve-driven, multi-axis, or swept-volume toolpath.
   - Apply the intended orientation law, including any 90-degree cutter rotation.
   - Simulate the tool and machine, checking collisions, gouges, and remaining stock.

3. **Validate the result**
   - Compare the simulated cut with the intended timing-screw envelope.
   - Inspect the A-to-B and B-to-C transitions.
   - Confirm that the machine, holder, fixtures, and tool-axis limits are valid.
   - Post-process only after the simulation is acceptable.

## Repository contents

### CAD data

- [`data_SW2026/Timing_Screw_Assy_SW_1.SLDASM`](data_SW2026/Timing_Screw_Assy_SW_1.SLDASM): SolidWorks assembly of the segmented timing screw.
- [`data_SW2026/Timing_Screw_Assy_SW_1.STEP`](data_SW2026/Timing_Screw_Assy_SW_1.STEP): neutral CAD exchange export.
- [`data_SW2026/SW_Timing_Screw_Multi_Body_1.SLDPRT`](data_SW2026/SW_Timing_Screw_Multi_Body_1.SLDPRT)
- [`data_SW2026/SW_Timing_Screw_Multi_Body_2.SLDPRT`](data_SW2026/SW_Timing_Screw_Multi_Body_2.SLDPRT)
- [`data_SW2026/SW_Timing_Screw_Multi_Body_3.SLDPRT`](data_SW2026/SW_Timing_Screw_Multi_Body_3.SLDPRT)

The three part files represent the practical segmented approach used after the single complex sweep proved unreliable.

### Documentation

- [`docs/CAM_packages_can_do_this_better.md`](docs/CAM_packages_can_do_this_better.md): rationale for using CAM to handle arbitrary cutter geometry, tool-axis rotation, curve-driven motion, and swept-volume simulation.
- [`data_SW2026/README_road_map_Sw2026.md`](data_SW2026/README_road_map_Sw2026.md): SolidWorks 2026 modeling paths, solid-sweep constraints, and fallback methods.
- [`docs/road_map_NX.md`](docs/road_map_NX.md): Siemens NX swept-volume and Boolean-subtract workflow, including optional table-driven motion.
- [`docs/road_map_SolidEdge.md`](docs/road_map_SolidEdge.md): Solid Edge Solid Sweep Cutout workflow and its tool-body constraints.
- [`docs/NX_video_tutorial_links.md`](docs/NX_video_tutorial_links.md): reference videos for NX swept volume and Boolean operations.

## Current conclusion

The existing CAD files are useful design and exchange artifacts, but the full timing-screw cutting process should be developed and validated in a CAM package with custom-tool and multi-axis motion support. Siemens NX, Mastercam, and comparable systems are promising candidates because their workflows treat the cutter as a moving manufacturing tool rather than requiring every position of that tool to be prebuilt as a static CAD solid.

The next technical milestone is a controlled CAM simulation using the STEP model or native CAD data, a defined custom cutter, and explicit motion laws for the three helical regions. The simulation should be treated as the source of truth for manufacturability; the CAD model should remain the source of truth for design intent and exchange.

## License

This project is distributed under the terms of the [GNU General Public License v3.0](LICENSE).