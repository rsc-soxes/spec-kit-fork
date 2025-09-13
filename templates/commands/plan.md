---
description: Execute the implementation planning workflow using the plan template to generate design artifacts.
scripts:
  sh: scripts/bash/setup-plan.sh --json
  ps: scripts/powershell/setup-plan.ps1 -Json
---

Given the implementation details provided as an argument, do this:

1. Run `{SCRIPT}` from the repo root and parse JSON for FEATURE_SPEC, IMPL_PLAN, SPECS_DIR, BRANCH. All future file paths must be absolute.
2. Read and analyze the feature specification to understand:
   - The feature requirements and user stories
   - Functional and non-functional requirements
   - Success criteria and acceptance criteria
   - Any technical constraints or dependencies mentioned

3. Read and analyze the test cases from `{SPECS_DIR}/test-cases.md` to understand:
   - All defined test cases (TC-001, TC-002, etc.)
   - Test categories (Critical Path, Edge Case, Integration, Performance, Security)
   - Test scenarios with Given-When-Then format
   - Any non-testable scenarios flagged for manual verification

4. Read the constitution at `/memory/constitution.md` to understand constitutional requirements.

5. Execute the implementation plan template:
   - Load `/templates/plan-template.md` (already copied to IMPL_PLAN path)
   - Set Input path to FEATURE_SPEC and TEST_CASES_PATH to `{SPECS_DIR}/test-cases.md`
   - Run the Execution Flow (main) function steps 1-8
   - The template is self-contained and executable
   - Follow error handling and gate checks as specified
   - Let the template guide artifact generation in $SPECS_DIR:
     * Phase 0 generates research.md
     * Phase 1 generates data-model.md, contracts/, test-contracts.md, test-matrices.md, quickstart.md
     * Phase 2 planning (NOT execution) - tasks.md created by /tasks command
   - Load `/templates/test-contracts-template.md` and `/templates/test-matrices-template.md` for Phase 1
   - Incorporate user-provided details from arguments into Technical Context: {ARGS}
   - Update Progress Tracking as you complete each phase

6. Verify execution completed:
   - Check Progress Tracking shows all phases complete
   - Ensure all required artifacts were generated including test-contracts.md and test-matrices.md
   - Verify test coverage analysis shows acceptable coverage percentages
   - Confirm no ERROR states in execution

7. Report results with branch name, file paths, and generated artifacts including:
   - Generated test contracts with unit, integration, and end-to-end test scenarios
   - Test traceability matrices showing requirement-to-test and test-case-to-contract mappings
   - Coverage analysis and gap identification
   - Non-testable scenarios with explicit rationale

Use absolute paths with the repository root for all file operations to avoid path issues.
