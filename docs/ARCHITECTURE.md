# ASTRAEUS Architecture

## Vision

ASTRAEUS is intended to be a personal technical-agent operating system rather than a single-purpose chatbot. The design combines a central orchestrator with reusable skills, trusted knowledge, external tools/MCP servers, persistent memory, context-management infrastructure, and explicit human approval for high-impact actions.

## Logical architecture

```text
                         USER
                          |
                          v
                 +------------------+
                 | ASTRAEUS COMMAND |
                 |   ORCHESTRATOR   |
                 +---------+--------+
                           |
          +----------------+----------------+
          |                |                |
          v                v                v
       SKILLS           KNOWLEDGE          TOOLS
          |                |                |
  Engineering         Web search        GitHub
  Research            Build Your X      Playwright
  Repository          Linux Command     Chrome DevTools
  Systems/DB          Project docs      Database MCP
  Architecture        Internal docs     APIs/connectors
  Verification
  Documentation
  Skill Observer
          |                |                |
          +----------------+----------------+
                           |
                           v
                 CONTEXT INFRASTRUCTURE
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
          Memory       Compression    Model Gateway
                        (Headroom)     (OmniRoute)
             |             |             |
             +-------------+-------------+
                           |
                           v
                    VERIFICATION
                           |
                           v
                  HUMAN APPROVAL GATE
                           |
                           v
                        RESULT
```

## Core behavior

ASTRAEUS should operate using an evidence-first cycle:

```text
Objective
  -> establish known facts
  -> collect minimal decisive evidence
  -> form hypotheses
  -> falsify/verify hypotheses
  -> perform work
  -> verify result
  -> critically review
  -> document outcome
```

Investigation state is tracked conceptually as:

- `CONFIRMED` — directly supported by evidence
- `DISPROVED` — contradicted by evidence or a decisive test
- `OPEN` — plausible but unresolved
- `NEEDS EVIDENCE` — cannot be assessed yet

## Skill layer

Planned skill set:

1. **Engineering Superpowers** — requirements, design, planning, implementation, TDD, debugging, review, verification.
2. **Adaptive Skill Observer** — detect recurring workflows, user corrections, gaps, and propose skill improvements.
3. **Deep Research** — source discovery, evidence synthesis, contradiction handling, primary-source preference.
4. **Code & Repository Investigator** — repository mapping, entry points, dependencies, code paths, tests, change analysis.
5. **Systems & Database Investigator** — logs, services, OS, runtime behavior, SQL/PostgreSQL, targeted read-only diagnostics.
6. **Architecture Mapper** — components, interfaces, data/control flows, trust boundaries, failure points.
7. **Security & Critical Verification** — challenge conclusions, verify evidence, review security and operational risk.
8. **Technical Documentation Engine** — README, investigation reports, architecture docs, runbooks, change summaries.

## Knowledge layer

Initial knowledge sources discussed:

- CodeCrafters `build-your-own-x`
- `jaywcjlove/linux-command`
- Microsoft documentation through web search
- project-specific files
- SharePoint/OneDrive/internal documentation when available

Knowledge is distinct from skills. Knowledge provides facts/reference material; skills define how ASTRAEUS works.

## Tool / MCP layer

Planned tools:

### Playwright
Browser automation and functional testing:
- navigation
- forms
- login flows
- regression tests
- screenshots/traces

### Chrome DevTools MCP
Browser diagnostics:
- network requests
- console errors
- runtime inspection
- performance traces
- request/response analysis

### GitHub
Repository operations:
- source inspection
- commits
- issues
- pull requests
- CI/workflows

### Database gateway / MCP
Controlled database diagnostics and, only with explicit approval, authorized changes.

Read-only investigation should be the default.

## Context infrastructure

### Persistent memory

Original inspiration: `thedotmack/claude-mem`.

Desired behavior:
- preserve project decisions across sessions
- retain useful observations
- avoid repeatedly rediscovering the same facts
- separate durable project memory from transient conversation context

Copilot Studio's native Memory preview was enabled during the prototype.

### Context compression

Original inspiration: `headroomlabs-ai/headroom`.

Desired behavior:
- compress large logs, tool outputs, RAG chunks, and files
- preserve critical evidence
- retain a retrieval path to original material
- reduce irrelevant context pressure

### Model gateway

Original inspiration: `diegosouzapw/OmniRoute`.

Desired role is an optional external specialist-model tool, not a replacement for the host agent model.

Example:

```text
ASTRAEUS host model
      |
      +--> external model tool / gateway
                 |
                 +--> specialist model A
                 +--> specialist model B
                 +--> low-cost classifier
```

## Human approval boundary

Explicit approval should be required before high-impact actions such as:

- deleting data
- altering production databases
- deleting branches/repositories
- production deployments
- access-control changes
- sending external messages/emails
- irreversible infrastructure changes
- destructive operating-system commands

Investigation, planning, simulation, command generation, and read-only inspection may proceed without destructive action.

## Design principle

ASTRAEUS should behave as one coordinated engineering intelligence. Skills, tools, knowledge, memory, and connected agents are implementation layers behind a unified interface rather than separate personalities competing for control.
