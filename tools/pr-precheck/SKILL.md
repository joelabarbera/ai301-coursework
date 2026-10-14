---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

Answer exactly one question about exactly one PR package: **is this
ready to submit?**

A PR package is a candidate pull request: its title, its description,
its commits, its diff, and its test evidence. Read it against two
things: the plan it claims to implement (including that plan's
deviation notes) and the issue that plan belongs to (the thread, the
reproduction behind it, and the repo's stated asks for pull requests).

Do not answer any other question. Do not review the code for general
quality, propose fixes, rewrite the description, grade the plan or the
repro as if they were the object, or grade more than one package per
run. If you are handed more than one package, stop and ask which one
to grade. Do not answer from gut feel: answer by executing the
components in this directory, as described under "Component reads".

## Inputs and modes

Decide the mode before reading anything else. If you were handed a
package bundle file, run in eval mode. Otherwise, run in live mode.

**Live mode** grades the student's own submission before it goes out.
Run from the student's working copy and gather these inputs:

1. **The plan**: `plan.md` in the working copy, deviation notes
   included. The deviation notes are part of the plan; read them as
   scope, not as commentary.
2. **The branch's diff**: run `git diff main...HEAD` (three dots) from
   the working copy. This is everything the branch changes relative to
   the repo's default branch, and it is the only diff you grade. Also
   run `git log main..HEAD --oneline` to get the commit list. Do not
   substitute a two-dot diff, the working tree's uncommitted changes,
   or a diff against any other base; uncommitted changes are not part
   of the PR.
3. **The draft PR title and description**: the text the student
   supplies for the pull request they are about to open (pasted into
   the conversation or in a file they name). Grade this text as
   written; it is what a maintainer will read.
4. **The test evidence**: the captured test output and before/after
   proof the student supplies, plus any test evidence quoted in the
   draft description.
5. **The issue**: identify the issue number from the plan and the
   branch name (`fix/<issue-number>-<slug>`). If they disagree, report
   the mismatch and grade against the issue the plan names. Read the
   full issue thread from the scoped repo with
   `gh issue view <number> --repo <scoped repo> --comments`, including
   any explicit maintainer direction posted there.
6. **The repo's stated asks**: the PR template at
   `.github/PULL_REQUEST_TEMPLATE.md` and the contributing rules at
   `docs/CONTRIBUTING.md`, both read from the working copy, including
   any AI-use disclosure policy they state.

A house-chain student reads the house plan and the house repro pack in
place of their own `plan.md` and posted repro; every check grades the
same things against them.

If the draft PR title and description are missing, or
`git diff main...HEAD` is empty, there is no candidate PR to grade:
stop and tell the student what to supply. Any other missing input is
not a reason to stop; it is evidence, and the checks that need it
grade its absence.

**Eval mode** grades a package bundle. The bundle is the whole world:
take every fact from the bundle text and nothing else. Do not fetch
anything, do not run git or `gh`, and do not read the working copy,
`scope.md`, or `voice-guide.md`. Always grade a complete package: run
every check in `rubric.md` and apply the full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before any other
input.

- Find the `Repo:` line. Ignore HTML comments on that line. If the
  value is still a bracketed placeholder rather than an
  `owner/repo` name, stop without grading and tell the student to fill
  the `Repo:` line in `scope.md` with their section's Path Review repo.
  Never guess a scope.
- Confirm the PR targets the scoped repo: the working copy must be the
  scoped repo or a fork of it, and the issue from the inputs must live
  in the scoped repo. If either is outside scope, refuse to grade and
  say which fact put it outside.
- Apply the house rules in `scope.md` as rules of the environment when
  reading evidence: the PR comes from the student's own fork's
  `fix/<issue-number>-<slug>` branch against the default branch, one
  bounded PR per issue, the template always used with real content in
  every section, a classmate's PR on the same issue never counts
  against this one, and what happens after the PR opens is not graded.

In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, read `voice-guide.md` after `scope.md` and before
grading. Hold the outgoing PR text, the draft title and the draft
description, against each rule in the guide. Report every rule the
draft breaks in the summary: name the rule, quote the offending
words, and show the guide's "Right" pattern it should follow.

Never let the voice guide change the verdict on its own. It is the
student's personal style, not a shared standard; only a check in
`rubric.md` that explicitly reads it may move the verdict.

In eval mode, ignore `voice-guide.md` entirely: voice is personal and
carries no gold labels, and the universal communication-quality checks
live in the rubric.

## Component reads

Read and use the components in these roles:

- `rubric.md` decides **what**: its checks table (check name, evidence,
  pass condition, weight) and its verdict rule. Grade every check it
  lists and no check it does not list; use each check's name exactly
  as written in the output JSON.
- `references/evidence-guide.md` decides **where**: for each evidence
  family (plan fidelity, test evidence, diff quality, standards and
  comms) it maps where the evidence lives in a bundle and, live, in
  the working copy and on GitHub, and what good looks like there.
- `procedure.md` decides **how**: the read order, the gathering moves,
  how a check executes, and how grades become the verdict. Execute it
  as written, in order.

Where the procedure is silent on a step you need, do not improvise
around it. Take the smallest step the rubric and evidence guide make
unavoidable, and report the gap in the summary so the student can fix
the procedure.

Check for content before grading. Ignore HTML comments and headings
when deciding whether a file has content; only written text counts. If
`rubric.md` has no filled check row, or `procedure.md` has no written
steps, refuse to grade: say which file is empty and stop. Do not
invent checks or steps to fill the hole.

Refuse to grade, and say why, in exactly these cases: the rubric or
procedure is empty; live mode and the scope's `Repo:` line is a
placeholder; live mode and the PR or issue lies outside the scoped
repo; there is no candidate PR (no draft title and description, or an
empty diff); more than one package was handed in. A refusal emits no
verdict and no JSON block.

## Verdict and output

The verdict is binary: `accept` means the package is ready to submit;
`reject` means hold it. There is no third verdict, no "accept with
reservations", and no score. Put reservations in check evidence lines
or the summary, never in the verdict.

Before the JSON block, show a short readable summary: one line per
check with its grade and deciding fact, the deciding check the
procedure names for the verdict, any procedure gaps, and (live mode)
any voice-guide notes. Then end the reply with this fenced JSON block,
valid, with one entry per rubric check, and nothing after it:

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

Set `item` to the bundle id in eval mode. In live mode, the PR does
not exist yet: set `item` to the scoped repo, issue number, and branch
(for example `owner/repo#72 fix/72-slug`). The harness parses the last
fenced JSON block in the reply, so emit exactly one, keep it last, and
do not alter, extend, or reorder the schema.

## Grading discipline

- **Evidence first.** Never grade a check without naming the fact or
  quoting the line that decided it: a file path from the diff, a
  sentence from the plan, a section of the template, a line of test
  output. "Looks fine" is not evidence.
- **Grade the thing, not the polish.** Read the diff against the plan
  and its deviation notes, the test evidence against the plan's test
  plan and the repo's checks, and the description against the diff.
  A terse complete PR can be ready; a confident, well-formatted one can
  be hiding drift. Never grade length, formatting, or commit count.
- **Honor honest outcomes.** A PR that discloses a shortfall or a
  deviation, and whose plan records it, can be ready. Do not treat
  "less than everything" as a reason to hold.
- **The rubric decides, not you.** If a check passes by its stated
  condition but feels wrong, grade it pass and note the tension in the
  summary; the fix belongs in the rubric, not in the run.
- **The procedure decides how, not you.** Follow `procedure.md` as
  written and report its gaps instead of silently inventing steps.
- **Unclear defaults to fail.** Treat `unclear` as the rubric's verdict
  rule directs. Where that rule is silent, treat `unclear` as `fail`:
  a claim you cannot verify from the package is a failing one, and a
  PR you cannot verify is not ready to submit.
