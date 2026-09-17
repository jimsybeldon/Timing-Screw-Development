Here's the corrected SolidWorks 2026 roadmap. Phases 0–3 are unchanged from before; Phase 4 is rewritten to reflect what **Solid Sweep** actually does and what it actually requires — which is stricter than the fallback method I described, so it doesn't remove the need for that fallback, it just changes when you need it.

## Phase 0 — Part setup
Multibody part (blank + tool as separate solid bodies). Tools > Options > Document Properties for units.

## Phase 1 — Screw blank (target cylinder)
1. Sketch circle on Front Plane at target OD.
2. **Features tab > Extruded Boss/Base**, depth = full screw length. Body 1.

## Phase 2 — Three helices + composite path
Same as before: **Features tab > Curves > Helix/Spiral** for each segment.
- Helix A — Constant pitch, no taper (baseline).
- Helix B — check **Variable pitch**, enter increasing Pitch values in the region table (progressive lead). Sketch its start circle at Helix A's endpoint.
- Helix C — Constant pitch + **Taper Helix** checked, set taper angle/outward (increasing radius). Sketch its start circle at Helix B's endpoint.
- **Insert > Curve > Composite Curve**, select A, B, C in order.
- Same caveat as before: this gives positional continuity at the joints, not tangency — matters for Phase 4.

## Phase 3 — Cutting tool body
Build it as **Revolve Boss/Base**, with **Merge result unchecked**, so it stays Body 2 (separate from the blank).

## Phase 4 — The boolean sweep cut (corrected)

**Insert > Cut > Sweep** (Swept Cut). In the PropertyManager, under *Profile and Path*, choose **Solid sweep** instead of Sketch/Circular profile. Select Body 2 as the tool body and the Composite Curve as the path.

This is a real, first-class feature — not a workaround — but it has hard constraints on the tool body that you should check against your "complex tool body" before committing to this route:

- **Convex.** Not merged with the main body (this is why Merge result had to be unchecked in Phase 3).
- Must be either **a revolved feature using only analytical geometry** (lines and arcs — no splines) **or a cylindrical extruded feature**. Nothing else qualifies.
- The path **must be tangent within itself — no sharp corners** — and must begin at a point on or within the tool body's profile.
- SolidWorks consumes/removes the tool body as part of the cut.

Two things this means for your specific setup:
1. **The tangency requirement on the path is not optional here the way it was cosmetic before** — Solid Sweep will reject a path with a hard kink, and your Composite Curve's tangency at the A→B and B→C joints is only guaranteed positionally, not tangentially, by construction. You need to actually check/match the lead angle at each joint before this feature will take the path at all (SolidWorks won't silently tolerate the mismatch the way Solid Edge's "Place tool on Path" option does).
2. **If your tool body is genuinely complex — concave, has a b-spline profile, isn't a simple revolve or cylindrical extrusion — Solid Sweep will refuse it outright**, full stop, regardless of the path.

## Phase 4b — Fallback (tool body fails the Solid Sweep constraints, or path tangency can't be fixed)
1. Extract the tool's silhouette as a 2D profile (Convert Entities/Intersection Curve on a plane normal to the path), then run an ordinary **Sketch-profile Swept Cut** along the Composite Curve. This tolerates non-tangent paths and any tool shape, at the cost of only capturing a static cross-section rather than the tool's actual 3D form.
2. For a tool body that's both non-convex/non-revolved *and* needs its full 3D shape preserved: **Combine (Subtract)** once at the path start, then **Curve Driven Pattern** that Combine feature along the Composite Curve with tight overlapping spacing.

**For Orientation/twist**, whichever route you use: set *Follow Path* with Path alignment = *None* — this is what correctly keeps the tool/profile tracking the helix's changing tangent through all three segments rather than holding a fixed orientation.

## Phase 5 — Cleanup
Fillets, then check the A→B and B→C joints via section view or Interference Detection for gouging/residual stock — same as before, but now doubly important since it's also a gating condition for Phase 4 succeeding at all, not just a cosmetic risk.

The practical fork is: check your actual tool geometry against the convex/analytic-or-cylindrical test first — that decides whether you're in Phase 4 or Phase 4b before you spend time matching tangency at the helix joints.