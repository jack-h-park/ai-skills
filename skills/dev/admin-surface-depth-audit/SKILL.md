---
name: admin-surface-depth-audit
description: Use this skill when the user says things like "admin UI messy", "nested cards", "double borders", "too many panels", "depth issue", "card explosion", "seams look wrong", "admin layout hierarchy", or "surface structure is off" and the task is to audit or refine the structural hierarchy of an admin surface. Use it for information architecture, section depth, seam ownership, nested-surface drift, primitive placement, and page-level hierarchy on dense operational surfaces. Do NOT use it for settings-policy decisions, drawer-only affordance tuning, or generic CSS token audits that are not about hierarchy and surface structure.
---

# When to use
- Use this skill to review the structure of dense admin or operational surfaces.
- Use it when the problem is hierarchy, too many framed regions, wrong depth, competing seams, or primitive-placement drift.
- Do not use it for settings ownership and policy, drawer affordances, or purely cosmetic token issues.

# Goals
- Map the target surface onto the depth model supplied by the local adapter.
- Identify hierarchy violations, nested-surface drift, or conflicting seam ownership.
- Verify that local primitive usage and component placement still match the intended structure.
- Produce a fix plan grouped into reviewable batches rather than scattered one-off tweaks.

# Required references
- Canonical playbook: `jackhpark-ai-skills/playbooks/admin-surface-hierarchy-audit.md`
- Required local adapter content:
  - local depth vocabulary
  - primitive mappings
  - page or surface maps
  - repo-specific exclusions

# Workflow
1. If the canonical playbook or local adapter has already been referenced in the conversation, reuse that context instead of re-reading.
2. Read the canonical playbook for the generic hierarchy-review method and the local adapter for repo-specific depth vocabulary, primitive mappings, and page maps.
3. Identify which local admin or operational surface is under review and which page-specific depth map applies.
4. Use the adapter to map local primitives, component boundaries, and page sections onto the shared depth and anti-pattern framework.
5. Classify the issue by structure: nested surfaces, competing seams, fragmentation, mode-toggle misuse, placement drift, or double framing.
6. Report the intended local depth map and the smallest useful batch of hierarchy fixes. Do not expand into settings policy or drawer-specific affordance work.

# Output format
- Surface reviewed
- Intended local depth map
- Key hierarchy findings
- Implicated local primitive or pattern
- Primary classification
- Most likely owner layer
- Whether the recommended fix stays inside: feature component markup | feature CSS module | shared primitive placement or naming cleanup
- Fix priority
- Next single action

Required ending:
- `Primary classification:` nested-surface drift | competing seams | fragmentation | mode-toggle misuse | placement drift | double framing
- `Owner layer:` UI structure | component composition | primitive placement | feature markup | feature CSS module
- `Fix priority:` now | later
- `Next single action:` one concrete follow-up step only

# Common pitfalls
- Do not restate the playbook in full; use the canonical playbook.
- Do not inline full page maps or primitive matrices here; use the local adapter.
- Do not turn a hierarchy audit into a settings-policy review.
- Do not suggest moving feature-specific structure into shared primitives without checking the local placement rules.
- Do not report isolated visual nits without tying them to a hierarchy or seam problem.
