# Admin Surface Hierarchy Audit

## Purpose

Use this method to review the structural hierarchy of dense admin surfaces
before changing visual styling. The goal is to identify the smallest
structural fix that restores a clear depth model.

## Review Steps

1. Identify the target page or surface and list its top-level workflow regions.
2. Map each region onto the local depth model supplied by the adapter.
3. Check which primitive owns the seam for each region.
4. Look for hierarchy failures:
   - nested framed surfaces that duplicate containment
   - competing seams where parent and child both draw strong boundaries
   - fragmentation where one logical workflow is split into too many shells
   - placement drift where a primitive is used at the wrong depth
   - mode-toggle misuse where structure changes instead of state
5. Recommend the smallest batch of fixes that restores one clear owner per
   seam.

## Output Expectations

- Name the surface reviewed.
- State the intended depth map.
- Call out the dominant structural failure.
- Tie each finding to seam ownership rather than visual preference alone.
- End with one concrete next action.

## Boundaries

- Do not turn this into a token or color audit.
- Do not focus on drawer-only affordances unless the adapter says the drawer is
  part of the structural problem.
- Do not propose broad shared-primitive changes unless the issue clearly cannot
  be fixed in local composition or feature markup.
