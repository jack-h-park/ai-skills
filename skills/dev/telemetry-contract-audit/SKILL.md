---
name: telemetry-contract-audit
description: Use this skill when the user says things like "telemetry looks wrong", "trace looks wrong", "event fields changed", "field semantics drifted", "finish reason is wrong", "cache semantics look off", "PII boundary check", "sampling/detail issue", or "telemetry contract drift" and the task is to verify that a repository's telemetry still obeys its documented signal contract. Use it for contract-level review of field semantics, summaries, cache truthfulness, finish or outcome semantics, privacy boundaries, and telemetry-control behavior. Do NOT use it for diagnosing a single retrieval issue, reviewing citation quality in one trace, running live incident triage after the alert is already understood, or doing broad product interpretation.
---

# When to use
- Use this skill to audit whether telemetry still tells the truth about runtime behavior in a repo.
- Use it when the question is semantic correctness, contract drift, missing summaries, cache truthfulness, finish or outcome classification, privacy boundaries, or telemetry-control behavior.
- Do not use it for single-trace retrieval diagnosis, on-call incident response, or general debugging once the telemetry contract violation is no longer the main question.

# Goals
- Verify that the local telemetry contract still matches emitted runtime evidence.
- Verify that traces, analytics events, and summary outputs stay semantically consistent.
- Verify that privacy and detail-level controls still enforce the intended local policy.
- Classify the narrowest telemetry contract failure and identify the smallest owner layer that must change.

# Required references
- Canonical playbook: `jackhpark-ai-skills/playbooks/telemetry-contract-audit.md`
- Required local adapter content:
  - local telemetry invariants
  - vendor surfaces
  - exact signals under review
  - alert or dashboard realization notes when relevant

# Workflow
1. If the canonical playbook or local adapter has already been referenced in the conversation, reuse that context instead of re-reading.
2. Read the canonical playbook for the generic audit method and the local adapter for repo-specific invariants, signals, vendor surfaces, alert groups, and control knobs.
3. Identify which local contract slice is under review: trace summaries, analytics event semantics, cache semantics, finish or outcome semantics, privacy boundaries, alert and dashboard realization, or telemetry-control behavior.
4. Use the adapter to select the exact local signals, surfaces, and canonical invariants that apply to that slice.
5. Compare observed runtime evidence against the local contract before using implementation details to explain the mismatch.
6. Report the narrowest contract failure and stop before drifting into retrieval trace review, live incident playbooks, or product interpretation.

# Output format
- Scope reviewed
- Local invariant or contract slice checked
- Exact local signals reviewed
- Observed evidence
- Result: pass | warning | fail | unverified
- Whether the issue is in: instrumentation emission | canonical semantic contract | vendor realization | privacy/PII policy | runtime-to-telemetry outcome mapping
- Whether the affected scenario is: success | cache hit | retrieval | abort | error
- Primary classification
- Most likely owner layer
- Severity
- Next single action

Required ending:
- `Primary classification:` missing telemetry | semantically incorrect telemetry | contradictory telemetry | unsafe telemetry | unverifiable telemetry
- `Owner layer:` instrumentation | contract/schema semantics | analytics/dashboards | privacy/governance | runtime outcome mapping
- `Severity:` critical | warning | info
- `Next single action:` one concrete follow-up step only

# Common pitfalls
- Do not restate the full telemetry audit method here; use the canonical playbook.
- Do not inline the repo's complete event schema, trace schema, or alert contract here; use the local adapter.
- Do not treat a single bad retrieval trace as a telemetry-contract audit by default.
- Do not confuse dashboard symptoms with canonical signal semantics.
- Do not expand into incident triage once the task has moved beyond contract verification.
