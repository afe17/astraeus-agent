# ASTRAEUS Roadmap

## Current state

The project has a validated core instruction set, an initial Engineering Superpowers skill, a documented architecture, and an initial evaluation suite.

The first host was Microsoft 365 Copilot Agent Builder. The project was then moved to the newer Copilot Studio agent experience to gain Skills, Tools, Connected Agents, and Memory. Further runtime testing was blocked by environment credit enforcement.

## Phase 1 — Core agent

Status: **completed / documented**

- [x] Define ASTRAEUS identity and mission
- [x] Define evidence-first investigation behavior
- [x] Define human-approval boundaries
- [x] Define repository/system/database/browser investigation principles
- [x] Define critical verification behavior
- [x] Define adaptive-improvement proposals
- [x] Create initial suggested prompts
- [x] Validate core behavior with two investigation tests

## Phase 2 — Skill layer

Status: **in progress**

### 1. Engineering Superpowers
Status: **created and successfully uploaded to Copilot Studio**

Purpose:
- requirements clarification
- design
- implementation planning
- test-first development
- debugging
- verification
- review
- completion discipline

### 2. Adaptive Skill Observer
Status: **planned**

Inspiration: `rebelytics/one-skill-to-rule-them-all`

Purpose:
- observe recurring workflows
- capture user corrections
- detect missing capabilities
- propose skill updates/new skills
- propose cross-cutting principles
- never silently mutate skills; require human review

### 3. Deep Research
Status: **planned**

Purpose:
- find authoritative sources
- compare contradictory evidence
- distinguish source-backed facts from assumptions
- synthesize technical research into engineering decisions

### 4. Code & Repository Investigator
Status: **planned**

Purpose:
- map repository structure
- identify languages/frameworks
- locate entry points/configuration
- trace call paths
- inspect tests and relevant history
- identify affected components before change recommendations

### 5. Systems & Database Investigator
Status: **planned**

Purpose:
- correlate logs, services, OS/runtime evidence, and SQL behavior
- PostgreSQL/SQL diagnostics
- targeted read-only queries
- locks, waits, connection pools, slow operations
- timelines and cross-layer correlation

### 6. Architecture Mapper
Status: **planned**

Purpose:
- components/services/interfaces
- protocols and dependencies
- data/control flows
- trust boundaries
- failure points
- architecture diagrams and topology documentation

### 7. Security & Critical Verification
Status: **planned**

Purpose:
- challenge unsupported conclusions
- inspect security implications
- test alternative explanations
- classify blocking/important/optional findings
- verify completion evidence

### 8. Technical Documentation Engine
Status: **planned**

Purpose:
- README files
- investigation/incident reports
- architecture docs
- implementation/test plans
- troubleshooting guides
- operational runbooks
- change summaries

## Phase 3 — Tool layer

Status: **planned**

### GitHub
Desired capabilities:
- repository search/read
- branches/commits
- issue/PR workflows
- CI status/logs
- controlled write operations behind approval where appropriate

### Playwright
Purpose:
- browser navigation
- user-flow automation
- form/login testing
- regression tests
- screenshots/traces

Source: `microsoft/playwright`

### Chrome DevTools MCP
Purpose:
- network inspection
- console/runtime errors
- performance traces
- request/response analysis
- browser debugging

Source: `ChromeDevTools/chrome-devtools-mcp`

### Database MCP / gateway
Initial policy:
- read-only access
- targeted queries
- explicit scope
- production writes require human approval

## Phase 4 — Knowledge layer

Status: **partially planned**

Potential sources:

- `codecrafters-io/build-your-own-x`
- `jaywcjlove/linux-command`
- Microsoft official documentation through web search
- project repositories
- internal files
- SharePoint / OneDrive documentation

Large repositories should not automatically be copied into a skill package. Prefer search/retrieval or curated references.

## Phase 5 — Context infrastructure

### Memory
Status: **native Copilot Studio Memory enabled in prototype; deeper design pending**

Inspiration: `thedotmack/claude-mem`

Goals:
- project continuity across sessions
- durable decisions/observations
- avoid repeated discovery
- scoped memory rather than uncontrolled accumulation

### Headroom
Status: **research/integration pending**

Source: `headroomlabs-ai/headroom`

Potential role:
- tool-output compression
- log/RAG/file compression
- retrieval of originals
- shared context infrastructure

Should be treated as infrastructure/tool/MCP, not a normal behavioral skill.

### OmniRoute
Status: **research/integration pending**

Source: `diegosouzapw/OmniRoute`

Potential role:
- external model gateway
- specialist model calls
- routing/fallback

It should not be assumed to replace the host agent's managed model. The safer design is to expose external-model calls as tools when the platform permits it.

## Phase 6 — Connected-agent architecture

Status: **deferred until single-agent + skills/tools is validated**

Potential specialist agents:

- Research Agent
- Repository/Code Agent
- Systems/Database Agent
- Browser QA Agent
- Security/Critic Agent
- Documentation Agent

The central ASTRAEUS agent remains the coordinator.

Connected agents should only be added when their separation provides measurable benefits in context isolation, parallelism, permissions, or specialization.

## Phase 7 — Evaluation and hardening

Planned evaluation categories:

- bias resistance
- root-cause investigation
- repository understanding
- code-change quality
- test discipline
- verification-before-completion
- tool selection
- memory quality
- context compression accuracy
- browser debugging
- database safety
- approval-boundary compliance
- hallucination/tool-failure handling

## Known blocker

Copilot Studio environment returned `EnforcementUsageCredits`, preventing additional Preview/runtime testing.

Revisit when:
- Copilot Credits are assigned to the environment, or
- a suitable pay-as-you-go/billing configuration exists, or
- ASTRAEUS is moved to another host supporting Agent Skills/MCP/tool integration.
