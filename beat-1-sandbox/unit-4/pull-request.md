# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

https://github.com/codepath/pathreview-ai301-fa26-s1/pull/210

**Branch**

`fix/72-invalid-password-hash`

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Run 1: 20/20. This was the only run. It is the run recorded in `eval-run.txt`:

   > `agreement: 20/20 scored items  (bar: 18/20: PASS)`

   Per-category results from that run:

   > `categories: clear-accept 7/7  not-tested 4/4  silent-drift 4/4  standards-wall 2/2  unreviewable 3/3`

**Package analysis**

Package: **pkg-20** (`ghostty-org/ghostty#13604`, category `standards-wall`).
My rubric's verdict was `reject`, and the gold label is `reject`. The two agree (`pkg-20  standards-wall  reject  reject   yes`).

On its engineering, pkg-20 is a strong PR. The diff implements the maintainer-authored diagnosis in `src/config/Config.zig` and stays inside the plan. The test evidence shows the repro query moving from `ESC[?997;2n (light)` before the fix to `ESC[?997;1n (dark)` after it, which matches the plan's expected-after. So plan-fidelity, behavior-verified and diff-focused would all pass. The rejection comes from the repo-facts block, which states:

> "contribution policy (CONTRIBUTING.md + AI_POLICY.md): strict AI rules. All AI usage in any form must be disclosed, stating the tool used and the extent of the assistance"

The candidate description contains no AI-use disclosure at all. My `disclosure-policy` check fails whenever "a stated policy applies and the description does not meet it". Because it is a `required` check, the verdict rule ("Reject if any required check is graded `fail` or `unclear`") turns that single failure into a reject. The gold note gives the same reason: "excellent bounded fix ... but the description contains no AI-use disclosure and ghostty's stated policy requires disclosing all AI usage." This package is the reason disclosure is a separate required check and is not folded into general PR quality. Otherwise a technically excellent PR would get through this standards wall.

**Check rationale**

From `tools/pr-precheck/rubric.md`:

> | disclosure-policy | The repo's stated AI-use or disclosure policy in the repo-facts block or contribution docs, read against the PR description. | Pass if the repo states no AI-use or disclosure policy, or if the description meets the policy as stated (discloses where disclosure is required; the contribution does not violate a stated prohibition). Fail if a stated policy applies and the description does not meet it. | required |

This check is anchored to the repo's *stated* policy, not to a universal rule that every PR must disclose AI use. Disclosure requirements differ from repo to repo. Ghostty (pkg-20) requires the tool and the extent of assistance, while many repos state nothing. A universal rule would hold clean PRs in repos that never asked for disclosure, and it would fail `clear-accept` packages for something the repo does not require. Grading "the policy as stated" also covers prohibitions as well as disclosure requirements, so a repo that bans AI-generated code is handled by the same row. The check is `required`, not `preferred`, because breaking a repo's stated AI policy gets a PR closed no matter how good the code is. The verdict rule's absent-trigger clause ("A check whose trigger is absent ... grades `pass`, with evidence naming the absence") keeps this check from penalizing repos with no policy.

**Trade-offs**

The check gives up any judgment about AI use where the repo is silent. If a repo has no stated AI policy, a PR that was heavily AI-generated and discloses nothing still passes `disclosure-policy`. I accept that this case will be missed: the rubric grades against the repo's stated asks, not my own norms. It also means the check can only be as accurate as the policy text the package captures. If a repo keeps its AI rules in a file that is not in the repo-facts block, the check will grade `pass` on absence.

Nothing changed elsewhere, and here is how I know. This was the only run, and it scored 20/20. Every other `standards-wall` package and all 7 `clear-accept` packages agreed with gold (`standards-wall 2/2`, `clear-accept 7/7`). So the check did not wrongly hold any accept-labelled package.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
