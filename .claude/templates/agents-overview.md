# Agents Overview

The Agentic Substrate provides **17 specialized agents** that work together across the complete software development lifecycle:

---

## TIER 1: ORCHESTRATION (1 agent)

### 1. chief-architect
**Purpose**: Master orchestrator for complex, multi-faceted projects

**Use when**: Project requires 3+ distinct capabilities or spans multiple domains

**Example**: "Build complete user authentication system with email verification and password reset"

**What it does**:
- Analyzes requirements and decomposes into specialized tasks
- Selects optimal team of specialist agents
- Manages dependencies and handoffs between agents
- Synthesizes results into cohesive deliverables
- Coordinates parallel agent execution (90.2% performance improvement on complex tasks)

**Think Protocol**: Uses "ultrathink" for critical architecture decomposition

**Best For**: Multi-step features, cross-domain tasks, uncertain scope

---

## TIER 2: CORE WORKFLOW (5 agents - Research → Plan → Analyze → Implement → Debug)

### 2. docs-researcher
**Purpose**: High-speed documentation specialist

**Use when**: Implementing features with external libraries or APIs

**Example**: "Research Redis caching best practices for Node.js"

**What it does**:
- Fetches version-accurate docs from official sources
- Prevents coding from potentially stale memory
- Delivers ResearchPack in < 2 minutes
- Uses contextual retrieval for 49-67% better accuracy
- Auto-invokes research-methodology skill

**Think Protocol**: Uses "ultrathink" for complex API landscape analysis

**Quality Gate**: ResearchPack must score ≥ 80 before proceeding to planning

---

### 3. implementation-planner
**Purpose**: Strategic architect for minimal-change, reversible plans

**Use when**: ResearchPack ready and implementation needs planning

**Example**: "Create implementation plan for Redis caching integration"

**What it does**:
- Transforms ResearchPacks into executable blueprints
- Identifies minimal changes required (surgical edits only)
- Creates step-by-step plans with rollback procedures
- Ensures no API hallucination (matches ResearchPack exactly)
- Auto-invokes planning-methodology skill

**Think Protocol**: Uses "ultrathink" for critical architecture decisions

**Quality Gate**: Implementation Plan must score ≥ 85 before proceeding to analysis

---

### 4. brahma-analyzer
**Purpose**: Cross-artifact consistency and coverage analysis specialist

**Use when**: Before implementation to catch conflicts early

**Example**: "Analyze plan consistency with research and detect conflicts"

**What it does**:
- Validates alignment between specifications, plans, tasks, and implementation
- Detects gaps in coverage (spec → plan → tasks)
- Identifies conflicts before coding begins
- Ensures traceability and completeness
- Multi-modal quality scoring (80+ required for pass)

**Think Protocol**: Uses extended thinking for complex conflict resolution

**Quality Gate**: Analysis must pass (80+ score) before implementation

**Tools**: Read, Grep, Glob, Write, TodoWrite

---

### 5. code-implementer
**Purpose**: Precision execution specialist with TDD enforcement

**Use when**: Both ResearchPack AND Implementation Plan are ready (and analysis passed)

**Example**: "Implement the caching plan"

**What it does**:
- Executes plans with surgical precision (minimal changes only)
- Enforces TDD: RED (write failing test) → GREEN (make it pass) → REFACTOR (improve quality)
- Self-corrects with 3 intelligent retries + circuit breaker
- Creates git commits with co-author attribution
- Validates against Implementation Plan

**Think Protocol**: Uses "ultrathink" for critical self-correction decisions

**Quality Gate**: All tests must pass before completion

**Circuit Breaker**: Opens after 3 failed attempts (requires manual intervention)

---

### 6. brahma-investigator
**Purpose**: Root cause analysis and debugging specialist

**Use when**: Complex bugs, production incidents, system failures

**Example**: "Investigate why database connections are timing out"

**What it does**:
- Systematic root cause analysis (not surface fixes)
- Error pattern recognition
- Performance issue diagnosis
- Integration failure investigation
- Limited retries (3 max) with think protocol
- Documents patterns for knowledge preservation

**Think Protocol**: Progressive modes based on complexity
- **think** (30-60s): Routine bugs with clear error messages
- **think hard** (1-2min): Multi-component failures
- **think harder** (2-4min): Production incidents, novel failures

**Tools**: Read, Grep, Glob, Bash, TodoWrite

---

## TIER 3: CODE QUALITY (5 agents - Review → Test → Refactor → Security → PR Feedback)

### 7. code-reviewer
**Purpose**: Code review specialist for quality, security, and best practices

**Use when**: Before commits, for PR reviews, wanting a second opinion

**Example**: "Review the authentication changes before merging"

**What it does**:
- Systematic review by priority (security → correctness → performance → maintainability)
- OWASP Top 10 security checklist for sensitive code
- Provides actionable suggestions with concrete fixes
- Acknowledges good code, not just problems
- Clear APPROVE / REQUEST CHANGES / BLOCK decisions

**Think Protocol**:
- **think**: Simple function reviews
- **think hard**: Complex logic, architectural concerns
- **think harder**: Security vulnerabilities, race conditions

**Command**: `/review`

**Tools**: Read, Grep, Glob, Bash, TodoWrite

---

### 8. test-generator
**Purpose**: Comprehensive test suite generation

**Use when**: Need tests for existing code, improving coverage, TDD support

**Example**: "Generate tests for the UserService class"

**What it does**:
- Generates unit tests (isolated, fast)
- Creates integration tests (component interaction)
- Covers edge cases (boundaries, errors, null handling)
- Uses AAA pattern (Arrange-Act-Assert)
- Runs generated tests to verify they work

**Think Protocol**:
- **think**: Simple function tests
- **think hard**: Complex state, async flows
- **think harder**: Integration tests, mocking strategies

**Command**: `/test`

**Tools**: Read, Grep, Glob, Bash, Write, TodoWrite

---

### 9. security-auditor
**Purpose**: Security scanning and vulnerability assessment

**Use when**: Security audits, pre-deployment checks, vulnerability assessment

**Example**: "Audit the application for security vulnerabilities"

**What it does**:
- OWASP Top 10 compliance checking
- Dependency vulnerability scanning (CVEs)
- Secrets detection (API keys, credentials)
- Security header verification
- Remediation guidance with severity ratings

**Think Protocol**:
- **think**: Common vulnerability patterns
- **think hard**: Complex attack vectors
- **think harder**: Cryptographic issues, auth flows

**Command**: `/audit`

**Tools**: Read, Grep, Glob, Bash, WebFetch, TodoWrite

---

### 10. refactoring-specialist
**Purpose**: Safe, incremental code improvement

**Use when**: Reducing technical debt, improving code quality without changing behavior

**Example**: "Refactor the payment service to reduce complexity"

**What it does**:
- Detects code smells (bloaters, couplers, dispensables)
- Applies refactoring techniques (Extract Method, Extract Class, etc.)
- Preserves behavior through test verification
- Commits each change separately for easy rollback
- Provides before/after metrics

**Think Protocol**:
- **think**: Simple renames, extractions
- **think hard**: Design pattern application
- **think harder**: Architecture changes

**Command**: `/refactor`

**Tools**: Read, Grep, Glob, Bash, Edit, Write, TodoWrite

---

### 11. pr-feedback-analyst
**Purpose**: GitHub PR feedback triage and action planning

**Use when**: PR has comments from Copilot, reviewers, or bots that need analysis

**Example**: "Analyze Copilot suggestions on this PR and create a plan"

**What it does**:
- Fetches ALL PR comments (Copilot, humans, CI bots)
- Validates each suggestion against the actual codebase
- Distinguishes valid suggestions from false positives
- Explains why invalid suggestions should be ignored
- Creates prioritized implementation plan for valid feedback

**Think Protocol**:
- **think**: Simple lint/style suggestions
- **think hard**: Conflicting suggestions, architectural feedback
- **think harder**: Security-related feedback, major refactoring suggestions

**Command**: `/pr-feedback`

**Tools**: Read, Grep, Glob, Bash, TodoWrite

**Trust Calibration**:
- Copilot security suggestions: HIGH trust
- Copilot null checks: MEDIUM trust (verify nullability)
- Copilot style/refactoring: LOW trust (check project conventions)

---

## TIER 4: INFRASTRUCTURE (3 agents - Migrate → Dependencies → API Design)

### 12. migration-specialist
**Purpose**: Database, API, and dependency migrations

**Use when**: Schema changes, version upgrades, platform migrations

**Example**: "Migrate the database from MySQL to PostgreSQL"

**What it does**:
- Database schema migrations (add/modify/remove)
- Data migrations and transformations
- API version upgrades
- Dependency major version upgrades
- Zero-downtime migration strategies
- Comprehensive rollback plans

**Think Protocol**:
- **think**: Simple schema additions
- **think hard**: Data transformations
- **think harder**: Breaking changes, zero-downtime planning

**Command**: `/migrate`

**Tools**: Read, Grep, Glob, Bash, Write, Edit, WebFetch, TodoWrite

---

### 13. dependency-manager
**Purpose**: Package management and security compliance

**Use when**: Updating dependencies, resolving conflicts, security patching

**Example**: "Update all dependencies and fix security vulnerabilities"

**What it does**:
- Audits all dependencies (outdated, vulnerable, unused)
- Analyzes changelogs for breaking changes
- Resolves version conflicts
- Plans safe update strategies by risk level
- Provides dependency health scores

**Think Protocol**:
- **think**: Patch updates, security fixes
- **think hard**: Minor version updates
- **think harder**: Major version updates, conflicts

**Tools**: Read, Grep, Glob, Bash, WebFetch, Write, TodoWrite

---

### 14. api-designer
**Purpose**: API design and documentation specialist

**Use when**: Designing new APIs, improving existing ones, generating specs

**Example**: "Design a REST API for the order management system"

**What it does**:
- Designs REST and GraphQL APIs
- Generates OpenAPI 3.0 specifications
- Plans versioning strategies
- Creates comprehensive documentation
- Follows best practices and conventions

**Think Protocol**:
- **think**: Simple endpoint design
- **think hard**: Resource relationships, pagination
- **think harder**: Versioning strategy, breaking changes

**Tools**: Read, Grep, Glob, Write, WebFetch, TodoWrite

---

## TIER 5: PRODUCTION DEPLOYMENT (3 agents - Deploy → Monitor → Optimize)

### 15. brahma-deployer
**Purpose**: Production deployment specialist with safety-first patterns

**Use when**: Deploying to production, managing releases

**Example**: "Deploy v2.5.0 to production with canary rollout"

**What it does**:
- Safe, incremental, validated deployments
- Defaults to canary releases (5% → 25% → 50% → 100%)
- Automatic rollback on failures (error rate >1%, latency >500ms)
- Blue-green deployment coordination
- CI/CD pipeline management
- Infrastructure as Code (IaC) provisioning

**Think Protocol**: Analyzes risk, rollback strategy, metrics before deploying

**Safety Patterns**:
- Progressive exposure with observation windows
- Feature flags (deploy dark, enable gradually)
- Monitoring integration (never deploy without observability)

**Tools**: Bash, Read, Write, Grep, TodoWrite, WebFetch

---

### 16. brahma-monitor
**Purpose**: Observability and monitoring specialist

**Use when**: Setting up observability, tracking SLI/SLO, incident detection

**Example**: "Set up comprehensive monitoring for user service"

**What it does**:
- Implements Anthropic's three pillars pattern (Metrics, Logs, Traces)
- SLI/SLO tracking and alerting
- Proactive incident detection
- Runbook automation
- Performance metrics collection
- Business metrics integration

**Think Protocol**: Designs observability strategy before implementation

**Three Pillars**:
1. **Metrics**: Time-series data (latency, error rate, throughput)
2. **Logs**: Structured event logging
3. **Traces**: Distributed request tracing

**Tools**: Bash, Read, Write, WebFetch, TodoWrite

---

### 17. brahma-optimizer
**Purpose**: Performance optimization and auto-scaling specialist

**Use when**: Performance issues, scaling challenges, cost optimization

**Example**: "Optimize API latency and set up auto-scaling"

**What it does**:
- Performance profiling with Anthropic patterns
- Horizontal/vertical scaling strategies
- Load balancing optimization
- Caching strategies (Redis, CDN, application-level)
- Database query optimization
- Continuous performance tuning

**Think Protocol**: Profiles before optimizing, measures impact

**Optimization Patterns**:
- Identify bottlenecks (profiling, tracing)
- Apply targeted optimizations (avoid premature optimization)
- Measure impact (before/after benchmarks)
- Auto-scaling configuration

**Tools**: Bash, Read, Write, Grep, TodoWrite, WebFetch

---

## WORKFLOW PATTERNS

### Complete Automation (Recommended)
```bash
/workflow Add Redis caching to ProductService
```
**Sequence**: research → plan → analyze → implement → (review → test → deploy → monitor → optimize)

### Step-by-Step Control
```bash
/research Redis for Node.js v5.0
/plan Redis caching for ProductService
/implement
/review
/test
```

### Direct Agent Invocation
```bash
@chief-architect Build complete payment processing system
@docs-researcher Research Stripe API v2023-10-16
@implementation-planner Plan integration of Stripe webhooks
@code-implementer Execute payment integration plan
@code-reviewer Review the implementation
@test-generator Generate tests for payment service
@security-auditor Audit payment code for vulnerabilities
@brahma-deployer Deploy to production with canary
@brahma-monitor Set up observability for payment service
@brahma-optimizer Optimize payment processing latency
```

### Quality-Focused Workflow
```bash
/review src/services/          # Review code first
/test src/services/            # Generate missing tests
/audit                         # Security audit
/refactor src/services/        # Improve code quality
```

---

## COMMAND QUICK REFERENCE

| Command | Agent | Purpose |
|---------|-------|---------|
| `/workflow` | chief-architect | Complete automation |
| `/research` | docs-researcher | Documentation research |
| `/plan` | implementation-planner | Create implementation plan |
| `/implement` | code-implementer | Execute plan |
| `/review` | code-reviewer | Code review |
| `/test` | test-generator | Generate tests |
| `/audit` | security-auditor | Security audit |
| `/refactor` | refactoring-specialist | Code refactoring |
| `/debug` | brahma-investigator | Debugging |
| `/migrate` | migration-specialist | Migrations |
| `/pr-feedback` | pr-feedback-analyst | Analyze PR comments |
| `/context` | - | Context management |

---

## AGENT COORDINATION

### Multi-Agent Orchestration (Anthropic Research 2024)

**Performance**: 90.2% improvement on complex tasks using parallel subagents

**Pattern**: Lead orchestrator + parallel specialized workers
- **Lead**: chief-architect (Claude Opus 4) - plans and coordinates
- **Workers**: Specialist agents (Claude Sonnet 4) - execute in parallel

**Key Challenge**: Without detailed task descriptions, agents duplicate work or leave gaps

**Solution**: Explicit objectives, output formats, tool guidance, clear boundaries per agent

### Quality Gates (Automatic)

**Research → Planning**:
- ✅ ResearchPack score ≥ 80
- ✅ Library version identified
- ✅ Minimum 3 APIs documented
- ✅ Code examples present
- ⛔ Blocks planning if fails

**Planning → Analysis**:
- ✅ Plan score ≥ 85
- ✅ Rollback plan present
- ✅ Risk assessment complete
- ⛔ Blocks analysis if fails

**Analysis → Implementation**:
- ✅ Analysis score ≥ 80
- ✅ No conflicts detected
- ✅ Coverage complete
- ⛔ Blocks implementation if fails

**Implementation → Completion**:
- ✅ All tests passing
- ✅ Circuit breaker closed
- ✅ Build successful
- ⛔ Up to 3 self-corrections, then blocks

---

## PERFORMANCE BENCHMARKS

From Anthropic research and Agentic Substrate testing:

**Accuracy**:
- Research: +49-67% with contextual retrieval
- Multi-agent: +90.2% on complex tasks
- Extended thinking: +54% on complex problems

**Speed**:
- Research: < 2 min (version-accurate docs)
- Planning: < 3 min (with think protocol)
- Implementation: 5-25 min (TDD enforced)
- **Total**: 10-30 min for production-ready features

**Quality**:
- API hallucination: 0% (validated against ResearchPack)
- Test coverage: 80%+ (TDD mandatory)
- Circuit breaker: Prevents infinite loops

---

## EXTENDED THINKING PROTOCOLS

All agents support extended thinking modes:

- **"think"** (30-60s): Routine planning, standard decisions
- **"think hard"** (1-2min): Multiple valid approaches, unclear tradeoffs
- **"think harder"** (2-4min): Novel problems, high-stakes decisions
- **"ultrathink"** (5-10min): Critical architecture, multi-agent coordination

**Performance**: 54% improvement on complex tasks (Anthropic research)

**Auto-triggered for**:
- Complex tool operations (irreversible effects)
- Long chains of tool outputs
- Sequential decisions where mistakes are costly
- Multiple valid approaches with unclear tradeoffs

---

**Updated**: 2025-12-31 (V4.3 - Added pr-feedback-analyst agent)
**Agent Count**: 17 (was 16)
**Command Count**: 12 (was 11)
