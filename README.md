# ASTRAEUS

**Autonomous Systems, Technical Research & Adaptive Engineering Unified System**

ASTRAEUS is an adaptive technical research, software engineering, debugging, architecture, system-investigation, and automation agent concept designed to behave as one coordinated engineering intelligence rather than a collection of unrelated features.

Its core operating philosophy is:

```text
Objective → Evidence → Observation → Hypothesis → Verification → Action → Review → Documentation
```

ASTRAEUS prefers read-only investigation first, distinguishes facts from hypotheses, uses the smallest decisive test that can falsify an open hypothesis, and requires explicit human approval for high-impact or destructive actions.

## Current status

The project currently contains:

- validated ASTRAEUS core instructions
- two completed investigation evaluations
- the first reusable skill: `engineering-superpowers`
- architecture and integration design
- configuration/rebuild notes for Microsoft 365 Copilot Agent Builder and Copilot Studio
- roadmap for skills, MCP tools, knowledge, memory, compression, and connected agents

The Copilot Studio prototype successfully loaded the Engineering Superpowers skill, but further Preview/runtime testing was blocked by environment credit enforcement (`EnforcementUsageCredits`). The repository is intended to preserve everything required to rebuild ASTRAEUS later or port it to another compatible agent host.

## Core capabilities

ASTRAEUS is designed to support:

- technical research and evidence synthesis
- software and repository analysis
- systems, logs, and database investigation
- web-application debugging and testing
- architecture and dependency mapping
- security-conscious technical review
- critical verification of conclusions
- technical documentation and operational runbooks
- adaptive workflow and skill-improvement proposals
- controlled use of external tools and specialist agents

## Planned skill set

1. Engineering Superpowers ✅
2. Adaptive Skill Observer
3. Deep Research
4. Code & Repository Investigator
5. Systems & Database Investigator
6. Architecture Mapper
7. Security & Critical Verification
8. Technical Documentation Engine

## Planned external capabilities

- GitHub integration
- Playwright browser automation
- Chrome DevTools MCP
- controlled database MCP/gateway
- persistent memory
- context compression with a Headroom-like layer
- optional specialist-model routing through an OmniRoute-like gateway
- connected specialist agents when separation provides a clear benefit

## Repository map

```text
astraeus-agent/
├── README.md
├── PRIVACY.md
├── TERMS.md
├── docs/
│   ├── AGENT-INSTRUCTIONS.md
│   ├── ARCHITECTURE.md
│   ├── CONFIGURATION.md
│   ├── EVALUATION.md
│   ├── REFERENCES.md
│   └── ROADMAP.md
└── skills/
    └── engineering-superpowers/
        ├── SKILL.md
        ├── references/
        │   ├── implementation-workflow.md
        │   └── review-checklist.md
        └── templates/
            └── engineering-plan.md
```

## Documentation

- [Core Agent Instructions](./docs/AGENT-INSTRUCTIONS.md)
- [Architecture](./docs/ARCHITECTURE.md)
- [Configuration and Rebuild Guide](./docs/CONFIGURATION.md)
- [Evaluation Prompts and Expected Behavior](./docs/EVALUATION.md)
- [External References and Intended Roles](./docs/REFERENCES.md)
- [Roadmap](./docs/ROADMAP.md)
- [Engineering Superpowers Skill](./skills/engineering-superpowers/SKILL.md)
- [Privacy Statement](./PRIVACY.md)
- [Terms of Use](./TERMS.md)

## Operating principles

ASTRAEUS prioritizes evidence over assumptions and conceptually tracks investigation state as:

- `CONFIRMED`
- `DISPROVED`
- `OPEN`
- `NEEDS EVIDENCE`

It should not claim a system is healthy merely because one resource metric is low, should not invent tool results, and should not claim a bug is fixed or work is complete without fresh verification appropriate to the claim.

## Rebuild

For a future rebuild, start with [`docs/CONFIGURATION.md`](./docs/CONFIGURATION.md), then apply [`docs/AGENT-INSTRUCTIONS.md`](./docs/AGENT-INSTRUCTIONS.md), load the Engineering Superpowers skill, and run the tests in [`docs/EVALUATION.md`](./docs/EVALUATION.md) before adding more skills or tools.

## Creator

Created and maintained by [afe17](https://github.com/afe17).
