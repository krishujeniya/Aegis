# 🌌 Antigravity Power: Sovereign Hub Design Specification

**Status:** Draft | **Date:** 2026-05-15 | **Author:** Antigravity AI

## 1. Vision
To transform a collection of agentic tools into a unified **Sovereign Hub** that serves as both a development platform and a master reference for building new projects. This hub integrates specialized skills, workflows, functional modules, and active agent personalities into a cohesive engine.

---

## 2. The 4-Layer Architecture

### Layer 1: Intelligence (The Knowledge Base)
*   **Path:** `/library/`
*   **Source:** Consolidated skills from `awesome-skills`, `skills-main`, `SEO-Skill`, and custom folders.
*   **Function:** Provides the `SKILL.md` playbooks for architectural, coding, and security tasks.

### Layer 2: Will (The Agents)
*   **Path:** `/agents/`
*   **Function:** Contains YAML/JSON definitions for specialized agent personas (Navigator, Architect, Coder, Researcher). Each persona defines its own system prompt and available toolsets.

### Layer 3: Muscle (The Engines)
*   **Path:** `/modules/`
*   **Source:** `AntigravityManager` (Navigator) and `antigravity-project-starter` (Project Engine).
*   **Function:** Functional components that handle account management and code manipulation.

### Layer 4: Procedure (The Workflows)
*   **Path:** `/workflows/`
*   **Source:** `antigravity-workflows`.
*   **Function:** Multi-step protocols (like the 5-Gate OpenSpec) that guide the agents through the development lifecycle.

---

## 3. Directory Mapping & Migration Plan

The following migrations will be performed using `mv` to ensure no data loss:

| Original Path | New Sovereign Path |
| :--- | :--- |
| `AntigravityManager/` | `modules/manager/` |
| `antigravity-project-starter/` | `modules/engine/` |
| `antigravity-awesome-skills-main/` | `library/awesome/` |
| `antigravity-skills-main/` | `library/base/` |
| `Agentic-SEO-Skill/` | `library/seo/` |
| `'Existing Skills'/` | `library/custom/` |
| `antigravity-workflows/` | `workflows/` |

**New Top-Level Directories:**
*   `/agents/`: For active agent definitions.
*   `/workspace/`: For new projects spawned from this reference.
*   `/tools/`: For binaries and CLI helpers.
*   `/.antigravity/`: For system state and session memory.

---

## 4. Configuration & Continuity

### 4.1 Root `package.json`
Initialize a root package manager with npm workspaces to manage dependencies across `modules/manager/` and `modules/engine/`.

### 4.2 `CLAUDE.md` (The Master Brain)
Define project-wide rules:
*   Always reference `library/` for technical playbooks.
*   Enforce the 5-Gate OpenSpec workflow.
*   Standardize on the Antigravity naming convention.

---

## 5. Success Criteria
1.  All existing functional components (Manager, Engine) remain operational.
2.  Skills are searchable and accessible via unified paths.
3.  The root directory is clean, organized, and follows the "Sovereign" aesthetic.
4.  New projects can be initialized within `workspace/` referencing the root libraries.
