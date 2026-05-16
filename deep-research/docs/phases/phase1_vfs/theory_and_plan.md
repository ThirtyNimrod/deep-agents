# Phase 1: Virtual Filesystem (VFS)

## Theory: Combating Context Rot
In traditional agent architectures, every tool output is returned to the chat context. In a deep research task, scraping multiple websites or reading PDFs quickly bloats the context window.
**The result:**
- Model reasoning degrades.
- Hallucinations increase.
- Token costs skyrocket.
- Attention "rots" as history becomes noise.

**The Solution:** The Virtual Filesystem (VFS) decouples data storage from the reasoning context. The model treats the VFS as a "shared workspace" (like a developer uses a terminal and an editor). It only reads specific files when it is ready to analyze them, keeping the main loop extremely lean.

## Plan
1.  **Structure:** Initialize a persistent or session-based folder structure.
    - `/sources/`: Raw data, clippings, search results.
    - `/analysis/`: Extracted facts, data tables, theme mappings.
    - `/output/`: Drafts and final reports.
2.  **Tools:**
    - `write_file(path, content)`: Agents save their findings here instead of printing them.
    - `read_file(path)`: Agents pull in content for synthesis.
    - `list_files(dir)`: The Router checks this to see what progress has been made.
3.  **Verification:** Ensure that agents do NOT return massive blobs of text to the `ResearchState`.
