# Rubric: is this reproduction package ready to post?

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks
| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | Repro report's environment record | Pass if the report names the tool version and OS. Fail if either is missing. | required |
| steps-complete | Repro report's reproduction steps | Pass if a stranger could re-run the reproduction without guessing. Fail if required actions, commands, or setup are missing. | required |
| behavior-matches | Repro artifacts and observed output read against the issue description | Pass if the evidence shows the behavior described by the issue, or clearly demonstrates an evidenced cannot-reproduce. Fail if it demonstrates a different or adjacent behavior. | required |
| conventions-followed | Repo-facts contribution policy read directly against the candidate claim comment and repro report | Pass only if the candidate comments visibly satisfy every communication requirement stated in repo-facts. Treat a repo-facts requirement that AI use must be disclosed as requiring the candidate comments to contain that disclosure; do not infer that disclosure is unnecessary because the comments do not mention AI. If the policy requires the tool and extent of assistance, both must appear. Fail if any required disclosure or other stated communication requirement is absent. | required |
| outcome-honest | Repro report's stated outcome read against its artifacts | Pass if the stated result accurately matches the evidence. Fail if the report claims reproduction or non-reproduction that the evidence does not support. | required |
| proof-screenshots | Evidence attached to the repro package | Pass if screenshots or equivalent captured evidence clearly show the relevant reproduction result. Fail if the claimed result has no supporting captured evidence. | preferred |

## Verdict rule
Accept only if every required check passes. Any required check graded fail or unclear makes the verdict reject. Preferred checks do not change the final verdict.
