# External References and Intended Roles

This project draws inspiration from several open-source projects. They are not all "skills" and should not all be integrated in the same way.

## Behavioral / methodology sources

### obra/superpowers
Repository: `https://github.com/obra/superpowers`

Role: software-engineering methodology for coding agents.

Useful concepts incorporated into ASTRAEUS:
- brainstorming before implementation
- written implementation plans
- test-driven development
- systematic debugging
- verification before completion
- code review discipline
- subagent/parallel work for independent tasks

ASTRAEUS uses an adapted `engineering-superpowers` skill rather than copying the entire plugin/harness structure.

### rebelytics/one-skill-to-rule-them-all
Repository: `https://github.com/rebelytics/one-skill-to-rule-them-all`

Role: meta-skill / task observer.

Planned ASTRAEUS use:
- detect repeated workflows
- observe user corrections and steering
- identify gaps in the current skill library
- propose new skills or skill changes
- retain human review before persistent changes

## Memory / context infrastructure

### thedotmack/claude-mem
Repository: `https://github.com/thedotmack/claude-mem`

Role: persistent memory/context continuity across sessions.

Planned ASTRAEUS use is architectural inspiration rather than direct Claude-specific hook reuse.

Desired capabilities:
- preserve project decisions and useful observations
- retrieve relevant history in later sessions
- summarize durable context
- avoid repeating investigations already completed

### headroomlabs-ai/headroom
Repository: `https://github.com/headroomlabs-ai/headroom`

Role: context compression and retrieval infrastructure.

Potential ASTRAEUS role:
- compress large tool outputs
- compress logs/RAG/file content
- retain original content for retrieval
- reduce model-context pressure
- optionally provide MCP/context infrastructure

Treat as infrastructure/tooling, not as one of the eight behavioral skills.

## Model routing / gateway

### diegosouzapw/OmniRoute
Repository: `https://github.com/diegosouzapw/OmniRoute`

Role: model gateway/router.

Potential ASTRAEUS role:
- optional specialist-model tool
- external model routing/fallback
- cost/availability-aware calls

Do not assume it can replace the managed host model inside Copilot Studio. Prefer exposing it as an external tool/gateway where supported.

## Engineering knowledge

### codecrafters-io/build-your-own-x
Repository: `https://github.com/codecrafters-io/build-your-own-x`

Role: curated engineering learning/reference index covering systems such as databases, operating systems, Docker, Git, web servers, search engines, programming languages, and network stacks.

Planned ASTRAEUS role: knowledge/reference source, not a behavioral skill.

### jaywcjlove/linux-command
Repository: `https://github.com/jaywcjlove/linux-command`

Documentation site: `https://jaywcjlove.github.io/linux-command`

Role: Linux command reference.

Planned ASTRAEUS role: searchable knowledge/retrieval source. Avoid copying the entire repository into a skill package.

## Browser tools

### ChromeDevTools/chrome-devtools-mcp
Repository: `https://github.com/ChromeDevTools/chrome-devtools-mcp`

Role: browser inspection/debugging through MCP.

Desired capabilities:
- performance traces
- network analysis
- console inspection
- runtime/client-side debugging
- screenshots and browser inspection

Security note: browser sessions can expose sensitive information. Use isolated profiles/sessions and least privilege where possible.

### microsoft/playwright
Repository: `https://github.com/microsoft/playwright`

Role: browser automation and testing.

Desired capabilities:
- functional browser flows
- navigation and form interaction
- end-to-end regression tests
- screenshots/traces
- browser-based verification

Playwright and Chrome DevTools are complementary:

```text
Playwright       -> user-flow automation / functional testing
Chrome DevTools  -> network/runtime/performance debugging
```

## Integration rule

Before adding any external project, classify it first:

- **Skill** — how ASTRAEUS should perform a type of work
- **Knowledge** — reference information ASTRAEUS can retrieve
- **Tool/MCP** — an external capability or action surface
- **Infrastructure** — memory, compression, routing, observability
- **Connected agent** — an independently scoped specialist agent

This separation is important to avoid wasting skill slots, bloating context, or creating conflicting behaviors.
