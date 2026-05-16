# Deep Research Agent - Project Context

This directory is a research and design workspace for the **Deep Research Agent**, a high-performance research pipeline built on a decoupled **Deep Agent** architecture.

## 📁 Directory Overview

The project is currently in the **Architectural Design and Planning** phase. The workspace is organized to facilitate theoretical deep-dives and implementation roadmaps.

### Key Components
- **Deep Agent Architecture:** Focuses on eliminating "Context Rot" by decoupling the model's reasoning history from raw data using a **Virtual Filesystem (VFS)**.
- **SLM Orchestration:** Utilizes ultra-small SLMs (e.g., `functiongemma:270m`) for high-speed, deterministic graph routing.
- **Nothing Design System:** Adopts a minimalist, typographically driven UI philosophy for exposing internal agent state.

## 🗺️ Key Files & Folders

- **`deep-research/README.md`**: Primary entry point. Explains the "Deep vs. Shallow" agent philosophy and the model role map.
- **`deep-research/docs/implementation/plan.md`**: The 5-phase execution strategy, from VFS setup to LangGraph integration.
- **`deep-research/docs/checklists/project_checklist.md`**: Actionable tracking for project milestones.
- **`deep-research/docs/phases/`**: Detailed theoretical justifications and implementation plans for each architectural pillar:
    - `phase1_vfs/`: Combating context rot via decoupled storage.
    - `phase2_planning/`: Externalized attention and SLM-driven traffic control.
    - `phase3_execution/`: Specialized reasoning nodes (Searcher/Analyst).
    - `phase4_verification/`: Adversarial validation and self-healing loops.
    - `phase5_integration/`: LangGraph topology and Nothing-inspired UI components.

## 🛠️ Usage & Intent

This workspace serves as the **instructional foundation** for the project. Future interactions should:
1.  **Respect the Architecture:** Refer to the phase-wise docs before proposing implementation changes.
2.  **Maintain the Design System:** Adhere to the Nothing Design principles (Space Grotesk, Space Mono, monochromatic) for any UI/UX tasks.
3.  **Prioritize Grounding:** Ensure all proposed agent loops include the adversarial verification patterns described in Phase 4.

---
*Last updated: March 2025*
