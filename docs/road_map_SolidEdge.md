One correction to my last answer before I get to Solid Edge: SolidWorks' Swept Cut does have a native "solid body as tool" mode in addition to the sketch-profile mode I described — I undersold that. It's still constrained (the tool body has to reduce to a single non-concave revolved solid about an axis), which is why I flagged Method B as a fallback, but it's a first-class option, not just a workaround. Worth knowing since it changes which method is "Method A" in both packages — and as it turns out, Solid Edge's version of this is more directly what you described.

## Solid Edge roadmap

Solid Edge actually has a command purpose-built for exactly what you described — a native **Solid Sweep Cutout** that spins a revolved solid tool body while translating it along a path and subtracts the swept volume. That's a closer match to "boolean subtraction of a complex tool body moving along a path" than anything in SolidWorks' stock toolset, with one real constraint to watch: the tool body must be a single, non-concave, non-disjoint solid of revolution that intersects its own spin axis, and it can't contain holes/cutouts or non-analytic (b-spline) faces. If your "complex tool body" violates any of that, you'll need the fallback in Phase 4b.

### Phase 0 — Part setup
- New Part file. Solid Edge gives you both Ordered and Synchronous modeling; the commands below exist in both, but dialog layout differs slightly — I'm describing Synchronous, since that's the current default workflow.

### Phase 1 — Screw blank (target cylinder)
1. Sketch a circle at OD on your base plane.
2. **Home tab > Solids group > Extrude** → full screw length. This is Body 1.

### Phase 2 — The three helices (as curves)
**Home tab > Curves group > Helix** (may be under the "More Curves" flyout depending on your ribbon config). Each opens the **Helix Options dialog**, with:
- *Helix Method:* Axis Length & Pitch / Axis Length & Turns / Pitch & Turns
- *Taper:* Method = None / By Angle / By Radius
- *Pitch:* Constant / Variable (with either a Pitch Ratio or an explicit End Pitch)

**Helix A — baseline:** Pitch = Constant, Taper Method = None. Set Method/turns/pitch as needed.

**Helix B — progressive lead:** sketch its start circle on a plane located at Helix A's end point (**Home tab > Planes group**, offset/parallel-by-distance from the helix endpoint). Pitch = **Variable**, and specify an **End Pitch** different from the start pitch — Solid Edge interpolates a continuously progressive lead between the two, which is a cleaner mechanism for this than SolidWorks' region table.

**Helix C — increasing radius:** sketch its start circle at Helix B's end. Taper Method = **By Radius**, set Start radius / End radius directly (or By Angle + Outward, if you'd rather drive it by taper angle). Pitch = Constant.

Join them: **Curves group > Composite Curve**, select Helix A, B, C in order. Same caveat as SolidWorks: this guarantees the curves meet at a point, not that their lead angle matches there. Solid Edge is at least explicit about this downstream — the Solid Sweep Cutout command documentation states the path must be tangent and continuous *unless* you use its "Place tool on Path" option, which exists specifically to tolerate a non-tangent composite path like yours at the A→B and B→C joints.

### Phase 3 — Cutting tool body
- Build it as a revolve: **Home tab > Solids group > Revolve**, but use **Add Body** (rather than merging into Body 1) so it stays a distinct solid — Body 2.
- Confirm it meets Solid Sweep Cutout's tool constraints: single connected cross-section when spun about the tool axis, must intersect that axis, no concavity, no holes, no b-spline faces. If it can't meet this, skip to Phase 4b.

### Phase 4 — The boolean sweep cut (native tool-body method)
- **Home tab > Solids group > (flyout next to Sweep) > Solid Sweep Cutout**
- Select: target body (Body 1), tool body (Body 2), the tool's spin axis, and the Composite Curve as the path.
- If the path isn't tangent-continuous at your helix joints, enable **Place tool on Path** to avoid a failed/garbage feature there.
- This performs the actual spinning-tool sweep-subtract in one feature — no discretization, no profile extraction.

### Phase 4b — Fallback, if the tool body fails Solid Sweep Cutout's constraints
1. Profile route (tool cross-section is constant, just not a simple revolve): extract the silhouette via **Project Curve**/derived sketch on a plane normal to the path start, then **Home tab > Solids group > Sweep** (cutout mode), profile = that sketch, path = Composite Curve.
2. True irregular-geometry route: do one **Boolean > Subtract** (Body 1 − Body 2) at the path start, then **Home tab > Pattern group > Pattern Along Curve**, seed = that Subtract feature, driving curve = the Composite Curve, spacing tight enough that instances overlap with no gaps.

### Phase 5 — Cleanup
- Fillet groove edges as needed.
- Check with **Inspect tab > Interference** (or a section view along the axis) at the Helix A→B and B→C transitions for stock left behind or over-cut, same failure mode I flagged for SolidWorks — Solid Edge's "Place tool on Path" option mitigates the sweep failing outright, but it doesn't guarantee the groove profile stays clean across a tangency discontinuity, so it's still worth checking by eye.

If you want, I can go through how to hand-match the exit lead angle of Helix A to Helix B's start (and B's exit to C's constant lead) so the whole path is C1-continuous rather than relying on "Place tool on Path" to paper over the joint.