# API Smoke Patterns

## Purpose

Use this method to run or interpret repeatable API smoke checks. The objective
is to localize the first failing stage quickly, not to complete full root-cause
analysis.

## Review Steps

1. Identify the scenario under test from the adapter:
   - baseline reachability
   - response content validation
   - streaming validation
   - repeat-request cache validation
   - degraded or fallback validation
2. Use the adapter to choose the correct endpoint, script, flags, and expected
   headers or response markers.
3. Execute the narrowest smoke scenario that answers the user request.
4. Record observable results only:
   - status code or transport failure
   - whether content returned
   - whether streaming occurred when expected
   - whether cache indicators behaved as expected
   - whether degraded-mode behavior still returned a valid response
5. Stop once the failing stage is localized.

## Output Expectations

- State the endpoint and command used.
- Report PASS, FAIL, or UNVERIFIED per scenario.
- Name the first failing stage.
- End with one concrete next action.

## Boundaries

- Do not treat smoke success as proof that quality, telemetry, or retrieval are
  correct.
- Do not drift into deep debugging once the failing stage is known.
- Do not assume every validation signal applies to every endpoint.
