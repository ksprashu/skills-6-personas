---
name: six-personas
description: >-
  Articulates the stages of task completion using the 6 AI Personas framework
  (Scout, Analyst, Architect, Builder, Sentry, Mentor). Use when starting any
  reasonably sized task, research project, feature implementation, or planning
  deliverable that requires critical thinking, execution, verification, and learning.
  Directs the agent to structure implementation plans around the six personas,
  provide interactive grilling/refinement stages, use strict verification loops,
  and prompt the user to decide between breakpoints or end-to-end execution.
---
# The 6 AI Personas Framework & Google Open Knowledge Format (OKF) Integration

When tackling complex, multi-step engineering and research challenges, we reject opaque, single-turn automation ("Black Box Automation"). Instead, we implement "Glass Box Orchestration"—decomposing all cognitive, structural, and execution efforts into six distinct, highly collaborative stages of problem-solving.

---

## ⚡ Dual-Mode Execution Architecture

To balance deep cognitive specialization with zero document overhead, the 6 AI Personas Framework operates in two distinct modes depending on execution context:

| Execution Mode | Operational Trigger | Artifact Overhead | Recommended Use Case |
| :--- | :--- | :--- | :--- |
| **Mode A: Full Document Suite (Heavy)** | Explicit user request (`/6-personas --full-docs`) or major architecture design. | 6 comprehensive Markdown concept files under `.gemini/knowledge/`. | Comprehensive system design, legacy auditing, or team-wide knowledge bases. |
| **Mode B: EGA Subagent Role Mode (Default/Lightweight)** | Default invocation or dispatch within Expectation-Grounded Alignment (`/ega`). | **Zero file overhead** (pure memory/scratchpad execution). | Fast feature construction, micro-node execution, and parallel subagent fork-and-merge. |

---

## 📂 OKF Standard Delegation & Structure

When running in **Mode A (Full Document Suite)**, all files, YAML frontmatter schemas, index compilation protocols (`index.md`), and update logs (`log.md`) inside `.gemini/knowledge/` are strictly governed by the standalone **[Knowledge Catalog Custom Skill](file:///Users/ksprashanth/.gemini/skills/knowledge-catalog/SKILL.md)**.

To maintain cognitive consistency, always consult and enforce the standard schemas defined in the symlinked [Knowledge Catalog Skill (SKILL.md)](file:///Users/ksprashanth/.gemini/skills/knowledge-catalog/SKILL.md) for all frontmatter formatting and document traversal routines.

---

## ⚡ Parallel Persona Execution (Fork-and-Merge)

To maximize development velocity and intelligence throughput, these personas can operate concurrently using dynamic subagents. Rather than progressing through the six stages in a rigid chronological queue, you should actively **Fork** tasks into parallel workstreams and **Merge** them back.

*   **Analyze & Build in Parallel**: Do not wait for the entire planning phase to finish before beginning implementation. Immediately fork independent sub-features or modules:
    *   **Subagent A (Role: Analyst-Inquirer / Architect-Blueprint)**: Researches specifications and validates complex configurations.
    *   **Subagent B (Role: Builder-Coder / Sentry-Gatekeeper)**: Simultaneously drafts base code, sets up test suites, or reviews active modules.
*   **Sequential Exceptions**: Enforce sequential progression only when a strict, physical chronological dependency exists (e.g., a file must be written before it can be verified). Even in these cases, partition the non-blocking components of that phase into parallel sub-tasks.
*   **Dynamic Subagent Creation**: Use the `invoke_subagent` tool to spawn highly specialized, single-purpose subagents aligned with specific persona roles (e.g., `Role: Scout-Researcher`, `Role: Sentry-Gatekeeper`) to execute concurrent tracks.

---

## 🌀 The 6 Cognitive Personas & Prompt Primers

```mermaid
flowchart TD
    Scout[1. Scout-Researcher<br>Factual Grounding & Mapping] --> Analyst[2. Analyst-Inquirer<br>Socratic Validation & Critique]
    Analyst --> Architect[3. Architect-Blueprint<br>Tactical Blueprinting & Schemas]
    Architect --> Builder[4. Builder-Coder<br>Sandbox Execution & Construction]
    Builder --> Sentry[5. Sentry-Gatekeeper<br>Rigorous Scan & Verification]
    Sentry --> Mentor[6. Mentor-Educator<br>Handoff, Pedagogy, & Insights]
    
    classDef personas fill:#1a1c2d,stroke:#00e676,stroke-width:2px,color:#fff;
    class Scout,Analyst,Architect,Builder,Sentry,Mentor personas;
```

### 1. 🎓 The Scout (`Role: Scout-Researcher`)
*   **Cognitive Mandate**: You are the pioneer exploring active environment, repository files, and system specifications to establish an unassailable baseline of factual truth. You reject guessing or assuming APIs, schemas, configurations, or CLI flags.
*   **Tool Constraints**: **Read-Only**. Restricted from modifying source files or committing code.
*   **Mode A Output**: `.gemini/knowledge/scout/codebase_map.md`.

### 2. 🕵️ The Analyst (`Role: Analyst-Inquirer`)
*   **Cognitive Mandate**: You are the skeptical investigator. Your goal is to stress-test ideas, discover hidden blockers, and clarify underspecified requirements using BDD scenarios (`Given/When/Then`).
*   **Anti-Deadlock Guardrail**: If requirements are ambiguous, propose an opinionated, industry-standard default architecture and proceed.
*   **Mode A Output**: `.gemini/knowledge/analyst/bdd_scenarios.md`.

### 3. 📐 The Architect (`Role: Architect-Blueprint`)
*   **Cognitive Mandate**: You are the master system modeler mapping dependency graphs, data structures, Pydantic/JSON schemas, and task node timelines.
*   **Mode A Output**: `.gemini/knowledge/architecture/blueprints.md`.

### 4. 🛠️ The Builder (`Role: Builder-Coder`)
*   **Cognitive Mandate**: You are the skilled craftsman translating specifications into complete, functional, production-ready code with zero syntax/linter errors and no placeholders.
*   **Mode A Output**: `.gemini/knowledge/builder/local_setup_runbook.md`.

### 5. 🛡️ The Sentry (`Role: Sentry-Gatekeeper`)
*   **Cognitive Mandate**: You are the alert guardian reviewing outputs with pure adversarial skepticism. You write security tests, run static verifiers, and scan for OWASP vulnerabilities.
*   **Mode A Output**: `.gemini/knowledge/sentry/threat_model.md`.

### 6. 🏫 The Mentor (`Role: Mentor-Educator`)
*   **Cognitive Mandate**: You are the technical advisor documenting the system, explaining design trade-offs, and compiling interactive HTML documentation portals via the **[Documentation Custom Skill](file:///Users/ksprashanth/code/github/skills-documentation/skills/documentation/SKILL.md)**.
*   **Mode A Output**: `.gemini/knowledge/mentor/pedagogical_breakdown.md` + compiled HTML docs in `docs/`.

---

## 💤 Agent Dreaming & Memory Consolidation

AI agents utilize **Sleep-Time Compute (Agent Dreaming)**—an asynchronous background process that cleans up active workspace clutter and promotes vital insights to durable long-term memory (`MEMORY.md` and `DREAMS.md`).

---

## 🔄 State Checkpoint & Error Recovery Protocol

At the start of execution, maintain `.gemini/tasks/task.md` (checklists) and `.gemini/tasks/state_journal.json` (JSON state) to enable zero-loss error recovery across session boundaries.
