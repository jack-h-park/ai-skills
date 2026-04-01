---
name: rag-trace-review
description: Use this skill when the user says things like "RAG quality", "citations missing", "retrieval issue", "selection pressure", "dedupe pressure", "quota pressure", "token budget clipping", "why did retrieval fail", or "trace review" and the task is to inspect retrieval traces and selection traces to determine where support was lost. Use it for contract-level review of retrieval weakness versus downstream selection pressure, dedupe pressure, quota pressure, budget clipping, or trace ambiguity. Do NOT use it for verifying the global telemetry contract, reviewing ingestion write-path correctness, or doing broad model-quality review once the failing retrieval stage is no longer the main question.
---

# When to use
- Use this skill to review retrieval traces when the question is where support disappeared between retrieval and the final answer context.
- Use it when the problem sounds like weak retrieval, missing citations, insufficient support, selection pressure, dedupe pressure, quota pressure, or token-budget clipping.
- Do not use it for telemetry-contract auditing, ingestion verification, broad model-quality review, or general debugging outside the retrieval trace.

# Goals
- Verify whether support was missing from the start or lost during downstream selection.
- Distinguish weak retrieval from dedupe pressure, quota pressure, budget clipping, or trace ambiguity.
- Map the failure to the narrowest local owner layer.
- Stop once the failing retrieval stage is clear enough to hand off or implement the next change.

# Required references
- Canonical playbook: `jackhpark-ai-skills/playbooks/retrieval-trace-review.md`
- Required local adapter content:
  - local trace names
  - stage map
  - metric glossary
  - ownership clues

# Workflow
1. If the canonical playbook or local adapter has already been referenced in the conversation, reuse that context instead of re-reading.
2. Read the canonical playbook for the generic retrieval-review method and the local adapter for repo-specific trace names, stage map, metrics, and ownership clues.
3. Identify which local trace slice is under review: retrieval summary, selection summary, verbose retrieval diagnostics, or answer-stage support impact.
4. Use the adapter to map the request onto the local observations, stage names, and metrics.
5. Compare raw support, selected support, and final answer support to classify the dominant failure stage.
6. Report the narrowest retrieval failure and stop before drifting into telemetry-contract review, ingestion verification, or general model-quality critique.

# Output format
- Scope reviewed
- Observation(s) reviewed
- Strategy path active
- Failing stage
- Observed evidence
- Dominant pressure
- Primary classification
- Most likely owner layer
- Confidence
- Next single action

Required ending:
- `Primary classification:` weak retrieval | selection pressure | deduplication pressure | quota or diversity pressure | budget pressure | trace ambiguity
- `Owner layer:` retrieval logic | selection logic | context assembly | trace instrumentation
- `Confidence:` high | medium | low
- `Next single action:` one concrete follow-up step only

# Common pitfalls
- Do not restate the full retrieval-review method here; use the canonical playbook.
- Do not inline the repo's trace schema, metric glossary, or strategy matrix here; use the local adapter.
- Do not treat a single bad answer as proof of weak retrieval without checking downstream selection pressure.
- Do not turn this skill into telemetry-contract review, ingestion review, or broad model-quality commentary.
- Do not keep digging once the failing retrieval stage is already clear.
