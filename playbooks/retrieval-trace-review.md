# Retrieval Trace Review

## Purpose

Use this method to determine where support disappeared between retrieval and
the final answer context. The goal is to identify the narrowest failing stage.

## Review Steps

1. Identify the trace slice under review using the adapter:
   - retrieval summary
   - selection summary
   - verbose retrieval diagnostics
   - answer-stage support impact
2. Compare the amount and quality of raw support retrieved with the support
   that survived selection and context assembly.
3. Classify the dominant pressure:
   - weak retrieval
   - deduplication pressure
   - quota or diversity pressure
   - token-budget pressure
   - strategy convergence or trace ambiguity
4. Confirm whether the answer failure started upstream at retrieval or
   downstream during selection or context assembly.
5. Stop once the owner layer is clear enough for follow-up work.

## Output Expectations

- State the observations reviewed.
- Name the dominant failing stage.
- Report the dominant pressure.
- Map the issue to the narrowest owner layer.
- End with one concrete next action.

## Boundaries

- Do not use this method for broad telemetry-contract auditing.
- Do not treat a weak answer alone as proof of weak retrieval.
- Do not continue into ingestion or model-quality review once the retrieval
  stage failure is already clear.
