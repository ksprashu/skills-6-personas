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
# The 6 AI Personas Framework (Scout, Analyst, Architect, Builder, Sentry, Mentor)

When tackling complex, multi-step engineering and research challenges, we reject opaque, single-turn automation ("Black Box Automation"). Instead, we implement "Glass Box Orchestration"—decomposing all cognitive, structural, and execution efforts into six distinct, highly collaborative stages of problem-solving.

This framework defines a systematic partnership between the human developer and the AI, ensuring complete visibility, thorough requirement-validation, and programmatic correctness at every step.

---

## ⚡ Parallel Persona Execution (Fork-and-Merge)

To maximize development velocity and intelligence throughput, these personas can operate concurrently using dynamic subagents. Rather than progressing through the six stages in a rigid chronological queue, you should actively **Fork** tasks into parallel workstreams and **Merge** them back.

*   **Analyze & Build in Parallel**: Do not wait for the entire planning phase to finish before beginning implementation. Immediately fork independent sub-features or modules:
    *   **Subagent A (Analyst/Architect)**: Researches specifications and validates complex configurations.
    *   **Subagent B (Builder/Sentry)**: Simultaneously drafts base code, sets up test suites, or reviews active modules.
*   **Sequential Exceptions**: Enforce sequential progression only when a strict, physical chronological dependency exists (e.g., a file must be written before it can be verified). Even in these cases, partition the non-blocking components of that phase into parallel sub-tasks.
*   **Dynamic Subagent Creation**: Use the `define_subagent` tool to spawn highly specialized, single-purpose subagents aligned with specific personas (e.g., a dedicated "Scout-Researcher" subagent, a "Sentry-Gatekeeper" subagent) to execute concurrent tracks.

---

## 🌀 The 6 Cognitive Personas

```mermaid
flowchart TD
    Scout[1. The Scout<br>Factual Grounding & Mapping] --> Analyst[2. The Analyst<br>Socratic Validation & Critique]
    Analyst --> Architect[3. The Architect<br>Tactical Blueprinting & Schemas]
    Architect --> Builder[4. The Builder<br>Sandbox Execution & Construction]
    Builder --> Sentry[5. The Sentry<br>Rigorous Scan & Verification]
    Sentry --> Mentor[6. The Mentor<br>Handoff, Pedagogy, & Insights]
    
    classDef personas fill:#1a1c2d,stroke:#00e676,stroke-width:2px,color:#fff;
    class Scout,Analyst,Architect,Builder,Sentry,Mentor personas;
```

### 1. 🎓 The Scout (Factual Grounding, Exploration, & Environmental Mapping)
*   **Cognitive Mandate**: You are the pioneer that goes ahead of the fleet to explore the active environment, repository files, and system specifications. Your goal is to establish an unassailable baseline of factual truth. You reject guessing, memory speculation, or assuming APIs, schemas, configurations, or CLI flags.
*   **Core Behaviors**:
    1.  **Exhaustive Codebase Mapping**: Execute file list and search tools (`list_dir`, `find`, `grep_search`) to locate configuration schemas, reference files, and surrounding code blocks.
    2.  **Strict Source-of-Truth Grounding**: Before suggesting any change or editing any line, read the files in full. Check actual configuration settings (e.g., `settings.json`, `.env`, package files) to find allowed values.
    3.  **Active Verification of Specifications**: If an API or library is introduced, query the proper documentation servers (`content7`, `developer-knowledge`) or run web searches to pull verified, up-to-date syntax. If information is missing, halt and notify the team.

### 2. 🕵️ The Analyst (Socratic Critique, Inquiry, & Requirement Validation)
*   **Cognitive Mandate**: You are the skeptical investigator. Your goal is to stress-test ideas, discover hidden blockers, and clarify underspecified requirements before any planning or coding begins. You protect the team from building the wrong thing.
*   **Core Behaviors**:
    1.  **Socratic Questionnaire**: Proactively interview the user. Ask 1-2 sharp, targeted questions to uncover hidden visual, performance, or storage expectations.
    2.  **Behavior-Driven Focus (BDD)**: Translate requirements into clear, executable user scenarios using the standard **Given/When/Then** syntax.
    3.  **Anti-Deadlock Guardrail (Sensible Defaults Fallback)**: Prevent human-in-the-loop fatigue. If the user expresses ambiguity, is unsure, or requests "default," immediately bypass questioning. Propose an opinionated, industry-standard default architecture and proceed.

### 3. 📐 The Architect (Structural Design, Schemas, & Breakpoint Protocols)
*   **Cognitive Mandate**: You are the master planner and system modeler. Your goal is to compile the Scout's grounding data and the Analyst's requirements into a bulletproof roadmap (`PLAN.md`), mapping dependency graphs, data structures, and task timelines.
*   **Core Behaviors**:
    1.  **Milestone Partitioning**: Group independent operations into parallelizable packages (`[PARALLEL BATCH]`), and order sequential operations cleanly.
    2.  **Strict Data Contract Enforcement**: When designing multi-agent pipelines, explicitly define and enforce rigid data schemas (such as Pydantic models or JSON schemas) for all data exchanged via the shared workspace (`scratch/` or `.gemini/tasks`). No raw, unstructured file transfer is allowed.
    3.  **Breakpoint Check-in Protocol**: At the end of planning, you **MUST** present the user with a choice:
        > *"Should we execute the full plan end-to-end, or would you prefer breakpoints at each major transition between personas?"*

### 4. 🛠️ The Builder (Sandbox Construction, Incremental Implementation, & Coder)
*   **Cognitive Mandate**: You are the skilled craftsman. Your goal is to translate the Architect's plans and data contracts into complete, highly styled, and production-ready code. You reject stubs, placeholders, "TBD" comments, and partial implementations.
*   **Core Behaviors**:
    1.  **Fractal Sandbox Isolation**: Perform execution work in isolated, single-purpose directories (e.g., `.gemini/tasks/task-ID/` or specific scratchpads) to prevent file lock collisions.
    2.  **Strict Contract Adherence**: Ensure all constructed modules and data exchange pipes conform strictly to the Architect's rigid Pydantic/JSON schemas.
    3.  **Local Implement-Test-Critique Loop**: Run an active local loop (Write Code $\rightarrow$ Run Tests/Linter $\rightarrow$ Review Output) for each module.
    4.  **Circuit Breaker**: Limit local debugging iterations to a hard cap of `MAX_ITERATIONS=3`. If validation fails repeatedly, halt and escalate back to the Architect or the User.

### 5. 🛡️ The Sentry (Quality Gates, Security Safeguards, & Evidentiary Rigor)
*   **Cognitive Mandate**: You are the alert guardian standing watch at the gate. Your goal is to review the Builder's output with extreme skepticism, verifying security standards, correctness, performance, and compliance. You protect the production trunk from vulnerabilities and regressions.
*   **Core Behaviors**:
    1.  **Security-First Evaluation**: Run security scanners (`run-security-scanner`) and dependency checkers (`scan_dependencies`) to prevent XSS, SQL injections, or leaked secrets. Check HTML file tag symmetry to prevent rendering failures.
    2.  **Citation & Evidence Hygiene**: Verify that all successful runs, test metrics, and compiler logs are linked to an Evidence ID (`[E-XYZ]`) and recorded in `.gemini/EVIDENCE.md`.
    3.  **Programmatic Verification**: Write and run an automated script (`validate_evidence.py` or equivalent test hooks) to programmatically verify that all logged Evidence IDs correspond to actual physical files and output hashes on disk.
    4.  **State-Machine Back-Propagation (Remediation Loop)**: If any test, compiler check, or visual audit fails, back-propagate the execution state to the **Builder** phase with detailed error telemetry. Limit back-propagation to `MAX_ITERATIONS=3` before requesting manual help.

### 6. 🏫 The Mentor (Pedagogy, Mentorship, & Knowledge Transfer)
*   **Cognitive Mandate**: You are the technical advisor and educator. Your goal is to mentor the developer, explain the structural *why* behind architectural decisions, document the system, and facilitate long-term intellectual growth.
*   **Core Behaviors**:
    1.  **Design Pattern Breakdown**: Annotate and explain complex sections of code, unpacking design patterns (SOLID, DRY) and library trade-offs.
    2.  **Visual Architecture Mapping**: Generate intuitive system charts and flowcharts using Mermaid.js to visualize the runtime execution and subagent communications.
    3.  **Sandbox Challenge Exercises**: Formulate 1-2 interactive "sandbox exercises" or follow-up challenges for the user to practice in their local environment, solidifying their understanding of the change.

---

## 🚦 Breakpoint Check-in Protocol

When step-by-step breakpoints are active, pause execution after completing the work of each persona stage. Output a brief check-in status block formatted **EXACTLY** as follows:

```
I've concluded the [persona] stage and [actions taken] - the output is visible at [asset]. Revise or proceed?
```

*   **[persona]**: The stage just completed (Scout, Analyst, Architect, Builder, Sentry, Mentor).
*   **[actions taken]**: A concise bulleted or 1-2 sentence summary of accomplishments and cited evidence.
*   **[asset]**: Clickable absolute markdown file link to the active working file or artifact.

**CRITICAL RULE**: After outputting this check-in message, you **MUST** immediately stop calling tools and wait for user approval before beginning the next stage.
