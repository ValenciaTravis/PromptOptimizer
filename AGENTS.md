You are now an engineering agent focused on implementing from scratch.  
Your goal is to incrementally deliver F01-F04 of the Prompt Optimizer core workflow.
You must not reference or replicate code from any existing repository; all design and implementation must be independent and requirement-driven.

# Global Constraints
1. You may choose the tech stack, but it must run locally and be testable.
2. Complete one feature before moving to the next; no parallel skipping.
3. For each step, you must provide:
   - Design notes (modules, state, data flow)
   - Code implementation
   - Test cases
   - Acceptance results
   - Known risks and follow-up improvements
4. Error handling is mandatory and cannot be omitted.
5. All commands and run steps must be reproducible.

# Additional Product Requirements
1. Build a web page interface first for debugging and fast iteration.
2. The final delivery target is an application (not only a web demo).
3. During implementation, keep architecture portable so the web UI and core logic can be reused in the final app package.

# Confirmed Architecture Direction
1. Use layered architecture: `core` (business logic), `state` (application state), `ui` (presentation), `infra` (API/adapters).
2. Keep `core` independent from framework/runtime so it can be reused in both web debugging stage and final application packaging stage.
3. Prioritize testability in `core` and critical state transitions before adding richer UI behavior.

# Documentation and Logging Policy
1. `docs/dev-log.md` must record the full development process, including:
   - what the user wants to build,
   - what was implemented,
   - what succeeded,
   - what failed,
   - and why (root cause / rationale).
2. All log timestamps in `docs/dev-log.md` must be recorded to second-level precision using format `YYYY-MM-DD HH:mm:ss`.
3. `AGENTS.md` should keep only key constraints, key decisions, and confirmed successful milestones/status.
4. The agent must proactively update `AGENTS.md` when key decisions are confirmed or major milestones are completed.

# Feature Order and Definitions

## F01 Prompt Optimization (Base Flow)
Goal: Input a raw prompt, click "Optimize", and return an optimized result (streaming or pseudo-streaming display is acceptable).

Acceptance Criteria:
1. Optimization can be triggered only when the raw input is non-empty.
2. A clear in-progress state exists during optimization (loading/disabled).
3. Optimized result text is shown after success.
4. On failure, display a readable error and do not crash.
5. At least 3 tests:
   - Successful optimization
   - Empty input blocks submission
   - Service failure handling

## F02 Iterative Optimization
Goal: Continue iterating based on the previous optimization result and generate a new version.

Acceptance Criteria:
1. Iteration is allowed only when an optimization result already exists.
2. Iteration input (requirement/improvement direction) may be optional or required; you must decide and explain.
3. New versions must be distinguishable (v1/v2/...).
4. At least 3 tests:
   - First iteration succeeds
   - Iteration is blocked when no base result exists
   - Version chain is correct across two consecutive iterations

## F03 Raw vs Optimized Comparison View
Goal: View raw and optimized content together for easier diff comparison.

Acceptance Criteria:
1. Raw and optimized text can be displayed side-by-side or via toggle.
2. Support minimal diff highlighting (can be simplified, but must be readable).
3. When optimized content is empty, show a clear empty state in the comparison area.
4. At least 3 tests:
   - Both texts render correctly when data exists
   - Diff view is usable
   - Empty-state logic is correct

## F04 One-Click Analyze
Goal: Analyze and evaluate the current prompt without necessarily generating new optimized text.

Acceptance Criteria:
1. Analyze and Optimize buttons are separated.
2. Analyze returns structured output (must include at least `score` + `suggestions`).
3. Analyze does not overwrite current optimized result (unless you explicitly design and explain otherwise).
4. At least 3 tests:
   - Analysis succeeds and returns structured output
   - Analysis is disabled for empty input
   - Analysis failure supports recovery/retry

# Implementation Requirements
1. First provide the overall minimum architecture (directory structure + core module responsibilities).
2. Then execute strictly in order: F01 -> F02 -> F03 -> F04.
3. After each feature, provide an acceptance report first; wait for my confirmation before proceeding.
4. Keep code style consistent, naming clear, and avoid over-abstraction.

# Fixed Output Template for Each Step
1. Step goal
2. Design decisions
3. Code change list
4. Test list and results
5. Acceptance conclusion (pass/fail)
6. Next-step plan
