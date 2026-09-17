---
name: "engineering-superpowers"
description: >-
  Use for substantial software engineering work, including requirements clarification,
  solution design, implementation planning, coding, debugging, testing, review, and
  completion verification. Prefer this skill when the user asks to build, change, fix,
  refactor, review, or complete software rather than merely explain a concept.
---

# Engineering Superpowers

## Purpose

Guide ASTRAEUS through disciplined software-engineering work from unclear request to verified result.

This skill complements the agent's global instructions. It does not override security boundaries, human-approval requirements, tool permissions, or evidence discipline.

## Activation

Use this skill when a task involves one or more of:
- designing or implementing software
- fixing a defect
- refactoring existing code
- planning a code change
- reviewing an implementation
- preparing a development branch for completion
- debugging behavior that is likely rooted in code
- creating tests for changed behavior

Do not activate it for simple factual questions that do not require an engineering workflow.

## Core workflow

For non-trivial engineering work, progress through these states:

DISCOVER → DESIGN → PLAN → IMPLEMENT → VERIFY → REVIEW → COMPLETE

Skip a state only when it is genuinely unnecessary, not merely to move faster.

### 1. DISCOVER

Before proposing code:
- establish the user's objective and acceptance criteria
- inspect the existing system when available
- identify constraints, compatibility requirements, interfaces, and affected components
- distinguish confirmed requirements from assumptions
- identify the smallest missing information that blocks a sound design

Do not invent requirements.

When the request is ambiguous in a way that could materially change the implementation, ask focused questions or inspect available project evidence before coding.

### 2. DESIGN

For changes with meaningful architectural impact:
- identify candidate approaches
- compare trade-offs relevant to this task
- prefer the simplest design that satisfies the confirmed requirements
- preserve existing conventions unless there is evidence they should change
- identify data-flow, API, persistence, security, concurrency, and failure-mode implications when relevant

Avoid speculative abstractions and future-proofing without a concrete need.

For small local changes, a short design decision is sufficient.

### 3. PLAN

Create an implementation sequence that is executable and testable.

A good plan:
- names affected components or files when known
- divides the work into small coherent changes
- includes tests alongside behavior changes
- identifies verification steps
- calls out migrations, compatibility risks, or rollback concerns when relevant

Prefer steps that can be independently verified.

When tools allow direct work, the plan is a guide for execution rather than a substitute for execution.

### 4. IMPLEMENT

During implementation:
- make the smallest change that satisfies the current requirement
- follow repository style and established patterns
- avoid unrelated cleanup unless necessary for correctness
- keep interfaces explicit
- handle errors intentionally
- preserve backward compatibility when required
- update tests with behavior changes
- update documentation when user-visible or operational behavior changes

Do not claim code was modified unless a tool result confirms it.

### 5. TESTING DISCIPLINE

Prefer test-first development when behavior can be specified as an observable contract.

Use this loop when practical:

RED → GREEN → REFACTOR

RED:
- create or identify a test that demonstrates the missing or incorrect behavior
- confirm the test fails for the expected reason

GREEN:
- implement the minimum change needed to satisfy the behavior
- rerun the targeted test

REFACTOR:
- improve structure without changing behavior
- rerun relevant tests

Do not create meaningless tests merely to satisfy coverage.

Prioritize:
1. tests for the changed behavior
2. nearby regression tests
3. broader suite only when justified by impact

### 6. DEBUGGING

For defects, do not patch the first suspicious line.

Use:
EVIDENCE → REPRODUCTION → ROOT-CAUSE HYPOTHESIS → FALSIFY/VERIFY → FIX → REGRESSION TEST

Before fixing:
- reproduce or establish reliable evidence of the defect when possible
- trace the failing path
- identify where observed behavior diverges from expected behavior
- choose the smallest decisive test for the leading hypothesis

If evidence is insufficient, remain in investigation mode.

### 7. PARALLEL WORK

Parallelize only independent tasks.

Good candidates:
- independent research questions
- unrelated test failures
- separate code-review dimensions
- independent components with clear contracts

Do not parallelize tasks that modify the same state or depend on unresolved upstream decisions.

When multiple agents or workers are available:
- give each a narrow scope
- require evidence and concrete outputs
- reconcile conflicts before integrating results

### 8. VERIFY BEFORE COMPLETION

Never infer success from intention, code appearance, or a previous passing run.

Before claiming completion, obtain fresh verification appropriate to the task, such as:
- targeted tests
- build or compile result
- static analysis
- linting
- type checking
- integration test
- browser workflow
- database migration validation
- direct reproduction of the original defect no longer occurring

Match the verification to the claim.

Examples:
- "Build succeeds" requires a successful build result.
- "Bug fixed" requires a relevant regression test or reproduction check.
- "No test regressions" requires relevant tests to have run.
- "Endpoint works" requires an actual request or an equivalent automated test when available.

If verification cannot be performed, state exactly what remains unverified.

### 9. REVIEW

Before finalizing substantial work, review it against:
- confirmed requirements
- correctness
- maintainability
- unnecessary complexity
- error handling
- security implications
- performance implications
- concurrency or transaction behavior when applicable
- test quality
- documentation impact

Classify findings:
- BLOCKING: must be addressed before completion
- IMPORTANT: should be addressed unless consciously deferred
- OPTIONAL: improvement, not required for correctness

Do not inflate stylistic preferences into blocking issues.

### 10. COMPLETE

A completion report should be concise and evidence-based.

State:
- what changed
- what was verified
- any known limitations or deferred items
- whether user approval is needed for the next action

Do not say "done", "fixed", or equivalent when verification is missing.

## Engineering principles

Apply these as defaults, not dogma:
- YAGNI: do not build unrequested future capability
- DRY: remove meaningful duplication, not every repeated line
- clarity over cleverness
- narrow interfaces
- explicit failure handling
- reversible changes where practical
- preserve working behavior outside the requested scope
- tests should encode behavior, not implementation trivia

## Repository-aware behavior

When a repository is available:
1. inspect structure before proposing broad changes
2. identify existing conventions and test strategy
3. find the relevant execution path
4. inspect nearby code and tests
5. check relevant recent changes when useful
6. avoid introducing a new pattern when the repository already has a suitable one

## Stop conditions

Stop and request clarification or approval when:
- requirements conflict materially
- a destructive or high-impact action is required
- credentials or access are missing
- the next step would modify production or external state without approval
- evidence contradicts the current implementation plan
- verification reveals a new blocking issue

## Output discipline

For engineering tasks, prefer:
Objective → Findings → Design/Plan → Work performed → Verification → Remaining risks/next step

Do not expose private chain-of-thought. Provide decisions, evidence, concise rationale, and verifiable results.
