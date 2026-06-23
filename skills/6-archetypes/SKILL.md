---
name: six-archetypes
description: >-
  Articulates the stages of task completion using the 6 AI Archetypes framework
  (Scholar, Analyst, Architect, Producer, Advisor, Teacher). Use when starting any
  reasonably sized task, research project, feature implementation, or planning
  deliverable that requires critical thinking, execution, verification, and learning.
  Directs the agent to structure implementation plans around the six archetypes,
  provide interactive grilling/refinement stages, use strict Vector verification loops,
  and prompt the user to decide between breakpoints or end-to-end execution.
---
# The 6 AI Archetypes Framework (Evolved with Vector Protocol)

> [!NOTE] **Reference Document:**
> This skill integrates the [5 AI Archetypes Framework](https://docs.google.com/document/d/1HoWJBg8AaIENMp-HZ69LhKqKGGN8KHaP3LmHKksWuRw/view?resourcekey=0-Ovkd4T7DYEwBVKGKnOFaLw) and the safety-critical execution standards of the **Vector Protocol**.

When tackling complex, multi-step engineering tasks, we avoid **"Black Box Automation"**—the habit of trying to solve entire problems in a single, unverified turn. Instead, we use **"Glass Box Orchestration"**, decomposing all cognitive and execution work into six distinct stages.

---

## 🌀 The 6 AI Archetypes

```mermaid
flowchart TD
    Scholar[1. The Scholar<br>Context & Grounding] --> Analyst[2. The Analyst<br>Grilling & Refinement]
    Analyst --> Architect[3. The Architect<br>Tactical Plan & Breakpoints]
    Architect --> Producer[4. The Producer<br>Swarms & Verification]
    Producer --> Advisor[5. The Advisor<br>Audit & Citations]
    Advisor --> Teacher[6. The Teacher<br>Pedagogy & Mental Models]
    
    classDef archetypes fill:#1a1c2d,stroke:#7c4dff,stroke-width:2px,color:#fff;
    class Scholar,Analyst,Architect,Producer,Advisor,Teacher archetypes;
```

### 1. 🎓 The Scholar (Context & Ingest)
*   **Role**: Absorbs codebase architecture, documentation, standards, and issues to establish a verified knowledge baseline.
*   **Vector Safeguard (Mandatory Grounding)**: You **MUST NOT** propose plans, structural modifications, or APIs without executing grounding tools (`grep_search`, `web_fetch`, or codebase checks) first. Any ungrounded assertion is rejected.
*   **Implicit Skills**: Integrates with `context-engineering`, `source-driven-development`, and `using-agent-skills`.

### 2. 🕵️ The Analyst (Insight, Critique, & Idea Refinement)
*   **Role**: Challenges assumptions, identifies blockers, and collaborates with the user to refine vague concepts.
*   **Interactive Grilling**: If the task details are underspecified or high-risk, the Analyst will pause to **interview the user, asking targeted questions one at a time**.
*   **Implicit Skills**: Integrates with `idea-refine`, `interview-me`, `grill-me`, and `grill-with-docs` to stress-test requirements.

### 3. 📐 The Architect (Structure, Plan, & Breakpoint Protocol)
*   **Role**: Organizes insights into a robust roadmap (`PLAN.md`) *before* writing code. Separates planning from execution.
*   **Tactical roadmaps**: Plan tasks as independent execution packages, grouping independent items into `[PARALLEL BATCH]` packages.
*   **Breakpoint Check**: At the end of the planning phase, you **MUST** ask the user:
    > *"Should we execute the full plan end-to-end, or would you prefer breakpoints at each major transition between archetypes?"*
*   **Implicit Skills**: Integrates with `planning-and-task-breakdown` and `spec-driven-development`.

### 4. 🛠️ The Producer (Drafting, Sandboxing, & Swarm Execution)
*   **Role**: Expands the agreed-upon structure into high-fidelity, production-ready assets (code, PRDs, scripts).
*   **Fractal Sandbox Isolation**: Execute parallel tasks in isolated fractal subdirectories (e.g., `.gemini/tasks/task-ID/`) to avoid file locking collisions and context bloat.
*   **Verification Loop**: For every module, run a strict `Implement` ➔ `Test` ➔ `Critique` loop.
*   **Circuit Breaker**: Limit retries to a hard cap of **`MAX_ITERATIONS=3`**. If a test or validation fails repeatedly, halt and escalate back to the Architect or User.
*   **Implicit Skills**: Integrates with `incremental-implementation`, `tdd`, `test-driven-development`, and `frontend-ui-engineering`.

### 5. 🛡️ The Advisor (Risk Audit & Citation Hygiene)
*   **Role**: Acts as a senior code reviewer, security auditor, or skeptical stakeholder to critique and harden the output.
*   **Citation Hygiene**: Every factual assertion, test success, or build run must reference a specific Evidence ID (`[E-XYZ]`) recorded in `.gemini/EVIDENCE.md`.
*   **Risk Audit**: Conduct an internal risk assessment answering:
    *   *Risk*: What are the irreversible consequences of this change?
    *   *Assumptions*: What unverified premises are we still relying on?
*   **Implicit Skills**: Integrates with `code-review-and-quality`, `security-and-hardening`, and `accidental-data-loss-prevention`.

### 6. 🏫 The Teacher (Pedagogy & Mental Models)
*   **Role**: Mentors the user by breaking down the final implementation, explaining the *why* behind architectural patterns, and reinforcing technical growth.
*   **Pedagogical Breakdown**:
    *   Explain design patterns, SOLID principles, and library trade-offs.
    *   Generate Mermaid.js system architecture or flow diagrams.
    *   Annotate critical sections of code, explaining key lines.
    *   Offer 1-2 interactive "sandbox exercises" or follow-up challenge questions for the user to try.
*   **Implicit Skills**: Integrates with `zoom-out` and `codelab-creator`.

---

## 🚦 Breakpoint Check-in Protocol

When running with step-by-step breakpoints, pause after completing the work of each archetype stage before beginning the next. Present a brief check-in message formatted **EXACTLY** as follows:

```
I've concluded the [archetype] stage and [actions taken] - the output is visible at [asset]. Revise or proceed?
```

*   **[archetype]**: The stage just completed (Scholar, Analyst, Architect, Producer, Advisor, Teacher).
*   **[actions taken]**: A concise 1-2 sentence summary of what was accomplished and grounding evidence cited.
*   **[asset]**: Clickable markdown file link to the artifact or code.

**CRITICAL RULE**: After presenting this check-in message, you **MUST** stop calling tools and wait for user approval before moving to the next stage.
