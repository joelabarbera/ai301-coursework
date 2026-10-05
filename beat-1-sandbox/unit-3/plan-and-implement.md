# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`.

---

## Posted upstream

**GitHub username**

joelabarbera

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-6003267917

I reproduced this issue on Python 3.11.15 with passlib 1.7.4. The existing regression test XFAILs as expected, and calling `verify_password("password", "not_a_valid_bcrypt_hash")` directly raises `passlib.exc.UnknownHashError`.

The exception comes from `pwd_context.verify()` in `core/security.py`. I plan to update `verify_password()` to catch that specific exception and return `False`, while leaving verification behavior for valid bcrypt hashes unchanged. I will also remove the Issue #72 `xfail` marker from the existing regression test so it becomes a normal test of the fixed behavior.

I’ll validate the change by re-running the Issue #72 regression test, the direct invalid-hash reproduction, and the security unit test suite. I’m keeping the change limited to handling the reproduced `UnknownHashError`; I do not plan to change the hashing configuration or unrelated authentication/JWT behavior.

---

## Your branch

**Branch**

`fix/72-invalid-password-hash`

**Evidence**

Before:

Command:

`pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -rx`

Output:

`XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False`

Direct reproduction command:

`python -c "from core.security import verify_password; verify_password('password', 'not_a_valid_bcrypt_hash')"`

Output:

`passlib.exc.UnknownHashError: hash could not be identified`

After:

Command:

`pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -rx`

Output:

`tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format PASSED [100%]`

`======================== 1 passed, 2 warnings in 0.47s =========================`

Direct reproduction command:

`python -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"`

Output:

`False`

Full security test command:

`pytest tests/unit/test_security.py -v`

Output:

`======================== 25 passed, 2 warnings in 5.37s ========================`

## Eval iterations

**Run history**

First full run:

`agreement: 17/20 scored items (bar: 18/20: FAIL)`

After revising the rubric, I ran targeted checks on `pkg-20`, `pkg-05`, and `pkg-14` to verify the behavior of the changed checks.

Final full run:

`agreement: 19/20 scored items (bar: 18/20: PASS)`

**Package analysis**

`pkg-14`

My rubric returned `reject`, while the gold label was `accept`.

The final run recorded:

`pkg-14 clear-accept accept/reject NO`

The failure was:

`failed: unknowns-honest`

My `unknowns-honest` check was still slightly too strict for this package. It treated a claim in an otherwise acceptable plan as insufficiently supported, even though the gold evaluation considered the plan ready to build. I accepted this remaining false rejection because the overall rubric reached 19/20 and passed the required 18/20 agreement bar.

**Check rationale**

From my rubric:

`unknowns-honest | Factual claims and statements of certainty in the plan read against the repro evidence, issue context, and repo facts; use stated risks, assumptions, or unknowns when present. | Pass unless the plan presents a material claim as certain that the available evidence leaves unresolved or contradicts it. A plan does not need to invent or list risks, assumptions, or unknowns when none are material to executing the proposed change. Missing a risks or unknowns statement alone is not a failure. | required`

I revised this check because the earlier version was too eager to reject plans simply for not including an explicit risks or unknowns section. The final wording focuses on unsupported material certainty instead. It explicitly says that missing a risks or unknowns statement by itself is not a failure.

**Trade-offs**

The revision to `unknowns-honest` improved acceptance of valid plans, including the targeted re-run of `pkg-05`, which returned the expected `accept`. I also re-ran `pkg-14`, which remained a false rejection under `unknowns-honest`. I accepted that trade-off rather than weakening the check further and risking false acceptance of plans that state unsupported material claims as facts. The final full evaluation reached:

`agreement: 19/20 scored items (bar: 18/20: PASS)`
