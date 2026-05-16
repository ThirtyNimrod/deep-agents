# Project Checklist: Deep Research SLM Implementation

## Phase 1: Virtual Filesystem (VFS)
- [ ] Define workspace directory structure (`sources/`, `analysis/`, `output/`).
- [ ] Implement `write_file` tool for agents.
- [ ] Implement `read_file` tool for agents.
- [ ] Implement `list_files` tool for manifest tracking.
- [ ] Verify VFS isolation (context stays lean).

## Phase 2: Planning & Orchestration
- [ ] Define `ResearchState` schema in LangGraph.
- [ ] Implement `write_todos` planning tool.
- [ ] Configure `functiongemma:270m` as the Router.
- [ ] Create specialized prompt templates for the SLM Router.
- [ ] Test deterministic routing based on VFS state and `todo_list`.

## Phase 3: Execution Loop
- [ ] Implement `Deep Searcher` node using `gemma4:e2b`.
- [ ] Integrate Search APIs (Exa/Google).
- [ ] Implement `Data Analyst` node using `gemma4:e2b`.
- [ ] Test data extraction and markdown synthesis into `sources/` and `analysis/`.

## Phase 4: Verification & Refinement
- [ ] Implement `Verifier Node` using `gemma3:4b`.
- [ ] Create adversarial validation prompts (hallucination detection).
- [ ] Implement the `Verifier Feedback` loop in the graph.
- [ ] Test "self-healing" behavior (Router sending agent back to fix defects).

## Phase 5: Integration & UI
- [ ] Finalize the LangGraph cyclic topology.
- [ ] Implement CLI for live updates.
- [ ] Integrate Nothing-inspired UI components.
- [ ] Conduct end-to-end deep research test.
