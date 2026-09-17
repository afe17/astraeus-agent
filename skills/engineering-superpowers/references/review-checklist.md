# Engineering Review Checklist

Use only relevant sections.

## Correctness
- Does the implementation satisfy confirmed requirements?
- Are edge cases that materially affect correctness handled?
- Are failures surfaced intentionally?

## Architecture
- Does it fit existing repository patterns?
- Are dependencies flowing in a sensible direction?
- Is new complexity justified?

## Security
- Any credential, authorization, injection, path, deserialization, or trust-boundary concern?
- Is sensitive data unnecessarily logged or returned?
- Is least privilege preserved?

## Reliability
- Timeouts, retries, idempotency, transactions, concurrency, cleanup?
- Could partial failure leave inconsistent state?

## Performance
- Obvious N+1 behavior, unbounded work, expensive repeated I/O, large allocations, or blocking operations?
- Is optimization evidence-driven?

## Tests
- Is changed behavior directly covered?
- Is the test capable of failing when the behavior regresses?
- Are assertions checking outcomes rather than incidental implementation details?

## Completion
- Was fresh verification run?
- Do claims match the verification evidence?
- Are remaining limitations stated?
