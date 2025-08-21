Perfect — we can update the prompt so that the **validation report is generated in a structured markup format** (Markdown or similar), making it readable, navigable, and easy to reference. Here’s the updated version of your prompt:

---

# **Objective**

Perform an **end-to-end validation** to confirm that the **generated application (`original-code/`)** (RHS) completely and correctly implements **all requirements from the structured prompts (`V1.1` – `V7` in `commonPrompts/`)** (LHS).

Validation should:

* Map **every instruction in prompts (LHS)** to its **implementation in code (RHS)**
* Detect **missing, partial, or incorrect implementations**
* Flag **extra code** not supported by prompts
* Provide **concrete improvement suggestions**

**Deliverable:** A **detailed validation report in markup language (Markdown)**.

---

# **Folder Structure Context**

* **Root folder**:

  * `CAPABILITY_NAME/` (e.g., `eKYC/`)

    * `original-code/` → Primary application (RHS)
    * `mock-code/` → Skip
    * `original-prompt/` and `mock-prompt/` → Skip
  * `commonPrompts/` → Source of truth (LHS)

**Analyze only:**

* `original-code/`
* `commonPrompts/`

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