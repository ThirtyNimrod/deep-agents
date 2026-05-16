# Phase 2: Planning & Orchestration

## Theory: Externalized Attention
Relying on a model's "latent attention" to remember its place in a 10-step plan is prone to failure. Deep Agents use a **Structured Tracking Tool** (the `todo_list`) to maintain explicit state.

The **SLM Router** (`functiongemma:270m`) acts as the "Traffic Cop." It is too small to do research, but it is highly optimized for **deterministic logic**. By feeding it only the lean state (todos + file manifest), it can instantly decide the next node without the latency or cost of a larger model.

## Plan
1.  **Planning Tool:** Implement `write_todos` powered by `ministral-3:3b`. This agent breaks the user query into sub-tasks.
2.  **State Mapping:**
    - If `todos` has pending search tasks -> Route to `search_node`.
    - If `sources/` exists but `analysis/` is empty -> Route to `analyst_node`.
    - If `output/` is ready -> Route to `verifier_node`.
3.  **SLM Optimization:** Use specialized chat templates with `<start_function_call>` tags to ensure the 270M model remains within structural constraints.
