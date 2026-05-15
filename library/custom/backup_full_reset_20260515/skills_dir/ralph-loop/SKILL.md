---
name: ralph-loop
description: "Iterative autonomous development loop using the 'Ralph Wiggum' persistence technique."
category: automation
---

# Ralph Loop (Ralph Wiggum Persistence)

The Ralph Loop is an autonomous development methodology designed to handle complex, multi-step tasks by breaking them into atomic iterations and preventing context rot.

## 🚀 The Core Loop

1. **Initialization**: Read the Product Requirements Document (`PRD.md`) and the current project state.
2. **Iteration**:
   - Set a clear goal for the current iteration.
   - Execute the task.
   - Run external verification (tests, builds, health checks).
3. **Termination/Persistence**:
   - If verification passes: Complete the task or move to the next step.
   - If verification fails: Log the failure in `progress.txt`, CLEAR context, and RESTART the loop using the failure log as the next starting point.

## 🛠️ Usage with Ralph MCP

Use the `@ralph-mcp` tools to manage this loop:
- `start_loop`: Initialize an autonomous session.
- `update_progress`: Log current state to persist across context clears.
- `verify_step`: Run external checks.

## 🧠 Philosophy

"I'm in danger!" — Like Ralph Wiggum, the loop is relentlessly persistent. By frequently clearing the conversation context and relying on the filesystem for memory, you avoid the "hallucination spiral" that occurs in long AI sessions.

## 📂 Required Files

- `PRD.md`: The source of truth for the project requirements.
- `progress.txt`: The linear log of what has been completed and what failed.
- `PLAN.md`: The immediate next steps for the current iteration.

## 🤖 When to Use
- Large refactors
- Building new features from scratch
- Fixing complex, multi-file bugs
- Migrating whole stacks
