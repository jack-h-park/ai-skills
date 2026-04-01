---
name: chat-api-smoke-regression
description: Use this skill when the user says things like "API not working", "run the smoke test", "check the chat endpoint", "verify streaming", "cache-hit header missing", or "degraded-mode smoke" and the task is to run or interpret repeatable smoke checks for chat API entrypoints. Use it especially after backend, guardrail, cache, telemetry, fallback, or debug-surface changes. Do NOT use it for deep root-cause analysis of retrieval quality, citation issues, telemetry-contract review, or broad incident response once the smoke failure is already understood.
---

# When to use
- Use this skill to execute or interpret a repository's chat API smoke workflow.
- Use it when the task is to validate endpoint reachability, streaming, repeat-request cache signaling, or degraded-mode behavior on chat API surfaces.
- Do not use it for retrieval-quality diagnosis, telemetry taxonomy review, ingestion verification, or general debugging after the failing stage is already clear.

# Goals
- Confirm that the target chat API smoke entrypoints still respond.
- Confirm that expected streaming behavior is still observable where applicable.
- Confirm that repeat-request cache signaling still behaves as expected for the local repo.
- Confirm that degraded or fallback smoke scenarios still return a response.
- Localize the narrowest failing smoke stage before deeper debugging starts.

# Required references
- Canonical playbook: `jackhpark-ai-skills/playbooks/api-smoke-patterns.md`
- Required local adapter content:
  - local smoke commands
  - entrypoint mapping
  - validation headers or signals
  - degraded-mode switches and exclusions

# Workflow
1. If the canonical playbook or local adapter has already been referenced in the conversation, reuse that context instead of re-reading.
2. Read the canonical playbook for the generic smoke method and the local adapter for repo-specific entrypoints, commands, validation signals, and exclusions.
3. Identify which local smoke scenario the user is asking about: current endpoint, legacy endpoint, repeat-request cache validation, or degraded-mode and fallback validation.
4. Use the adapter to select the correct local script, request path, flags, and expected validation signals for the scenario.
5. Run or interpret the smoke check and classify the result by stage: reachability, output or content, streaming, cache validation, or degraded-mode behavior.
6. Stop at smoke failure localization. If the issue is clearly a retrieval-quality, telemetry-contract, or broader incident problem, hand off to the appropriate skill instead of expanding scope.

# Output format
- Endpoint tested
- Script or command used
- Scenario executed
- Smoke result per scenario: PASS, FAIL, or UNVERIFIED where the local adapter explicitly allows it
- Key local observables: endpoint response, streaming status, cache signal status, degraded-mode result
- Whether smoke headers were expected and observed
- Whether degraded-mode or local-required preset coverage was included
- Whether debug-surface expectations were part of the run
- Failing stage
- Primary classification
- Most likely owner layer
- Next single action

Required ending:
- `Primary classification:` endpoint/config failure | output/content failure | streaming failure | cache validation failure | degraded-mode failure
- `Owning layer:` API | transport/streaming | caching | runtime/config | fallback/degraded-mode
- `Failing stage:` baseline request | output validation | streaming validation | repeat-request cache validation | degraded-mode validation
- `Next single action:` one concrete follow-up step only

# Common pitfalls
- Do not re-teach the generic smoke method inside this skill; use the canonical playbook.
- Do not inline the repo's full command matrix or header matrix here; use the local adapter.
- Do not treat smoke success as proof that retrieval, telemetry, or prompt behavior is correct.
- Do not drift into deep root-cause analysis after the failing stage is clear.
- Do not assume every smoke request path or validation signal applies to every local scenario.
