# Phase 4: Verification & Refinement

## Theory: Adversarial Validation
A single agent "grading its own homework" often misses its own hallucinations. We implement an **independent Verifier Node** (`gemma3:4b`).

The Verifier doesn't perform research; it only audits. It cross-references the `output/` draft against the `analysis/fact_sheet.md` and `sources/`. If a claim in the report doesn't exist in the sources, it's flagged as an "Unverified Claim."

## Plan
1.  **Verifier Logic:**
    - Prompting: "Act as a hostile auditor. Find every claim that lacks a specific citation in the source clippings."
2.  **Feedback Loop:**
    - The Verifier writes to `verifier_feedback`.
    - The SLM Router sees this feedback and **resets** the status of the related todo item.
    - The loop repeats until the Verifier gives a "PASS" signal.
3.  **Self-Healing:** This ensures the final output is high-fidelity and grounded in reality.
