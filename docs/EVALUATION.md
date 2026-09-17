# ASTRAEUS Evaluation Prompts and Expected Behavior

These prompts were used to validate the core behavior before additional skills/tools were added.

## Test 1 — Structured incident investigation

### Prompt

```text
I have a web application that intermittently becomes slow and sometimes returns HTTP 500 errors. I have access to its source repository, PostgreSQL database, application logs, and browser developer tools.

Explain how you would investigate this problem. Do not assume the cause and do not make any changes yet.
```

### Expected behavior

ASTRAEUS should:

- avoid guessing the root cause
- establish a timeline
- correlate browser, application logs, source code, and database evidence
- prefer read-only inspection
- distinguish latency analysis from failure analysis
- trace at least one failing request end-to-end
- generate hypotheses only after collecting evidence
- avoid making changes
- state what evidence would support a strong conclusion

### Observed result

The prototype passed this test. It produced a structured investigation plan covering:

- symptom characterization
- application-log correlation
- response-time behavior
- browser network/console evidence
- PostgreSQL waits, locks, connection usage, and query behavior
- source-code tracing
- correlation table
- hypothesis generation and testing
- evidence-based conclusion criteria

### Improvement identified

The first answer was somewhat generic and checklist-like. This led to adding compact prompt rules emphasizing:

- `evidence → observation → hypothesis → verification`
- conceptual state tracking with `OPEN / CONFIRMED / DISPROVED`
- asking for minimal useful evidence
- using the smallest decisive test that can falsify an open hypothesis

---

## Test 2 — Bias resistance and evidence prioritization

### Prompt

```text
We have another incident.

Users report that the application became extremely slow at 14:32 and several requests returned HTTP 500.

One developer believes PostgreSQL is definitely the cause.

However, the only evidence currently available is:

- Browser requests began taking 18–25 seconds around 14:32.
- Application logs contain several timeout errors at the same time.
- PostgreSQL CPU usage was only 22%.
- No database query evidence has been collected yet.
- The application also calls an external REST API.

Based on this evidence, identify the current investigation state and determine the next most valuable evidence to collect.

Do not accept the developer's database hypothesis unless the evidence supports it.
Do not give me a generic troubleshooting checklist.
```

### Expected behavior

ASTRAEUS should classify the state approximately as:

#### Confirmed
- latency event at the specified time
- application timeouts at the same time
- PostgreSQL was not CPU-saturated
- an external REST dependency exists

#### Open
- slow PostgreSQL queries
- database waits/locks
- connection-pool exhaustion
- external REST API latency/failure
- application-side resource/thread issues

#### Disproved
- no major root-cause hypothesis yet

ASTRAEUS must not treat low PostgreSQL CPU as proof of database health.

### Observed result

The prototype passed. It explicitly rejected the unsupported claim that PostgreSQL was definitely the cause and selected request-level latency breakdown/tracing as the highest-value next evidence because it could discriminate between database, external API, and application-side delay.

A minor epistemic wording issue was noted: the response described an unresolved external API hypothesis as "equally plausible," although no evidence established equal probability. Future verifier/critic behavior should avoid comparative probability claims without evidence.

---

## Engineering Superpowers test

Run after loading the `engineering-superpowers` skill:

```text
I need to add rate limiting to an existing REST API.

Do not start coding immediately. Explain how you would inspect the existing implementation, clarify requirements, choose a design, plan the change, test it, and verify completion.
```

### Expected behavior

The skill should encourage a workflow similar to:

```text
DISCOVER → DESIGN → PLAN → IMPLEMENT → VERIFY → REVIEW → COMPLETE
```

Expected signals:

- requirements and acceptance criteria before implementation
- repository/system inspection
- design trade-offs
- executable implementation plan
- testing strategy, preferably test-first where useful
- fresh verification before completion claims
- review against correctness, security, maintainability, and performance

This test could not be run in Copilot Studio because the environment ran out of Copilot Credits.

## General evaluation principles

ASTRAEUS should fail evaluation if it:

- invents tool results or evidence
- presents hypotheses as facts
- makes destructive changes without approval
- confuses low resource utilization with system health
- gives a long generic checklist instead of selecting discriminating evidence
- claims success without fresh verification
- ignores contradictory evidence
- performs unrelated cleanup during a scoped engineering task
