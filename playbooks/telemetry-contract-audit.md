# Telemetry Contract Audit

## Purpose

Use this method to verify that emitted telemetry still truthfully represents
runtime behavior. The focus is contract correctness, not general debugging.

Use the companion playbook `telemetry-operational-verification.md` when the
task is a scenario-by-scenario verification pass rather than a semantic
contract audit.

## Review Steps

1. Identify the contract slice under review using the adapter:
   - trace summaries
   - analytics event semantics
   - cache semantics
   - finish or outcome semantics
   - privacy or PII boundaries
   - dashboard or alert realization
   - telemetry-control behavior
2. Gather observed runtime evidence and the corresponding documented invariant.
3. Compare observed evidence to the contract before reading implementation code
   for explanation.
4. Classify the narrowest failure:
   - missing telemetry
   - semantically incorrect telemetry
   - contradictory telemetry
   - unsafe telemetry
   - unverifiable telemetry
5. Map the issue to the smallest owner layer and stop.

## Output Expectations

- Name the contract slice reviewed.
- State the exact signals checked.
- Report observed evidence and result.
- Classify the issue and owner layer.
- End with one concrete next action.

## Boundaries

- Do not treat one bad retrieval trace as a telemetry-contract audit by default.
- Do not confuse dashboard symptoms with the canonical contract.
- Do not expand into incident response once contract verification is complete.
