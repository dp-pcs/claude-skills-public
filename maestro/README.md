# Maestro - Parallel Multi-Agent Execution

> Transform complex deployment plans into coordinated parallel execution using Claude Code sub-agents.

## What is This?

Maestro is a Claude Code skill that reads complex implementation plans (like database migrations, API changes, or feature rollouts) and automatically:

1. **Analyzes** the plan for parallelizable work
2. **Spawns** specialized sub-agents for each work stream
3. **Coordinates** dependencies and handoffs between agents
4. **Validates** integration at each phase
5. **Manages** merges to avoid conflicts

## When to Use

Perfect for:
- **Large feature implementations** (50+ files, multiple components)
- **Database migrations** with service layer changes
- **API refactors** touching many endpoints
- **Performance optimizations** across layers
- **Security updates** requiring validation pipelines

Not needed for:
- Single-file changes
- Simple bug fixes
- Documentation updates

## How It Works

### Input

Provide a deployment plan (Markdown document) with:
- **Phases**: What needs to be implemented
- **Files**: Which files will be created/modified
- **Dependencies**: What depends on what
- **Critical fixes**: Any specific requirements (from code reviews, security audits, etc.)

Example plan structure:
```markdown
# Implementation Plan: Feature X

## Phase 0: Pre-Implementation
- Database backup
- Baseline metrics

## Phase 1: Database Migration
Files: alembic/versions/xxx.py, app/services/migration_helpers.py

## Phase 2: Models & Services
Files: app/models/*.py, app/services/*.py
Dependencies: Needs Phase 1 complete

## Phase 3: API Layer
Files: app/routers/*.py
Dependencies: Needs Phase 2 complete
...
```

### Output

The orchestrator spawns sub-agents in **dependency-aware waves**:

```
Wave 1 (Parallel):
  🗄️ Database Migration Agent
  📋 Model & Schema Agent
  🧪 Testing Agent (baseline)

Wave 2 (Parallel, after Wave 1):
  🔒 Validation & Security Agent
  ⚙️ Service Layer Agent
  🎯 Pipeline & Queue Agent

Wave 3 (Sequential, after Wave 2):
  🌐 API & Router Agent

Wave 4 (Parallel, final validation):
  🧪 Integration Tests
  🧪 Load Tests
  🧪 Monitoring Setup
```

Each agent:
- Works on its own files (no conflicts)
- Creates a `COMPLETION.md` when done
- Produces testable, mergeable code

## Example Usage

```bash
# In your project with a deployment plan
User: I want to implement the plan at ~/.claude/plans/my-feature-plan.md

Deployment Orchestrator:
Reading plan...
Identified 7 work streams, 67 files
Recommended: 4 waves, 3-4 agents per wave
Estimated: 2-3 hours total

Wave 1: Migration + Models + Testing
Ready to spawn 3 agents in parallel? (yes/no)

User: yes

Orchestrator:
✅ Migration Agent spawned
✅ Models Agent spawned
✅ Testing Agent spawned

Monitoring progress...
[45 minutes later]

Wave 1 Complete:
✅ Migration: 5 files created, validated
✅ Models: 8 files created, imports working
✅ Testing: Baseline metrics collected

Wave 2: Validation + Services + Pipeline
Spawning 3 agents...
```

## Sub-Agent Specializations

### 🗄️ Database Migration Agent
- Creates Alembic migration scripts
- Implements bulk operations
- Adds validation and row checks
- Creates downgrade scripts

**Completion**: `MIGRATION_COMPLETE.md` with validation results

### 📋 Model & Schema Agent
- Creates SQLAlchemy models
- Defines relationships
- Creates Pydantic schemas

**Completion**: `MODELS_COMPLETE.md` with API contracts

### 🔒 Validation & Security Agent
- Builds security scanners
- Implements semantic validation
- Creates entity mappers

**Completion**: `VALIDATION_COMPLETE.md` with test examples

### ⚙️ Service Layer Agent
- Builds business logic
- Integrates validators
- Implements patterns

**Completion**: `SERVICES_COMPLETE.md` with interfaces

### 🎯 Pipeline & Queue Agent
- Builds processing queues
- Implements retry logic
- Creates pipelines

**Completion**: `PIPELINE_COMPLETE.md` with metrics

### 🌐 API & Router Agent
- Creates FastAPI routers
- Implements endpoints
- Adds validation

**Completion**: `API_COMPLETE.md` with endpoint docs

### 🧪 Testing & Monitoring Agent
- Creates unit/integration tests
- Builds load tests
- Sets up monitoring

**Completion**: `TESTS_COMPLETE.md` with coverage

## Conflict Avoidance

### File Ownership
- One agent per file
- Declared upfront
- No cross-editing

### Dependency Management
- Explicit wave structure
- Completion markers between waves
- Interface contracts documented

### Merge Strategy
- Agents work in branches
- Merge in dependency order
- Orchestrator resolves conflicts

## Example Plan

See the included [example plan](../parallel-agents-strategy.md) based on a real deployment (document processing use cases) with:
- 7 phases
- 67 files
- 9 critical fixes from code review
- Database migration + service layer + API changes

The orchestrator analyzes this and creates a 4-wave parallel execution strategy, reducing implementation time from ~1 week sequential to ~3 hours parallel.

## Token Usage

Running multiple agents in parallel uses significant tokens:

**Typical Usage**:
- Wave 1: 450K tokens (3 agents × 150K avg)
- Wave 2: 600K tokens (3 agents × 200K avg)
- Wave 3: 200K tokens (1 agent × 200K)
- **Total**: ~1.25M tokens (~$15 with Sonnet 4)

**Cost Optimization**:
- Use Haiku for simpler agents
- Sequential for budget constraints
- Hybrid: critical path parallel, others sequential

## Limitations

- **Maximum 10 parallel agents** (Claude Code limit)
- **Requires clear plan** - orchestrator can't invent requirements
- **No cross-agent collaboration** - agents work independently
- **Manual conflict resolution** may be needed for shared files
- **Token intensive** - parallel execution uses more tokens than sequential

## Best Practices

1. **Start with clear plan**: More detail = better orchestration
2. **Identify dependencies upfront**: Helps wave planning
3. **Use completion markers**: Enables clean handoffs
4. **Validate each wave**: Don't proceed if integration fails
5. **Review before merging**: Orchestrator shows diffs, you approve
6. **Monitor token usage**: Know your budget
7. **Test incrementally**: Don't wait until the end

## Files

- `SKILL.md` - Skill definition and orchestration logic
- `README.md` - This file
- `../parallel-agents-strategy.md` - Detailed strategy document

## Author

David Proctor - AI CoE

## Version

1.0.0

## Sources

Based on:
- [Claude Code Sub-Agents Documentation](https://code.claude.com/docs/en/sub-agents)
- [Parallel Development with Sub-Agents](https://zachwills.net/how-to-use-claude-code-subagents-to-parallelize-development/)
- [Multi-Agent Parallel Coding](https://medium.com/@codecentrevibe/claude-code-multi-agent-parallel-coding-83271c4675fa)
