# Settings Ownership Audit

## Purpose

Use this method to review who owns a setting, how precedence should work, and
whether UI, persistence, and runtime enforcement all reflect the same policy.

## Review Steps

1. Identify the setting or setting group under review.
2. Use the adapter to map the control into the local ownership vocabulary.
3. Check whether the current behavior matches the intended bucket:
   - managed or preset-owned
   - session-only user override
   - request-scoped action
   - server-managed or policy-only control
4. Compare three layers for consistency:
   - UI presentation and affordances
   - client persistence or session behavior
   - server or runtime enforcement
5. Classify the narrowest failure:
   - ownership misclassification
   - precedence conflict
   - UI and runtime mismatch
   - unsafe persistence
   - ambiguous managed-state UX

## Output Expectations

- Name the control reviewed.
- State current and expected ownership.
- Identify where enforcement drift exists, if any.
- Map the issue to the smallest owner layer.
- End with one concrete next action.

## Boundaries

- Do not turn this into a layout or visual polish review.
- Do not assume editability just because the runtime can technically support it.
- Do not stop at UI behavior if forbidden state is still accepted downstream.
