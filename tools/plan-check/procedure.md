# Procedure: how this skill grades a plan package

## Read order

1. Read the issue and thread highlights first. Record the reported problem, expected behavior, relevant maintainer requests, constraints, and any repository conventions mentioned in the thread.

2. Read the repo-facts block next. Record repository-level facts that affect the proposed change, including relevant files, contribution conventions, test commands, or implementation constraints supplied in the package.

3. Read the repro evidence before reading the proposed plan. Record the exact reproduction steps, the observed failing behavior, the expected behavior, relevant commands and output, and any evidence that points toward a likely cause. Reading the reproduction first prevents the plan's diagnosis from biasing interpretation of the evidence.

4. Read the complete plan. Record its stated diagnosis, proposed scope, explicit non-goals, files to touch, implementation approach, test plan, risks, assumptions, and unknowns.

5. Read the draft plan comment last. Record what diagnosis, scope, approach, and validation it communicates publicly and compare those claims with the issue/thread, repro evidence, repo facts, and full plan.

6. Do not grade any rubric check until the initial read of all available package material is complete.

## Evidence gathering

1. For `diagnosis-grounded`, gather the plan's stated diagnosis or cause and compare it directly with the repro evidence's observed behavior, expected behavior, commands, output, and any cause-related evidence. Record any supporting evidence and any contradiction.

2. For `scope-bounded`, gather the plan's scope statement, files to touch, proposed changes, and explicit non-goals. Compare them with the reproduced issue. Record whether every proposed change contributes directly to fixing or validating that issue and whether unrelated work has been introduced.

3. For `cause-targeted`, gather the proposed implementation approach and compare it with both the stated diagnosis and the repro evidence. Record whether the approach changes the behavior at the likely source of the failure or merely hides, bypasses, or compensates for the visible symptom.

4. For `executable`, gather the files to touch, implementation steps, relevant repo facts, and available issue/repro context. Record whether another contributor can identify where to begin, what behavior must change, and the basic implementation strategy without inventing a missing approach.

5. For `test-observable`, gather the original repro steps, original observed failure, expected behavior, and the plan's proposed test steps and expected post-fix results. Record whether the planned validation exercises the relevant behavior and whether its result can distinguish the fixed behavior from the reproduced failure.

6. For `unknowns-honest`, gather every risk, assumption, unknown, tentative statement, and unsupported factual claim in the plan. Compare those statements with the evidence available in the package. Record whether material uncertainty is acknowledged rather than stated as established fact.

7. For `comment-aligned`, gather the draft comment's claims about diagnosis, scope, implementation, and validation. Compare them with the full plan, issue/thread highlights, repo facts, and repository conventions. Record any material omission, contradiction, or conflict.

8. Use `references/evidence-guide.md` whenever the location or meaning of a piece of evidence is unclear. Do not infer missing evidence from what a good plan would normally contain.

## Check execution

1. Grade checks in this order: `diagnosis-grounded`, `scope-bounded`, `cause-targeted`, `executable`, `test-observable`, `unknowns-honest`, then `comment-aligned`.

2. For each check, use only the evidence sources named by that rubric row and the evidence gathered according to this procedure. Do not substitute unrelated package material for a required evidence source.

3. Compare the gathered evidence with the check's pass condition. Grade `pass` only when the available evidence establishes the pass condition.

4. Grade `fail` when the available evidence establishes that the pass condition is violated, including when evidence directly contradicts the plan's claim or shows a concrete deficiency covered by the check.

5. Grade `unclear` when evidence necessary to decide the check is genuinely absent, incomplete, or ambiguous and the available material does not establish either pass or fail. Do not guess or fill gaps using assumptions.

6. Once the evidence needed for a check has been gathered, grade that check from the recorded evidence without reinterpreting unrelated parts of the package. Re-read source material only when a specific conflict or ambiguity must be resolved.

7. Record a concise reason for every grade. The reason must identify the concrete evidence that caused the grade rather than merely restating the rubric.

## Verdict assembly

1. After all checks are graded, apply the verdict rule from `rubric.md`.

2. Accept the package only when every required check is graded `pass`.

3. Reject the package if any required check is graded `fail` or `unclear`. An `unclear` required check counts as a failure for verdict purposes because readiness has not been established.

4. Preferred checks, if any are added later, may be reported but never change the final verdict.

5. For an accepted package, report that all required checks passed and support the result with the most relevant evidence from the package.

6. For `unknowns-honest`, inspect factual claims and statements of certainty in the plan and compare them with the repro evidence, issue context, and repo facts. Use stated risks, assumptions, or unknowns when present. Record a problem only when a material claim is presented as established even though the available evidence leaves it unresolved or contradicts it. Do not treat the absence of an explicit risks, assumptions, or unknowns list as a deficiency by itself.

7. End with the required JSON output using only the binary verdict `accept` or `reject`, and ensure the JSON verdict matches the grades reported above it.