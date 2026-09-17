# Implementation Workflow Reference

Use this reference when the task is large enough to require a written implementation plan.

## Planning template

1. Objective
2. Confirmed requirements
3. Constraints
4. Existing-system findings
5. Chosen design
6. Alternatives rejected and why
7. Implementation steps
8. Tests/verification
9. Risks and rollback considerations
10. Approval gates

## Step quality

Each implementation step should ideally:
- affect a coherent behavior or component
- have a defined expected outcome
- include a verification method
- avoid bundling unrelated cleanup
- be reversible or reviewable before the next high-impact step

## Dependency ordering

Order work so that:
- prerequisite interfaces come before consumers
- schema/data changes account for compatibility
- tests can validate behavior as early as practical
- risky changes are isolated
- deployment or migration steps occur only after required approval
