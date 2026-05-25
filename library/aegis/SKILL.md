---
name: aegis
description: "The master orchestrator for autonomous development. Activates when building a product from idea to production, managing multi-gate workflows, or when the user says 'build', 'create project', 'aegis mode', 'full lifecycle', or 'idea to deployment'. Coordinates all expert skills through the 5-Gate workflow."
category: orchestrator
version: "2.0.0"
author: "Krish Ujeniya"
---

# Aegis: Autonomous Development Orchestrator

> **Author**: Krish Ujeniya
>
> Aegis transforms ideas into production-grade software through a disciplined 5-Gate workflow. It coordinates expert agents (PM, Architect, Engineer, DevOps, QA) using filesystem-based state persistence, token-efficient codebase understanding, and human-in-the-loop guardrails only where legally or personally required.

## When to Activate

Trigger when detecting:
- **New project** — "build", "create", "start project", "new app"
- **Full lifecycle** — "idea to production", "end to end", "full stack"
- **Aegis mode** — "aegis", "5-gate", "autonomous build"
- **Team coordination** — "orchestrate experts", "multi-agent build"

## Core Principles

1. **Skills-First**: Every action invokes a specialized skill — never freestyle
2. **Filesystem Persistence**: All state in `.sovereign/` — survives crashes and token limits
3. **Token Efficiency**: Use AST packing, not file reading — understand codebases in O(1)
4. **Progressive Disclosure**: Load gate protocols JIT from `references/` — not upfront
5. **HITL Guardrails**: Human approval ONLY for: legal, financial, personal data, and production deployments

## The 5-Gate Workflow

```
IDEA → [GATE 1: UNDERSTAND] → [GATE 2: ANALYZE] → [GATE 3: PLAN] → [GATE 4: IMPLEMENT] → [GATE 5: VERIFY] → PRODUCTION
```

### Gate 1: UNDERSTAND
**Purpose**: Explore intent, gather requirements, research the domain.
**Skills Invoked**:
- `brainstorming` — Explore user intent before any implementation
- `openspec-explore` — Investigate problems and clarify requirements
- `notebooklm-researcher` — Deep domain research (if available)

**Deliverable**: `requirements.md` in `.sovereign/`
**HITL Gate**: ✅ User confirms requirements before proceeding

> 📖 Full protocol: `references/gate-1-understand.md`

### Gate 2: ANALYZE
**Purpose**: Evaluate feasibility, assess risks, define scope and metrics.
**Skills Invoked**:
- `expert-product-manager` — Product vision, PRD, SaaS metrics
- `expert-product-owner` — User stories with Gherkin AC, MoSCoW prioritization
- `project-development` — Task-model fit, pipeline architecture, cost estimation

**Deliverable**: `analysis.md` with PRD, user stories, and risk assessment
**HITL Gate**: ✅ User approves scope and priorities

> 📖 Full protocol: `references/gate-2-analyze.md`

### Gate 3: PLAN
**Purpose**: Design architecture, create implementation plan, define quality gates.
**Skills Invoked**:
- `expert-tech-architect` — System design, ADRs, API/DB schema
- `writing-plans` — Bite-sized implementation plan with file paths
- `planning-with-files` — Filesystem state machine (task_plan.md, progress.md)
- `expert-qa-engineer` — Test strategy, coverage goals, QA gates
- `tool-design` — Consolidate tools into primitives

**Deliverable**: `task_plan.md` with checkboxed tasks, `design.md` with ADRs
**HITL Gate**: ✅ User approves architecture decisions

> 📖 Full protocol: `references/gate-3-plan.md`

### Gate 4: IMPLEMENT
**Purpose**: Execute the plan with expert agents, write code, write tests.
**Skills Invoked**:
- `expert-dev` — Clean code implementation (SOLID, DRY)
- `expert-devops` — CI/CD, Docker, infrastructure
- `subagent-driven-development` — Parallel task dispatch
- `dispatching-parallel-agents` — Fan-out independent work
- `test-driven-development` — Red-Green-Refactor cycle
- `systematic-debugging` — 4-phase root cause analysis
- `using-git-worktrees` — Feature branch isolation

**Deliverable**: Working code with tests
**HITL Gate**: ❌ Autonomous (unless security/legal impact)

> 📖 Full protocol: `references/gate-4-implement.md`

### Gate 5: VERIFY
**Purpose**: Verify everything works, review code, prepare for deployment.
**Skills Invoked**:
- `verification-before-completion` — Evidence before claims
- `expert-qa-engineer` — QA gate validation
- `requesting-code-review` — PR review checklist
- `vibe-code-auditor` — Audit for structural flaws
- `finishing-a-development-branch` — Merge/PR/cleanup workflow

**Deliverable**: Verified, reviewed, merged code
**HITL Gate**: ✅ User approves production deployment

> 📖 Full protocol: `references/gate-5-verify.md`

---

## State Machine

All state persists in `.sovereign/` at the project root:

```
.sovereign/
├── state.json          # Current gate, task index, timestamps
├── requirements.md     # Gate 1 output
├── analysis.md         # Gate 2 output
├── task_plan.md        # Gate 3 output (with checkboxes)
├── design.md           # Gate 3 output (ADRs, schema)
├── progress.md         # Gate 4 running log
├── findings.md         # Gate 4 investigation notes
└── verification.md     # Gate 5 evidence log
```

### State Recovery Protocol

On session start, check for `.sovereign/state.json`:

```json
{
  "project": "my-app",
  "current_gate": 4,
  "current_task": 7,
  "total_tasks": 15,
  "started_at": "2026-05-25T10:00:00Z",
  "last_updated": "2026-05-25T12:30:00Z",
  "completed_gates": [1, 2, 3],
  "hitl_approvals": {
    "gate_1": "2026-05-25T10:15:00Z",
    "gate_2": "2026-05-25T10:45:00Z",
    "gate_3": "2026-05-25T11:00:00Z"
  }
}
```

If `state.json` exists:
1. Read current gate and task index
2. Read `task_plan.md` — find next unchecked `- [ ]` task
3. Resume from that exact point
4. Announce: "Resuming Gate {N}, Task {M}/{Total}"

If no `state.json`: Start fresh from Gate 1.

---

## Token Efficiency

### AST Packer (Codebase Understanding)

Instead of reading entire files, use `scripts/ast_packer.sh` to extract structure:

```bash
./library/aegis/scripts/ast_packer.sh /path/to/project > .sovereign/ast_index.md
```

This produces a compact representation (~2KB per 1000-line file) containing:
- File tree with sizes
- Function/class/method signatures (no bodies)
- Import/dependency graph
- TODO/FIXME markers

### Context Budget Rules

| Context Element | Max Tokens | Strategy |
|----------------|-----------|----------|
| System prompt + skills | 4,000 | Fixed |
| State files (.sovereign/) | 2,000 | Structured summary |
| AST index | 3,000 | Compressed skeleton |
| Active working files | 8,000 | Only files being edited |
| Conversation history | Remainder | Sliding window |

### Progressive Disclosure

- Gate protocols load from `references/` only when entering that gate
- Expert skills invoke only when their expertise is needed
- Tool outputs are masked after processing (keep summary, drop raw output)

---

## Expert Team Coordination

### Complexity Assessment (Before Spawning Agents)

Use the `expert-orchestrator` complexity scorecard:

| Score | Architecture | Token Cost |
|-------|-------------|-----------|
| 6-9 | Single agent | 1× |
| 10-14 | Small swarm (2-3 experts) | ~4× |
| 15+ | Full swarm (all experts) | ~15× |

### Execution Patterns

**Sequential Chain** (dependencies exist):
```
PM → Architect → Engineer → QA → DevOps
```

**Parallel Map** (independent tasks):
```
Fan-out: [Engineer-A, Engineer-B, Engineer-C]
Fan-in: Orchestrator integrates results
```

**Supervisor** (complex coordination):
```
Orchestrator delegates, monitors, integrates
```

---

## Quality Guardrails

All 11 rules from `library/experts/rules/` are enforced:

| Rule | Enforcement |
|------|-------------|
| `development.md` | No exceptions under time pressure |
| `testing.md` | No code without tests |
| `security.md` | Security-first, always |
| `git-workflow.md` | Clean commits with What + Why |
| `error-handling.md` | No silent fails |
| `logging.md` | Structured logging from day 1 |
| `environment.md` | Config as code, no hardcoding |
| `performance.md` | Performance is a requirement |
| `continuity.md` | Working memory across sessions |
| `memory.md` | Automatic knowledge persistence |
| `openspec-archive.md` | Archive completed changes |

---

## HITL (Human-in-the-Loop) Policy

### Requires Human Approval
- ✅ Requirements confirmation (Gate 1)
- ✅ Scope and priority approval (Gate 2)
- ✅ Architecture decisions (Gate 3)
- ✅ Production deployment (Gate 5)
- ✅ Legal/contract/NDA content
- ✅ Financial transactions
- ✅ Personal data handling
- ✅ API key/secret management

### Fully Autonomous
- ❌ Code implementation
- ❌ Test writing and execution
- ❌ Debugging and fixing
- ❌ Git operations (branch, commit, PR)
- ❌ CI/CD pipeline configuration
- ❌ Code review (automated)
- ❌ Documentation generation
- ❌ Refactoring and optimization

---

## Quick Start

```
User: "Build a task management API with authentication"

Aegis:
1. [GATE 1] Brainstorm requirements → user confirms
2. [GATE 2] PM creates PRD, PO writes stories → user approves scope
3. [GATE 3] Architect designs API, writes ADR → user approves architecture
4. [GATE 4] Engineer implements (TDD), DevOps sets up CI/CD → autonomous
5. [GATE 5] QA verifies, code reviewed → user approves deployment
```

## Integration

This skill connects to every skill in the ecosystem:
- `library/core/skills/` — 81 foundational workflow skills
- `library/experts/skills/` — 50 expert role skills
- `library/experts/rules/` — 11 quality guardrails
- `library/community/skills/` — 1,459 community skills
