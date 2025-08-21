# **Objective**

Perform an **end-to-end validation** to confirm that the **generated application (`original-code/`)** (RHS) completely and correctly implements **all requirements and instructions from the structured prompts (`V1.1` – `V7` in `prompts/`)** (LHS).

This validation should:

* Map **every instruction in prompts (LHS)** to its **implementation in code (RHS)**
* Detect any **missing, partially implemented, or incorrectly implemented** requirements
* Highlight **hallucinations or extra code not specified in prompts**
* Provide **improvement suggestions** for each violation

The final output must be a **comprehensive validation report**.

---

# **Folder Structure Context**

* **Root folder**:

  * `CAPABILITY_NAME/` (e.g., `eKYC/`)

    * `original-code/` → **Primary application (RHS to validate)**
    * `mock-code/` → Third-party mock services (skip)
    * `original-prompt/` and `mock-prompt/` → Skip
  * `prompts/` → Contains structured prompts (`V1.1`–`V7`) → **Source of truth (LHS)**

**Analyze only:**

* `original-code/` (RHS implementation)
* `prompts/` (LHS requirements)

**Skip:**

* `mock-code/`
* `original-prompt/`
* `mock-prompt/`

---

# **Validation Workflow**

## **1. Build Prompt–Requirement Matrix (LHS)**

* Parse all prompt files (`V1.1` – `V7`) line by line.
* For each instruction:

  * Assign unique ID → `P<file>-L<line>`
  * Record requirement in plain business/technical terms

---

## **2. Compare LHS vs RHS**

For each requirement in the matrix:

* Inspect `original-code/` for corresponding implementation.
* Mark status as:

  * Fully Implemented
  * Partially Implemented
  * Missing
  * Incorrect or contradicting prompt

Additionally:

* Flag **extra code in RHS** that is not backed by any LHS requirement.

---

## **3. Report Generation**

Produce `CAPABILITY_NAME/end-to-end-validation-report.txt` containing:

1. **Prompt–Implementation Mapping Table**

   * Prompt ID
   * Requirement summary
   * Implementation status
   * Evidence (file + code snippet reference)

2. **Violation Report**

   * List of all missing/partial/incorrect/extra implementations
   * Root cause (hallucination, skipped instruction, misinterpretation, etc.)

3. **Improvement Suggestions**

   * Specific recommendations for fixing gaps in implementation
   * If needed, suggestions to refine prompt phrasing to avoid ambiguity

---

# **Key Notes**

* Validation must be **deep and exhaustive** — every line in prompts (LHS) should be mapped to RHS.
* Report should be **detailed and auditable**, not a high-level summary.
* No testing guardrails — **pure LHS vs RHS alignment check**.

---