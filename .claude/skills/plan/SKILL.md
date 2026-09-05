---
name: plan
description: Full planning workflow — branch, plan mode, implement, archive. Use for any non-trivial change.
---

Follow this workflow whenever the user wants to plan and implement a change.
Apply @docs/guidelines/ai-collaboration.md throughout — it is not optional
reading, it governs every step below.

## Step 1 — Clarify
If the user hasn't described what they want precisely enough to plan against,
ask them now before proceeding. Don't guess at ambiguous requirements.

## Step 2 — Create a branch
Before writing any code, create and check out a new git branch. Use the branch
naming convention from @docs/guidelines/git-workflow.md:
  <type>/<short-description>
Types: feat/, fix/, chore/, docs/, refactor/, test/
Example: feat/task-list-api

Do NOT start implementing on main.

## Step 3 — Plan
Enter plan mode. Explore the codebase and design the implementation.

The plan must include:
- The approach, and what alternatives were considered and rejected, and why
  (per the guidelines' "Proposing Alternatives" rule — this is not optional,
  even for a plan that feels obvious).
- Explicit acceptance criteria: what must be true for this to be done.
- What is explicitly out of scope for this increment.

Present the plan and wait for the user to approve it. Only once they have:

1. Exit plan mode with the approved plan content.
2. Write that content to docs/plans/current-plan.md (overwrite if it already
   exists from a prior increment). This is the canonical location for the
   in-progress plan — the review skill reads from this exact path, so it must
   exist before implementation begins. The file is gitignored; the archived
   copy written in Step 6 is the durable record.

Do not write any code — including the plan file — before that approval.

## Step 4 — Implement
Execute the approved plan exactly as approved. Implement exactly what was
scoped — no gold-plating, no unrequested extras. If something adjacent looks
broken or suboptimal, flag it to the user rather than fixing it silently.

Keep changes small. If the task is larger than expected mid-implementation,
stop and confirm direction with the user before continuing, per the
incremental-changes rule.

Write tests alongside or after implementation per the Test Requirements table
in the guidelines. No new logic ships without tests.

## Step 5 — Verify definition of done
Before archiving, confirm every item in the guidelines' Definition of Done:
build succeeds, all tests pass, lint and format checks pass. Do not proceed
to archiving on a red build or a "should be fine."

Stop here and tell the user: "Implementation complete and definition of done
verified. Run /review-implementation before archiving." Do not proceed to
Step 6 until the user confirms the review has been run and issues addressed.

/review-implementation checks the diff against the plan — scope, acceptance
criteria, missing work. It is not a correctness audit. For anything with
non-trivial logic, suggest /code-review as well; the two are complementary.

## Step 6 — Archive the plan
1. List docs/plans/ to find the highest existing plan number.
2. Copy docs/plans/_template.md to docs/plans/NNNN-<slug>.md, where NNNN is
   the next number.
3. In the new file, replace the
   `<!-- Copy the implemented session plan verbatim above this line, then
   adjust the frontmatter. -->` comment with the full content of
   docs/plans/current-plan.md, then remove the comment itself. Preserve all
   design decisions, context, and detail exactly as implemented, including
   the alternatives considered in Step 3 — do not summarize or rewrite.
4. Update the frontmatter: set `created` to the date work started and
   `updated` to today.
5. Delete docs/plans/current-plan.md now that it's archived, so the next
   increment starts clean and the review skill never reads a stale plan.
6. Commit the archive file together with any other final tidy-up commits.