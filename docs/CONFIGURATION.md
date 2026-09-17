# ASTRAEUS Configuration Snapshot

This document records the configuration used during the Microsoft 365 Copilot Agent Builder and Copilot Studio prototypes so the agent can be reconstructed later.

## Identity

**Name:** `ASTRAEUS`

**Expanded name:** `Autonomous Systems, Technical Research & Adaptive Engineering Unified System`

**Short description:**

> Adaptive technical research, engineering, debugging, architecture, and system investigation agent.

## Creator metadata

**Creator website:**

`https://github.com/afe17/astraeus-agent`

**Privacy statement:**

`https://github.com/afe17/astraeus-agent/blob/main/PRIVACY.md`

**Terms of use:**

`https://github.com/afe17/astraeus-agent/blob/main/TERMS.md`

## Core instructions

The complete core prompt is stored in:

- [`AGENT-INSTRUCTIONS.md`](./AGENT-INSTRUCTIONS.md)

The original Microsoft 365 Agent Builder instruction field had an 8,000-character limit, so the instruction set was compressed aggressively while preserving the operating principles.

## Microsoft 365 Agent Builder prototype

The initial prototype was built in Microsoft 365 Copilot Agent Builder.

Configuration used:

- Web search: enabled
- Knowledge URL candidates:
  - `https://github.com/codecrafters-io/build-your-own-x`
  - `https://jaywcjlove.github.io/linux-command`
- Microsoft documentation: intended to be retrieved through web search rather than consume a scarce public-URL knowledge slot
- project/internal documentation: planned for later file, SharePoint, or OneDrive ingestion

### Suggested prompts

#### Investigate a System

```text
Investigate this technical system systematically. Establish what we know, identify its architecture and dependencies, collect relevant evidence, generate and verify hypotheses, and tell me what we should investigate next.
```

#### Analyze a Repository

```text
Analyze this software repository as a senior engineer. Map its architecture, technologies, entry points, dependencies, important code paths, potential problems, tests, and documentation gaps before recommending changes.
```

#### Research & Engineer

```text
Research this technical objective deeply, compare the available approaches and evidence, then turn the findings into a practical engineering design and implementation plan.
```

#### Debug a Web Application

```text
Investigate this web application systematically. Reproduce the behavior when possible, inspect the user flow, browser network activity, console errors, application behavior, and relevant backend evidence. Correlate the findings before identifying likely root causes, and do not make changes until the evidence supports them.
```

#### Investigate Logs & Database

```text
Analyze these application logs and database evidence as a technical investigator. Establish a timeline, correlate errors and events with relevant queries and application behavior, identify supported hypotheses, reject unsupported explanations, and propose the safest next diagnostic steps.
```

#### Design System Architecture

```text
Design a technical architecture for this objective. Identify requirements, constraints, components, services, interfaces, data stores, dependencies, data flows, trust boundaries, failure modes, scalability concerns, and important design trade-offs before proposing the architecture.
```

#### Review an Implementation

```text
Review this implementation as a critical senior engineer. Check correctness, architecture, maintainability, security, error handling, testing, performance implications, unnecessary complexity, and consistency with the intended requirements. Separate confirmed problems from optional improvements.
```

#### Create Technical Documentation

```text
Turn the available technical information into clear, reusable documentation. Determine the appropriate format, preserve verified facts, explain architecture and operational behavior where relevant, document assumptions and limitations, and include actionable procedures or troubleshooting steps when useful.
```

## Copilot Studio prototype

ASTRAEUS was later recreated in the newer Copilot Studio agent experience.

Observed UI components:

- Model
- Skills
- Tools
- Knowledge
- Connected agents
- Memory (Preview)

Configuration at the point work stopped:

- **Model:** `GPT-5.6 Reasoning`
- **Skill loaded:** `engineering-superpowers`
- **Knowledge:** `Search all websites`
- **Memory:** enabled
- **Tools:** none configured yet
- **Connected agents:** none configured yet

The Skill upload initially failed because the YAML `description` contained special characters in an unquoted plain scalar. It was fixed by quoting `name` and using a folded block scalar (`>-`) for `description`.

## Billing blocker

The Copilot Studio prototype could not be tested further because the environment returned:

```text
You need credits to continue. Credits power building and running your agents and workflows.
This environment is out of credits. Contact your admin to add more credits.
Error code: EnforcementUsageCredits
```

This was an environment/Copilot Credits enforcement issue, not a failure in the ASTRAEUS prompt or skill package. The selected model can affect consumption, but zero available environment credits prevents Preview/runtime regardless of model choice.

## Rebuild order

When a suitable host/environment is available again:

1. Create `ASTRAEUS`.
2. Apply [`AGENT-INSTRUCTIONS.md`](./AGENT-INSTRUCTIONS.md).
3. Enable web search / appropriate knowledge retrieval.
4. Add Engineering Superpowers.
5. Run the stored evaluation prompts in [`EVALUATION.md`](./EVALUATION.md).
6. Add remaining skills one at a time and test each trigger.
7. Add GitHub and browser tools.
8. Add database access in read-only mode first.
9. Evaluate persistent memory/context compression options.
10. Add connected specialist agents only when orchestration benefits are demonstrated.
