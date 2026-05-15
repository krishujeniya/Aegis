# Antigravity Power Restructuring Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Restructure existing Antigravity repositories into a unified Sovereign Hub.

**Architecture:** A 4-layer monorepo (Intelligence, Will, Muscle, Procedure) using npm workspaces for module management.

**Tech Stack:** Bash (mv/mkdir), npm (workspaces), Markdown.

---

### Task 1: Initialization & Directory Scaffolding

**Files:**
- Create: `/docs/superpowers/plans/2026-05-15-antigravity-power-restructuring.md` (this file)
- Create: `library/`, `modules/`, `workflows/`, `agents/`, `tools/`, `workspace/`, `.antigravity/`

- [ ] **Step 1: Create the Sovereign directory structure**

Run:
```bash
mkdir -p library/awesome library/base library/seo library/custom modules/manager modules/engine workflows agents tools workspace .antigravity
```

- [ ] **Step 2: Verify directory creation**

Run: `ls -d library/ modules/ workflows/ agents/ tools/ workspace/ .antigravity/`
Expected: All directories exist.

- [ ] **Step 3: Commit initial structure**

Run:
```bash
git add .
git commit -m "chore: scaffold sovereign hub directory structure"
```

---

### Task 2: Migrate Core Modules (The Muscle)

**Files:**
- Move: `AntigravityManager/` -> `modules/manager/`
- Move: `antigravity-project-starter/` -> `modules/engine/`

- [ ] **Step 1: Move AntigravityManager**

Run:
```bash
# We move the contents to avoid nested folders if the target exists
mv AntigravityManager/* modules/manager/
mv AntigravityManager/.* modules/manager/ 2>/dev/null || true
rmdir AntigravityManager
```

- [ ] **Step 2: Move Antigravity Project Starter**

Run:
```bash
mv antigravity-project-starter/* modules/engine/
mv antigravity-project-starter/.* modules/engine/ 2>/dev/null || true
rmdir antigravity-project-starter
```

- [ ] **Step 3: Commit migrations**

Run:
```bash
git add .
git commit -m "feat: migrate core modules to modules/ folder"
```

---

### Task 3: Migrate Knowledge Library (The Intelligence)

**Files:**
- Move: `antigravity-awesome-skills-main/` -> `library/awesome/`
- Move: `antigravity-skills-main/` -> `library/base/`
- Move: `Agentic-SEO-Skill/` -> `library/seo/`
- Move: `'Existing Skills'/` -> `library/custom/`

- [ ] **Step 1: Move Awesome Skills**

Run:
```bash
mv antigravity-awesome-skills-main/* library/awesome/
mv antigravity-awesome-skills-main/.* library/awesome/ 2>/dev/null || true
rmdir antigravity-awesome-skills-main
```

- [ ] **Step 2: Move Base Skills**

Run:
```bash
mv antigravity-skills-main/* library/base/
mv antigravity-skills-main/.* library/base/ 2>/dev/null || true
rmdir antigravity-skills-main
```

- [ ] **Step 3: Move SEO Skill**

Run:
```bash
mv Agentic-SEO-Skill/* library/seo/
mv Agentic-SEO-Skill/.* library/seo/ 2>/dev/null || true
rmdir Agentic-SEO-Skill
```

- [ ] **Step 4: Move Existing Skills**

Run:
```bash
mv 'Existing Skills'/* library/custom/
mv 'Existing Skills'/.* library/custom/ 2>/dev/null || true
rmdir 'Existing Skills'
```

- [ ] **Step 5: Commit library migrations**

Run:
```bash
git add .
git commit -m "feat: consolidate knowledge library into library/ folder"
```

---

### Task 4: Migrate Procedures & Tools

**Files:**
- Move: `antigravity-workflows/` -> `workflows/`

- [ ] **Step 1: Move Workflows**

Run:
```bash
mv antigravity-workflows/* workflows/
mv antigravity-workflows/.* workflows/ 2>/dev/null || true
rmdir antigravity-workflows
```

- [ ] **Step 2: Commit workflow migrations**

Run:
```bash
git add .
git commit -m "feat: migrate workflows to workflows/ folder"
```

---

### Task 5: System Configuration (The Brain)

**Files:**
- Create: `package.json`
- Create: `CLAUDE.md`

- [ ] **Step 1: Initialize root package.json with workspaces**

```json
{
  "name": "antigravity-power-sovereign",
  "version": "1.0.0",
  "description": "The Sovereign Engine of Creation",
  "private": true,
  "workspaces": [
    "modules/*"
  ],
  "scripts": {
    "manager": "npm run dev --workspace=modules/manager",
    "engine": "npm run dev --workspace=modules/engine"
  }
}
```

- [ ] **Step 2: Create root CLAUDE.md**

```markdown
# 🌌 Antigravity Power: Sovereign Rules

## 🏛️ Project Vision
The Sovereign Hub is a unified agentic platform. All development follows the **5-Gate OpenSpec** workflow.

## 📜 Development Rules
- **Knowledge**: Always reference `library/` for specialized skills.
- **Procedures**: Follow protocols in `workflows/`.
- **Agents**: Use definitions in `agents/` for specialized tasks.
- **Sovereignty**: New projects MUST be created in `workspace/`.

## 🛠️ Commands
- `npm install`: Install dependencies for all modules.
- `npm run manager`: Start the Antigravity Manager.
- `npm run engine`: Start the Project Engine.
```

- [ ] **Step 3: Commit system configuration**

Run:
```bash
git add package.json CLAUDE.md
git commit -m "chore: initialize sovereign configuration and workspaces"
```
