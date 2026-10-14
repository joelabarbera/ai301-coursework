# Rubric: is this pull request ready to submit?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| plan-fidelity | The diff's changed files and hunks read against the plan's scope, files to touch, steps, and non-goals, plus any deviation note recorded in the plan or stated in the PR description with what changed and why. | Pass if every changed hunk implements, tests, or documents a step the plan names (or a recorded deviation), no hunk does work the plan lists as out of scope, and every planned step is either present in the diff or its absence is recorded as a deviation. Fail if the diff does more than the plan, or less than the plan, without a recorded deviation. A recorded, explained deviation passes. | required |
| description-matches-diff | Every factual claim in the PR title and description (what changed, what was not changed, "implements the plan exactly", which files, which tests were added, which checks ran) read against the diff, commit list, and test evidence. | Pass if no claim in the title or description is contradicted by the diff or test evidence, and the description does not omit a change in the diff that alters behavior. Fail if the description claims fidelity, scope, tests, or results that the diff or evidence contradicts or does not contain. | required |
| behavior-verified | The test evidence section (or, live, the captured test output) read against the plan's test plan and the repro evidence's failing steps. | Pass if, for every failure mode or scenario the plan's test plan names, the evidence shows the repro step re-run on the branch with an observed after-result that matches the plan's expected-after (a before/after pair, a named test asserting that behavior, or captured output). A scenario the contributor could not run passes only if the description explicitly discloses it and gives the reason, and the issue's primary repro is still shown fixed. Fail if evidence is absent, only says "tests pass" or "should fix it", or skips a named scenario without disclosure. | required |
| repo-checks-run | The test evidence read against the test commands the plan's test plan names and the checks the repo's contribution docs or PR template require (test suite, lint, typecheck, CI). | Pass if the outcome of each required check is visible in the evidence (a command with its result, or a stated pass count), or if neither the plan nor the repo names any check. In live mode, CI cannot run before the PR opens: the local equivalents the contribution docs name must show a result, and the description must not claim CI is green. Fail if a named required check has no visible outcome or shows a failure the description does not address. | required |
| diff-focused | Every hunk of the unified diff and every entry in the commit list. | Pass if every hunk is needed to implement, test, or document the change (including changelog or doc entries the repo requires), and the diff contains no debug output, commented-out code, dead code, formatting or whitespace churn on untouched logic, drive-by refactors, or dependency/lockfile changes the fix does not require. Fail if any such hunk rides along. | required |
| template-and-asks | The repo-facts block's PR template sections and contribution asks (live: the repo's PR template and CONTRIBUTING.md, plus scope.md house rules) read against the PR description, commits, and diff. | Pass if every section or checklist item the repo explicitly asks for is addressed with content specific to this change (an "n/a" with a reason is fine where the ask is conditional), every artifact the repo requires is present in the diff (for example a changelog entry, tests with behavior changes, removed xfail markers for a seeded bug), and the issue is referenced where the repo asks. Pass if the repo states no template and no asks beyond those already met. Fail if a stated ask is ignored or answered with untouched boilerplate. | required |
| disclosure-policy | The repo's stated AI-use or disclosure policy in the repo-facts block or contribution docs, read against the PR description. | Pass if the repo states no AI-use or disclosure policy, or if the description meets the policy as stated (discloses where disclosure is required; the contribution does not violate a stated prohibition). Fail if a stated policy applies and the description does not meet it. | required |
| maintainer-direction | The thread highlights (live: the full issue thread), filtered to explicit direction from maintainers or collaborators about how this issue should be fixed, scoped, tested, or submitted, read against the diff and description. | Pass if every explicit maintainer direction is followed by the diff, or the description explicitly addresses why it is not. Pass if the thread contains no such direction. Fail if the PR contradicts or ignores explicit direction. | required |
| commit-messages | The commit list. | Pass if each commit message names what that commit changes, and follows the repo's commit convention when one is stated. | preferred |
| title-specific | The PR title read against the diff. | Pass if the title names the behavior the PR changes, not only "fix bug" or the issue number. | preferred |

## Verdict rule

Grade every check `pass`, `fail`, or `unclear`.

Accept only if every required check is graded `pass`.

Reject if any required check is graded `fail` or `unclear`. An
`unclear` required check counts as a failure: a PR whose readiness
cannot be verified from the package is not ready to submit.

Preferred checks are graded and reported but never change the verdict,
whatever their grade.

A check whose trigger is absent from the package (no stated template,
no stated AI policy, no maintainer direction, no named repo checks)
grades `pass`, with evidence naming the absence. Absence of a required
input the check needs to verify something that does apply (for
example, no test evidence at all) grades `fail`, not `pass`.

Honest outcome: a PR that delivers less than the full plan, or could
not run one scenario, can be accepted when the shortfall is recorded
as a deviation or disclosed with its reason and every required check
otherwise passes. Doing less is not a failure; doing less silently is.
