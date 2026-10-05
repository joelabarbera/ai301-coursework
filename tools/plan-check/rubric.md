# Rubric: is this plan ready to post and build from?

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| diagnosis-grounded | The plan's stated diagnosis/cause read against the repro evidence, including reproduced behavior, expected behavior, commands, and output. | Pass if the proposed diagnosis is consistent with the reproduced evidence and does not ignore or contradict evidence that materially changes the likely cause. | required |
| scope-bounded | The plan's scope statement, files to touch, proposed changes, and explicit non-goals read against the reproduced issue. | Pass if the proposed work is one bounded change needed to address the reproduced issue and does not introduce unrelated work or unnecessary scope. | required |
| cause-targeted | The plan's proposed approach read against its diagnosis and the repro evidence. | Pass if the proposed change addresses the likely cause supported by the evidence rather than only masking the observed symptom. | required |
| executable | The plan's files-to-touch and implementation approach read against the repo facts and available issue/repro context. | Pass if another contributor could begin implementing the change from the plan without having to invent a missing implementation strategy or determine the basic target of the change themselves. | required |
| test-observable | The test plan read against the repro evidence's steps, observed failure, and expected behavior. | Pass if the planned checks exercise the relevant behavior and specify an observable result that would distinguish the fixed behavior from the reproduced failure. | required |
| unknowns-honest | Factual claims and statements of certainty in the plan read against the repro evidence, issue context, and repo facts; use stated risks, assumptions, or unknowns when present. | Pass unless the plan presents a material claim as certain that the available evidence leaves unresolved or contradicts. A plan does not need to invent or list risks, assumptions, or unknowns when none are material to executing the proposed change. Missing a risks or unknowns statement alone is not a failure. | required |
| comment-aligned | The draft plan comment read against the issue/thread highlights, repo facts, and all explicit repository conventions or contribution requirements provided in the package. | Pass only if the comment follows every applicable explicit maintainer request and repository convention supplied in the package, including required content, formatting, testing, or disclosure requirements. Fail when the comment omits or conflicts with an applicable explicit requirement, even when its technical diagnosis and implementation plan are otherwise correct. | required |

## Verdict rule

Accept only if every required check passes.

Reject if any required check fails.

Treat `unclear` as a failure for required checks because a plan is not ready to post or build from when the evidence is insufficient to establish that a required condition passes.

Preferred checks, if added later, do not change the final verdict.