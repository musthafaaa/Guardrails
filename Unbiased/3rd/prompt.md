# **Objective**

Perform an **end-to-end validation** to confirm that the **generated application (`original-code/`)** (RHS) completely and correctly implements **all requirements and instructions from the structured prompts (`V1.1` – `V7` in `prompts/`)** (LHS).

This validation should:

* Map **every instruction in prompts (LHS)** to its **implementation in code (RHS)**
* Detect any **missing, partially implemented, or incorrectly implemented** requirements
* Highlight **hallucinations or extra code not specified in prompts**
* Capture **any errors in the RHS code** (e.g., compilation or runtime errors)
* Provide **improvement suggestions** for each violation

The final output must be a **comprehensive, narrative-style validation report**.

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

## **1. Parse Prompts (LHS)**

* Read all prompt files (`V1.1` – `V7`) line by line.
* For each instruction:

  * Assign a unique identifier → `P<file>-L<line>`
  * Summarize the requirement in clear, plain terms

---

## **2. Compare LHS vs RHS**

* Inspect `original-code/` for each requirement.

* For each requirement, document:

  * Implementation status: Fully implemented, partially implemented, missing, or incorrect
  * Evidence: file path and relevant code snippet
  * Any **errors detected** in the RHS code, including:

    * Error type (compilation/runtime)
    * File name
    * Line number
    * Code snippet causing the error

* Flag **extra code in RHS** that is not linked to any LHS requirement

---

## **3. Narrative Report Generation**

Produce `CAPABILITY_NAME/end-to-end-validation-report.txt` with the following sections:

1. **Requirement Validation**

   * For each requirement, describe in narrative form:

     * Requirement summary
     * Status of implementation
     * Evidence from code
     * Any errors encountered (file, line, snippet)
     * Notes on partial or incorrect implementations

2. **Extra/Unexpected Code**

   * Describe any RHS code not covered by LHS
   * Include file names, code snippets, and possible implications

3. **Improvement Suggestions**

   * Recommendations for fixing missing or incorrect implementations
   * Recommendations for fixing code errors
   * Suggestions to refine prompts if ambiguity caused misimplementation

---

# **Key Notes**

* Validation must be **deep and exhaustive** — every line in prompts (LHS) should be mapped to RHS.
* Report should be **narrative, detailed, and auditable**, without tables.
* Capture **all errors**, including file, line number, and snippet.
* No testing guardrails — **pure LHS vs RHS alignment check**.

---
