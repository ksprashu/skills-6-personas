# 🌀 6 AI Archetypes (Evolved with Vector Protocol)

![6-archetypes Header](./docs/images/header.png)

A state-of-the-art framework for **"Glass Box Orchestration"** of agentic AI coding assistants. This framework rejects unverified, black-box automation in favor of a highly structured, transparent, and verifiable pipeline. 

By decomposing complex engineering tasks into **six distinct cognitive stages**, this skill establishes a collaborative, high-fidelity partnership between the developer and the agent.

---

## 🧭 The 6 AI Archetypes

```mermaid
flowchart LR
    Scholar[1. Scholar<br>Context & Ingest] ──> Analyst[2. Analyst<br>Grilling & Refine]
    Analyst ──> Architect[3. Architect<br>Tactical Plan]
    Architect ──> Producer[4. Producer<br>Isolated Sandbox]
    Producer ──> Auditor[5. Auditor<br>Audit & Citations]
    Auditor ──> Teacher[6. Teacher<br>Pedagogy & Models]
    
    classDef archetypes fill:#0e101f,stroke:#7c4dff,stroke-width:2px,color:#fff;
    class Scholar,Analyst,Architect,Producer,Auditor,Teacher archetypes;
```

### 1. 🎓 The Scholar (Context & Grounding)
*   **Role**: Ingests repository files, structural guidelines, and standards to establish an unassailable knowledge baseline.
*   **Vector Safeguard**: Strictly prohibits ungrounded assertions. All plan components must be backed by codebase search evidence (`grep_search`, `list_dir`, or file views).

### 2. 🕵️ The Analyst (Socratic Critique & Idea Refinement)
*   **Role**: Proactively interviews the user, stress-testing requirements and clarifying underspecified designs one targeted question at a time.
*   **Vector Safeguard**: Intercepts vague requirements before planning begins, leveraging `idea-refine`, `interview-me`, and `grill-me` capabilities.

### 3. 📐 The Architect (Tactical Roadmaps & Breakpoints)
*   **Role**: Formulates robust execution schedules (`PLAN.md`) detailing dependency chains, parallel operations, and rollback conditions.
*   **Vector Safeguard**: Presents the **Breakpoint Check-in Protocol** asking the user whether to proceed end-to-end or with step-by-step pauses at each stage.

### 4. 🛠️ The Producer (Fractal Sandbox Execution)
*   **Role**: Runs implementation work in parallel, isolated sandbox subdirectories, utilizing robust `Implement ➔ Test ➔ Critique` loops.
*   **Vector Safeguard**: Integrates a circuit breaker capping failed attempts at `MAX_ITERATIONS=3` before escalating back to the Architect or User.

### 5. 🛡️ The Auditor (Risk Audit & Citation Hygiene)
*   **Role**: Acts as a senior security auditor and quality gates controller, verifying license compliance, credentials safety, and regression tests.
*   **Vector Safeguard**: Enforces **Citation Hygiene** by requiring all outcomes, tests, and metrics to reference verified Evidence IDs in `.gemini/EVIDENCE.md`.

### 6. 🏫 The Teacher (Pedagogy & Mental Models)
*   **Role**: Mentors the developer, providing clear explanations of architectural patterns, design principles (SOLID, DRY), and interactive exercises to reinforce learning.
*   **Vector Safeguard**: Generates intuitive system diagrams (Mermaid.js) and structures a seamless developer handoff.

---

## 📁 Repository Structure

```
6-archetypes/
├── README.md               # This comprehensive guide
├── docs/
│   ├── guide.html          # SOTA local interactive user guide
│   └── images/
│       └── header.png      # Custom generated repository banner
└── skills/
    └── 6-archetypes/
        └── SKILL.md        # Primary skill system instructions for the agent
```

---

## 🛠️ Installation & Linking

This skill lives in your `~/code/github/` workspace as a single source of truth and symlinks back to your primary agent configuration folders.

```bash
# Link the skill to your primary ~/.agents/skills hub:
ln -s "$(pwd)/skills/6-archetypes" ~/.agents/skills/6-archetypes
```

The system automatically handles client resolution:
*   **Gemini / Antigravity CLI:** Loads via `~/.gemini/skills/6-archetypes` pointing to `~/.agents/skills/6-archetypes`.
*   **Claude Code CLI:** Loads via `~/.claude/skills/6-archetypes` pointing to `~/.agents/skills/6-archetypes`.

---

## 🚥 The Breakpoint Check-in Protocol

When running in step-by-step mode, the agent pauses after completing each archetype's stage, outputting the exact status block:

```
I've concluded the [archetype] stage and [actions taken] - the output is visible at [asset]. Revise or proceed?
```

*   **[archetype]**: Stage just completed (Scholar, Analyst, Architect, Producer, Auditor, Teacher).
*   **[actions taken]**: Bulleted highlights of completed actions and grounding evidence.
*   **[asset]**: Absolute markdown file link to the active working file or artifact.

The agent will **halt execution and wait** for your manual approval before transitioning into the next archetype stage.

---

## 📖 Local Interactive Documentation

This repository includes a stunning, high-fidelity interactive user guide loaded with hover transitions, micro-animations, and full documentation on the integrated Vector safeguards.

To open and explore it locally in your browser:
```bash
# On Mac:
open ./docs/guide.html
```
