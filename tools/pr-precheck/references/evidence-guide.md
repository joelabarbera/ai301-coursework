# Evidence guide: where evidence lives in a PR package

## Plan fidelity (harness category: silent-drift)

Checks: `plan-fidelity`, `description-matches-diff`.

### Where it lives

In an eval package:

- The plan's scope lives in the "Plan context" block: the "Plan:"
  paragraph names the steps, the "Scope, one bounded change" line, the
  "Not in scope" non-goals, and the "Files:" list. Any deviation note
  appears there or in the candidate PR's description.
- What actually changed lives in "Candidate PR → Diff" (the `---
  a/` / `+++ b/` file headers and each `@@` hunk) and "Commits".
- The fidelity claims live in "Candidate PR → Title" and
  "Description" ("implements the plan exactly", "no changes beyond
  it", "tests added", "CHANGELOG entry included").

In live mode:

- The plan is `plan.md` in the working copy, including its
  `## Deviations` section (house-chain: the house plan).
- The change is `git diff main...HEAD`, and `git diff --stat
  main...HEAD` gives the file list; commits are `git log main..HEAD
  --oneline`.
- The claims are the draft PR title and description the student
  supplies.

### What good looks like

Every changed file and hunk maps to a step, file, or test the plan
names, or to a deviation that is written down with what changed and
why; nothing in the diff touches a non-goal; and every planned step is
in the diff or its absence is recorded. The description says what the
diff does and no more: a claim of exact fidelity sits beside a diff
with no extra hunks, and "tests added" sits beside a test file in the
diff.

Silent drift runs both ways. More than the plan: an unplanned
refactor, a dependency bump, a second file the plan never named. Less
than the plan: a planned step, file, or test missing with no note. A
description claiming more or less than the diff delivers is silent
drift, not a comms problem.

## Test evidence (harness category: not-tested)

Checks: `behavior-verified`, `repo-checks-run`.

### Where it lives

In an eval package:

- What must be proven lives in the "Plan context" block's "Test plan:"
  sentence (each scenario or failure mode, its command, and its
  expected-after) and its "Repro evidence" line (the original failing
  command and output).
- What was proven lives in "Candidate PR → Test evidence": commands
  with before and after output, named tests, and suite results ("cargo
  test passes (614 tests)"). New tests also show up as test files in
  the diff.
- The checks the repo requires live in the repo-facts block's
  "pull requests" and "contribution policy" lines.

In live mode:

- What must be proven is the test plan in `plan.md` and the repro it
  cites.
- What was proven is the captured terminal output the student supplies
  and any evidence pasted into the draft description's "Testing"
  section.
- The checks Path Review requires are in `docs/CONTRIBUTING.md`:
  `make lint`, `make typecheck`, `make test-unit`, `make
  test-integration`, and the frontend tests, with `make check && make
  test-unit` before pushing. CI ("all five jobs") cannot run until the
  PR opens, so before submission the local runs of those commands are
  the evidence, and the "CI is green" box stays unchecked.

### What good looks like

Each scenario the test plan names is re-run on the branch, and the
observed after-result is shown and matches the plan's expected-after:
for example `# before: DuplicateOptionError ... # after: parsed OK`,
or the exact error message and exit code the plan predicted. A
scenario that could not be run is named in the description with the
reason, and the issue's primary repro is still shown fixed. Each check
the plan or repo names shows its outcome: a command and its result, or
a pass count.

Not tested looks like "(none provided)", "tests pass" with no command
or result, "should fix it", "did not get a chance to test", a test
plan naming two failure modes with evidence for only one, or a claim
that CI is green on a PR that has not been opened.

## Diff quality (harness category: unreviewable)

Check: `diff-focused`.

### Where it lives

In an eval package, the change itself is "Candidate PR → Diff" (every
file header and `@@` hunk) and "Commits". Commit messages often name
the debris ("gofmt", "cleanup", "bump X").

In live mode, run `git diff main...HEAD` and `git log main..HEAD
--oneline` from the working copy. Only committed changes count;
uncommitted working-tree files are not part of the PR.

### What good looks like

The fix is visible in a small number of hunks, and every hunk
implements, tests, or documents that fix, including a changelog or doc
entry the repo requires. A reviewer can read the diff without
separating the change from noise.

The debris tells are: `print`, `console.log`, or `dbg!` leftovers;
commented-out blocks; dead code; formatting or whitespace churn on
lines the fix does not touch; a rewrite of an unrelated function in
another file; dependency, `go.mod`, `package.json`, or lockfile changes
the plan does not call for; and stray files (scratch notes, `.orig`
files, local config). In Path Review, also look for `# noqa` lines
"cleaned up" and bulk `ruff --fix` rewrites, which CONTRIBUTING.md
forbids in a bug-fix PR.

## Standards and comms (harness category: standards-wall)

Checks: `template-and-asks`, `disclosure-policy`,
`maintainer-direction`.

### Where it lives

In an eval package:

- The repo's asks live in the repo-facts block: the "pull requests"
  line (template sections and checklist items, or "no PR template" plus
  any asks the contribution docs make) and the "contribution policy"
  line (including any AI-use policy, or "no stated AI policy").
- Maintainer direction lives in "Thread highlights".
- The PR's response lives in the description (sections, checklist,
  issue reference, disclosure), the commits, and the diff (changelog
  entries, tests).

In live mode:

- The asks are in `.github/PULL_REQUEST_TEMPLATE.md`. Its sections are
  Summary, Issue (`Closes #<n>`), Changes, Testing (the checklist,
  including removing the `@pytest.mark.xfail` marker and any matching
  `pyproject.toml` suppression for a seeded bug), Screenshots / Demo
  (conditional), and Notes for Reviewers.
- `docs/CONTRIBUTING.md` adds Conventional Commit messages, the
  `<type>/<issue-number>-<slug>` branch name, Google-style docstrings
  on public functions, and tests with every code change.
- `scope.md` house rules add one PR per issue, from the fork's
  `fix/<n>-<slug>` branch, with every template section filled with
  real content, including disclosure where it applies.
- Maintainer direction is in the full issue thread from `gh issue
  view <n> --repo <scoped repo> --comments`.

### What good looks like

Every template section and checklist item has content specific to this
change, or "n/a" with a reason where the ask is conditional. Every
required artifact is in the diff (changelog entry, tests, removed
xfail markers). The issue is referenced the way the repo asks. Where a
disclosure policy exists, the description meets it in the policy's own
terms. Explicit maintainer direction in the thread is followed or
explicitly answered.

The standards wall looks like a repo that asks for a changelog entry or
a checklist and a PR that has neither, a template left as untouched
placeholder comments, a stated AI-disclosure requirement with no
disclosure, or a maintainer's "please don't change X" ignored. When
the repo states no template, no policy, and no direction, there is
nothing to meet, and these checks pass on that absence. Whether the
description's claims match the diff belongs to plan fidelity, above.
