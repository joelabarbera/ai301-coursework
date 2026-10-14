# Procedure: how this tool grades a PR package

## Read order

Read the package in this order, and do not grade any check until the
whole package has been read. The order builds the expectation (what
the plan says should change and how it should be proven) before you
see what the PR actually did, and reads the description last so its
claims cannot shape how you read the diff.

1. **Repo facts and stated asks.** In eval mode, read the repo-facts
   block. In live mode, read `.github/PULL_REQUEST_TEMPLATE.md`,
   `docs/CONTRIBUTING.md`, and the house rules in `scope.md`. Write
   down an **asks list**: every PR template section and checklist
   item, every required artifact (changelog entry, tests, removed
   xfail markers, issue reference), every named check (suite, lint,
   typecheck, CI), any commit convention, and any AI-use or
   disclosure policy. Mark which asks are conditional ("if
   applicable").
2. **Issue and thread.** Read the issue body and the thread highlights
   (live: `gh issue view <n> --repo <scoped repo> --comments`). Write
   down the reported behavior and expected behavior, and add any
   explicit maintainer or collaborator direction on how to fix,
   scope, test, or submit to a **direction list**, quoted.
3. **Plan context.** Read the plan and the repro evidence it built on
   (live: `plan.md`, including `## Deviations`, and the repro it
   cites). Write down a **plan ledger**: each planned step, each file
   or area to touch, each explicit non-goal, and each recorded
   deviation. Write down a **test-plan ledger**: each scenario or
   failure mode the test plan names, its command or steps, and its
   expected-after result, plus any suite or check the plan says to
   run.
4. **Commits and diff.** Read the commit list, then the unified diff
   (live: `git log main..HEAD --oneline` and `git diff main...HEAD`).
   Write down a **diff ledger**: one row per changed file, and per
   hunk where a file has more than one, with a one-line note on what
   the hunk does.
5. **Test evidence.** Read the test-evidence section (live: the
   captured output the student supplied, plus any evidence quoted in
   the draft description). Write down each command or test shown, its
   before result if given, and its observed after result.
6. **Title and description, last.** Read the PR title and
   description. Write down a **claims list**: each factual claim about
   what changed, what did not change, fidelity to the plan, tests
   added, checks run, and results; each deviation or shortfall it
   discloses; and each section it fills against the asks list.

## Evidence gathering

Run these pairings against the ledgers from the read order. Each
pairing feeds the named check; record the fact or quote that will
decide it.

1. **Diff against plan** (`plan-fidelity`). Classify each diff-ledger
   row as one of: implements a planned step; tests the change;
   documents the change as the repo requires; covered by a recorded
   deviation; or outside the plan. Then walk the plan ledger the other
   way and mark each planned step and file as present in the diff,
   absent with a recorded deviation, or absent with no note. Record
   every "outside the plan" row and every "absent with no note" step.
   A deviation counts as recorded only if the plan's deviation notes
   or the PR description state what changed and why.
2. **Description against diff** (`description-matches-diff`). For each
   entry on the claims list, find the diff hunk, commit, or evidence
   line that confirms or contradicts it. Record each contradiction
   (for example, "implements the plan exactly" beside a hunk outside
   the plan; "tests added" with no test file in the diff). Then walk
   the diff ledger and record any behavior-changing hunk the
   description never mentions.
3. **Tests against test plan** (`behavior-verified`). For each
   test-plan-ledger scenario, find the evidence entry that re-runs it
   on the branch and compare the observed after-result with the plan's
   expected-after. Record each scenario as shown-matching,
   shown-mismatching, disclosed-not-run (with the stated reason), or
   missing. Note separately whether the issue's primary repro is shown
   fixed. "Tests pass", "should fix it", and "looks right" are not
   observed after-results.
4. **Evidence against required checks** (`repo-checks-run`). For each
   check named in the test-plan ledger or the asks list, find its
   outcome in the evidence (a command with its result, or a stated
   pass count). Record each as shown-passing, shown-failing, or not
   shown. In live mode, record the local runs of `make lint`,
   `make typecheck`, and `make test-unit` (and `make
   test-integration` and the frontend tests when the diff touches
   them) in place of CI, and record any description claim that CI is
   green.
5. **Diff for debris** (`diff-focused`). Re-walk the diff ledger and
   record any hunk that is debug output, commented-out code, dead
   code, formatting or whitespace churn on lines the fix does not
   change, a refactor of code the fix does not need, or a dependency,
   lockfile, or version change the plan does not call for. Record the
   commit that introduced each one when the commit list shows it.
6. **PR against asks** (`template-and-asks`). For each entry on the
   asks list, record where the description, commits, or diff meets
   it, or that it is missing or left as boilerplate. A conditional
   ask answered "n/a" with a reason counts as met.
7. **Description against policy** (`disclosure-policy`). If the asks
   list has an AI-use or disclosure policy, record the policy's exact
   requirement and the description text that meets or misses it. If
   there is none, record "no stated policy".
8. **PR against direction** (`maintainer-direction`). For each entry
   on the direction list, record the hunk or description sentence
   that follows or addresses it, or that it is ignored or
   contradicted. If the list is empty, record "no explicit
   direction".
9. **Preferred checks.** Record each commit message from the commit
   list and the title as written.

When it is unclear where a piece of evidence lives, look it up in
`references/evidence-guide.md`. Do not infer evidence the package does
not contain from what a good PR would normally include.

## Check execution

1. Grade checks in rubric order: `plan-fidelity`,
   `description-matches-diff`, `behavior-verified`, `repo-checks-run`,
   `diff-focused`, `template-and-asks`, `disclosure-policy`,
   `maintainer-direction`, then the preferred checks `commit-messages`
   and `title-specific`. Grade every check; do not stop at the first
   failure.
2. Grade each check only from the evidence its rubric row names and
   the record its evidence-gathering pairing produced. Do not let a
   fact from another check's evidence decide this one.
3. Grade `pass` only when the recorded evidence establishes the pass
   condition. Grade `fail` when the recorded evidence shows the pass
   condition is violated. Grade `unclear` only when evidence the check
   needs is genuinely absent or ambiguous and neither pass nor fail is
   established.
4. When a check's trigger is absent (no stated template or asks, no
   AI policy, no maintainer direction, no named checks), grade it
   `pass` and use the absence as its evidence line. When the trigger
   is present but the evidence to verify it is missing (for example,
   the plan names a scenario and there is no test evidence for it),
   grade `fail`.
5. One fact may decide more than one check when it meets each check's
   own condition (an unrelated refactor can fail `plan-fidelity`,
   `diff-focused`, and, if the description claims "no changes beyond
   the plan", `description-matches-diff`). Grade each check on its own
   condition; do not skip one because another already failed.
6. Once a check's pairing is recorded, grade from the record. Re-read
   the package only to resolve a specific conflict between two
   recorded facts.
7. Write one evidence line per check: the fact or quote that decided
   it (a file path and what the hunk does, a quoted claim, a test-plan
   scenario and its observed result, a named ask). Never write a
   restatement of the pass condition as evidence.

## Verdict assembly

1. Apply the verdict rule in `rubric.md`: accept only if every
   required check is `pass`; reject if any required check is `fail` or
   `unclear`, counting `unclear` as `fail`.
2. Preferred-check grades are reported and never change the verdict.
3. Pick the deciding check: on reject, the first required check in
   rubric order graded `fail` or `unclear`. On accept, there is no
   failing check; name `plan-fidelity` as the deciding check and quote
   its evidence, since fidelity to the plan is what makes the PR
   submittable.
4. Write the summary: one line per check with its grade and evidence,
   then the deciding check and its evidence quoted, then any
   procedure gaps met during the run, then (live mode only)
   voice-guide notes.
5. Emit the JSON block last: `item` per SKILL.md, one `checks` entry
   per rubric check in rubric order with the same grade and evidence
   line as the summary, and `verdict` equal to the result of step 1.
   Confirm the JSON verdict matches the grades above it before
   emitting it.
