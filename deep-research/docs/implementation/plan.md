# Deep Research Implementation Plan

This document outlines the phased implementation of the Deep Research architecture using ultra-small SLMs and a decoupled state management system.

## 1. Model Roles & Assignments

| Role | Model | Description |
| :--- | :--- | :--- |
| **SLM Router** | `functiongemma:270m` | High-speed, deterministic routing between graph nodes based on lean state. |
| **Task Planner** | `ministral-3:3b` | Manages the dynamic `todo_list` and sub-task decomposition. |
| **Execution Nodes** | `gemma4:e2b` | Handles complex reasoning, tool use (search/scrape), and content synthesis. |
| **Verifier Node** | `gemma3:4b` | Adversarial validation; cross-references generated reports against raw source files. |

## 2. Phase 1: Virtual Filesystem (VFS) & Tools
Establish the decoupled workspace to prevent context rot.

*   **Workspace Structure:** `workspace/research/{session_id}/`
    *   `sources/`: Raw web scrapes and PDF extracts.
    *   `analysis/`: Intermediate synthesis and data tables.
    *   `output/`: Final report drafts.
*   **Core Tools:**
    *   `write_file(path, content)`: Primary output for execution nodes.
    *   `read_file(path)`: Targeted data retrieval for synthesis.
    *   `list_files(dir)`: Manifest tracking for the SLM Router.

## 3. Phase 2: Planning & Orchestration
Implement the state-aware routing logic.

*   **State Schema:**
    ```python
    class ResearchState(TypedDict):
        todos: List[str]
        workspace_manifest: List[str]
        current_focus: str
        verifier_feedback: Optional[str]
    ```
*   **SLM Router Node:**
    *   Prompt optimized for `functiongemma:270m` using structural tags.
    *   Logic: If `todos` has pending search -> `search_node`. If sources exist but no analysis -> `analyst_node`. If verifier feedback exists -> `refinement_node`.

## 4. Phase 3: Execution Loop (Deep Searcher & Analyst)
Implement nodes powered by `gemma4:e2b`.

*   **Deep Searcher:**
    *   Tools: Google Search / Exa API.
    *   Output: Markdown files in `sources/` containing URL, snippet, and cleaned text.
*   **Data Analyst:**
    *   Reads `sources/*.md`.
    *   Extracts key facts, statistics, and contradictions.
    *   Saves to `analysis/fact_sheet.md`.

## 5. Phase 4: Verification & Refinement
Close the loop with automated quality control.

*   **Verifier Node:**
    *   Reads `output/draft.md` and `analysis/fact_sheet.md`.
    *   Checks for: Hallucinations, missing citations, logical gaps.
    *   Output: Structured JSON feedback for the Router.
*   **Healing Loop:** If verification fails, the SLM Router re-targets the Searcher or Analyst to address specific gaps.

## 6. Phase 5: Integration
Connect nodes in LangGraph and deploy.

*   **Graph Definition:** Cyclic graph with conditional edges driven by the 270M Router.
*   **Interface:** CLI-based researcher that shows "live" updates of the `todo_list` and VFS manifest.
