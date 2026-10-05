# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

### Where it lives

In an eval package, read the candidate plan's diagnosis or stated cause together with the repro-evidence block. Use the reproduced steps, observed behavior, expected behavior, commands, output, and any artifacts or observations that narrow the cause. Also use relevant issue context when it establishes behavior the diagnosis must explain.

In live mode, read the diagnosis in `plan.md` against the student's posted repro comment or repro pack and the original GitHub issue thread.

### What good looks like

The stated cause explains behavior that the reproduction actually demonstrates and does not contradict material evidence. The diagnosis should distinguish what the evidence establishes from what is still an inference or unknown.

A diagnosis is not grounded when it ignores reproduced behavior, contradicts the available output, or claims a cause that the evidence does not support as established fact.

## Scope

### Where it lives

In an eval package, read the candidate plan's scope statement, explicit non-goals, files or areas to touch, and implementation approach. Compare these with the issue context and repro evidence to determine what work is actually necessary.

In live mode, read the scope, files-to-touch, and non-goals in `plan.md` against the reproduced issue and relevant repository structure.

### What good looks like

The scope describes one bounded change that directly addresses the reproduced issue and includes only work necessary to implement or validate that change. Named files or areas should be plausible targets based on the available evidence.

Scope is not bounded when the plan adds unrelated cleanup, refactors, features, broad rewrites, or speculative changes that are not required to fix the reproduced behavior.

## Executability

### Where it lives

In an eval package, read the candidate plan's files-to-touch section, proposed approach, implementation steps, and ordering of work. Use the repo-facts block and issue/repro context to check whether those targets and actions make sense in the repository.

In live mode, read `plan.md` together with relevant repository files and contribution documentation.

### What good looks like

A contributor unfamiliar with the author's thinking can identify where to begin, what behavior needs to change, and the basic implementation strategy without inventing the core approach.

The plan does not need to contain finished code, but it must provide enough concrete direction that implementation can begin without first rediscovering the entire solution.

## Test plan

### Where it lives

In an eval package, read the candidate plan's test plan against the repro-evidence block. Compare the original reproduction steps, failing result, and expected behavior with the proposed post-fix commands, checks, and expected results.

In live mode, compare the test plan in `plan.md` with the student's Unit 2 repro comment or provided repro pack.

### What good looks like

The test plan exercises the behavior involved in the reproduced failure and states an observable expected result after the fix. Someone running the test should be able to distinguish the fixed behavior from the original failure.

A test plan is insufficient when it only says to run tests, verify the fix, or check that things work without identifying what behavior or output demonstrates success.

## Honesty

### Where it lives

In an eval package, read the candidate plan's risks, assumptions, unknowns, tentative claims, and deviations when present. Compare factual claims with the repro evidence, issue context, and repo facts.

In live mode, inspect the risks and unknowns in `plan.md`. After implementation begins, also inspect the `## Deviations` section for differences between the posted plan and the actual change.

### What good looks like

Material uncertainty is explicitly described as uncertainty. Assumptions that still require verification are not presented as proven facts, and risks that could affect the implementation or test result are acknowledged.

After a build, a material change from the original plan is recorded under `## Deviations` with what changed and why. If nothing changed, the plan should say so rather than inventing a deviation.

## Comms

### Where it lives

In an eval package, read the candidate plan comment against the issue context or thread highlights and the repo-facts block. Check relevant contribution instructions, templates, maintainer requests, and any stated AI-use or disclosure policy.

In live mode, read `comment.md` against the full GitHub issue thread, especially maintainer comments, and against the repository's contributing documentation and applicable templates or policies.

### What good looks like

The comment accurately communicates the diagnosis, bounded scope, intended approach, and validation that the contributor plans to perform. It responds to material maintainer requests and follows relevant repository conventions.

Thread-aware communication does not contradict the issue discussion, ignore explicit maintainer direction, claim unsupported certainty, or omit a disclosure or other contribution requirement that the repository explicitly requires.