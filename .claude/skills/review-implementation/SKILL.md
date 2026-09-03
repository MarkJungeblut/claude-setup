---
name: review-implementation
description: Independently review the current implementation against its plan for correctness, edge cases, and scope creep
context: fork
agent: Explore
background: false
disable-model-invocation: true
---

## Plan for this increment
@docs/plans/current-plan.md

## Implementation diff
!`git diff HEAD`

## Changed files
!`git diff --name-only HEAD`

## Your task

You are reviewing this implementation as an independent reviewer with no
prior context on this project beyond what's above. Do not assume anything
was discussed elsewhere — evaluate only against the plan and the diff.

1. Does the diff actually implement what the plan describes? Flag anything
   missing, anything added that wasn't in the plan (scope creep), and
   anything that diverges from the stated approach.
2. Check the plan's acceptance criteria one by one — does the code satisfy
   each, explicitly? Report pass/fail per criterion.
3. Look for edge cases the plan didn't anticipate: empty/null inputs,
   error paths, boundary conditions, race conditions.
4. Flag anything over-engineered relative to what the plan called for.
5. Check test coverage: do the tests assert behavior described in the plan's
   acceptance criteria, or do they merely mirror what the implementation
   currently does? Flag any test whose expected values look like they were
   derived from running the code rather than from the plan.

Report findings as a short list: pass/fail per acceptance criterion, then
any additional issues found, each with the file and line. Do not modify any
files — report only.