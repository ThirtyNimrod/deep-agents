# Deep Research Agent

A high-performance research pipeline built on **Deep Agent** architecture, utilizing **ultra-small SLMs** (270M parameters) for orchestration and **Gemma 4** for high-fidelity reasoning. Designed to eliminate context rot through a decoupled Virtual Filesystem (VFS).

## 🚀 The Architecture: Deep Agents vs. Shallow Agents

Traditional "shallow" agents dump every tool output and intermediate thought into the chat history. In long-horizon research, this leads to **Context Rot**—degraded reasoning and soaring token costs.

This project implements the **Deep Agent** pattern:
*   **Decoupled State:** reasoning history is kept lean; raw data is offloaded to a **Virtual Filesystem (VFS)**.
*   **SLM Orchestration:** Routing and state evaluation are handled by `functiongemma:270m`, ensuring near-zero latency and deterministic graph transitions.
*   **Execution & Synthesis:** Heavy lifting (searching, analyzing, writing) is performed by `gemma4:e2b` and `ministral-3:3b`.
*   **Adversarial Verification:** An independent `gemma3:4b` node audits the final report against raw sources to prevent hallucinations.

## 🏗️ Model Role Map

| Role | Model | Task |
| :--- | :--- | :--- |
| **Traffic Cop (Router)** | `functiongemma:270m` | Deterministic node routing based on VFS manifest. |
| **Architect (Planner)** | `ministral-3:3b` | Dynamic `todo_list` management and task decomposition. |
| **Specialist (Execution)** | `gemma4:e2b` | Deep search, data extraction, and report synthesis. |
| **Auditor (Verifier)** | `gemma3:4b` | Adversarial cross-referencing of claims vs. sources. |

## 📂 Documentation Structure

Detailed documentation is available in the `docs/` folder, organized by implementation phase:

*   **[Implementation Roadmap](./docs/implementation/plan.md):** The high-level build strategy.
*   **[Project Checklist](./docs/checklists/project_checklist.md):** Actionable milestones for tracking progress.
*   **[Phases/](./docs/phases/):** Deep-dives into the theory and plan for each architectural pillar:
    *   **Phase 1: VFS** — Combating context rot.
    *   **Phase 2: Planning** — Externalized attention via SLM routing.
    *   **Phase 3: Execution** — Specialized reasoning nodes.
    *   **Phase 4: Verification** — Self-healing loops.
    *   **Phase 5: Integration** — LangGraph and Nothing-inspired UI.

## 🎨 UI/UX Philosophy: Nothing Design

The interface follows the **Nothing Design System**:
*   **Monochromatic & Typographically Driven:** Using `Doto`, `Space Grotesk`, and `Space Mono`.
*   **Information-Dense:** Exposes the internal state of the agent (todos, VFS manifest, current node).
*   **Mechanical Aesthetic:** Features segmented progress bars and dot-matrix motifs to feel like a high-precision instrument.

---
*Built for the next generation of local, efficient, and grounded AI research.*
