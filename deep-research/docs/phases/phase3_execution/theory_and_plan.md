# Phase 3: Execution Loop

## Theory: Specialized Reasoning
Once the Router identifies a task, it hands execution to the "Reasoning Engine" (`gemma4:e2b`). Unlike the Router, these nodes have full tool-use capabilities and larger context windows.

Execution is split into two primary roles:
1.  **The Deep Searcher:** Focuses on breadth—finding information across the web.
2.  **The Data Analyst:** Focuses on depth—synthesizing and cross-referencing information already in the VFS.

## Plan
1.  **Deep Searcher:**
    - Parallel async calls to search providers.
    - Automatic cleaning of HTML to Markdown.
    - Storage in `sources/` with full metadata (URL, Date).
2.  **Data Analyst:**
    - Reads multiple files from `sources/`.
    - Identifies contradictions or gaps.
    - Outputs `fact_sheet.md` into `analysis/`.
3.  **Report Writer:** Synthesizes the analysis into a final coherent structure.
