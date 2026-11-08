---
name: review-code-quality
description: "Review code quality in any programming language when asked for a code review or an assessment of clarity, error handling, and duplication. Provide findings in English, ordered by impact, and make fixes when requested. Use for existing code or specific changes; do not use to explain programming concepts or build features without a review request."
---

# Code Review and Improvement

Review code in the context of its project. Write the report in English, preserving symbol names and commands. Respect any other language requested by the user.

## Define the Scope

- Read the project instructions, expected behavior, tool configuration, and tests relevant to the requested scope.
- When reviewing changes, inspect the diff, surrounding context, and relevant callers. Tie findings to the changes, and identify pre-existing issues separately when needed to understand them.
- When reviewing an entire project, start with entry points and important execution paths. State which files you actually covered; do not claim to have reviewed unread code.
- "Review" means report only. "Review and fix" authorizes edits and verification within the specified scope. Do not expand fixes into a redesign or public API change without a request.

## Review Criteria

1. **Behavioral correctness and error handling:** Trace inputs, outputs, failure paths, and cleanup. Look for swallowed exceptions, false success, edge cases, and possible data corruption. Evaluate behavior against the function's contract and usage, not unsupported assumptions.
2. **Clarity:** Look for names, control flow, or mixed responsibilities that make behavior ambiguous or changes error-prone. Do not present personal preferences as defects.
3. **Duplication:** Suggest consolidation when the same rule is repeated and its distribution causes inconsistent behavior or a concrete maintenance cost. Textual similarity alone does not justify a new abstraction.

Validate findings through callers, tests, or a reproducible example whenever possible. Distinguish facts from suspicions and state what remains unverified. Do not invent findings to fill a report; "No substantiated issues found within the reviewed scope" is an acceptable outcome.

## Prioritize and Report Findings

- **P0 - Critical:** A confirmed, widespread failure requiring immediate intervention, such as ongoing data loss. Do not use for hypothetical scenarios.
- **P1 - High:** A crash, data loss, or failure of a primary execution path under realistic usage conditions.
- **P2 - Medium:** Incorrect failure handling or an incorrect result in a specific case, or a maintenance problem with a clear impact.
- **P3 - Low:** A limited-impact clarity or duplication improvement. Place it under optional improvements unless it is a substantiated defect.

Order findings by impact, then likelihood. An error-handling issue may be P1 or P2 depending on its harm; do not assign priority based only on its category.

For each finding, provide `[priority] Specific title`, then `path:line`, the triggering condition, evidence, impact, and the smallest suitable fix. Keep line ranges narrow and verify line numbers against the version reviewed. Group symptoms with the same root cause.

Start with substantiated findings, followed by optional improvements, then verification and its limitations. Include a revision reference when reviewing an external repository. Do not describe the review as a comprehensive security audit.

## Fix and Verify

- When fixes are requested, make the smallest change that addresses the root cause while preserving the public contract and the user's existing changes.
- Add a regression test for a behavioral defect, and verify that it fails before the fix and passes afterward. Do not add superficial tests for a simple naming improvement.
- Run tests relevant to the change. Report the command, actual result, and anything that could not be run; unavailable tools do not count as success.
- Explain what was fixed and what remains, with reasons. If a fix requires a decision about undocumented behavior, ask for that decision before changing the behavior.

## Example Requests

- "Review this file for clarity, error handling, and duplication, and prioritize the findings."
- "Review the changes on this branch without modifying files."
- "Review and fix errors in this function, then run its tests."

For an example of review, repair, and verification, read [references/review-example.md](references/review-example.md) when a model is useful.
