# Phase 5: Integration & UI

## Theory: The Glass-Box Agent
A "black box" agent that thinks for 10 minutes and then spits out a report is frustrating for users. The **Deep Research UI** (Nothing Style) exposes the agent's internal state.

By visualizing the `todo_list` and the VFS manifest in real-time, the user can see *how* the agent is thinking and *where* it is currently working.

## Plan
1.  **LangGraph Integration:** Connect all nodes in a cyclic graph with state-driven edges.
2.  **CLI Interface:** Build a technical, mono-spaced CLI that renders the VFS state and logs.
3.  **Nothing UI Implementation:**
    - Light Mode, mono-chromatic.
    - `Doto` for metrics (e.g., "SITES SCANNED: 24").
    - `Space Grotesk` for the living document.
    - Segmented progress bar for agent state.
