# Unit 2 — Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

## Your identity upstream

**GitHub username**

joelabarbera

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5874174530

Hi! I'd like to investigate this issue. I'll reproduce the reported `verify_password` behavior where an `UnknownHashError` is raised instead of returning `False`. I'll test it in my local environment and post a reproduction report with my environment, steps, and observed result.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72#issuecomment-5874598264

# Reproduction Report — Issue #72

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

## Environment

- OS: macOS 15.6.1 (Build 24G90)
- Python: 3.11.15
- passlib: 1.7.4
- bcrypt: 4.3.0
- Commit: f89c06fc3ff292df2a04a39ac51319d32a76b779

## Steps to reproduce

1. Clone the repository and enter it.
2. Create and activate a Python 3.11 virtual environment.
3. Install the project development dependencies with:

   `pip install -e ".[dev]"`

4. Run the existing regression test:

   `pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -rx`

5. The test reports `XFAIL` for Issue #72. Because this test is marked `xfail(strict=True)`, the XFAIL indicates the known bug is still present.

6. I also reproduced the behavior directly with:

   `python -c "from core.security import verify_password; verify_password('password', 'not_a_valid_bcrypt_hash')"`

## Observed behavior

The existing regression test reports:

`XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False`

Calling `verify_password()` directly with the invalid hash raises:

`passlib.exc.UnknownHashError: hash could not be identified`

The exception originates from the call to `pwd_context.verify()` in `core/security.py`.

## Expected behavior

`verify_password()` should handle an invalid/non-bcrypt hash gracefully and return `False` rather than raising `UnknownHashError`.

## Outcome

Reproduced. On the environment above, an invalid hash causes `verify_password()` to raise `passlib.exc.UnknownHashError` instead of returning `False`.

## Eval iterations

**Run history**

Full run: 19/20 agreement.
Targeted revision and sanity checks were then run against the disagreement.
Final full run: 18/20 agreement (PASS), with every category matched.

**Package analysis**

`pkg-20`: My initial rubric decided accept, while the gold label was reject. The package's technical reproduction evidence was strong, but repo-facts required all AI usage to be disclosed, including the tool and extent of assistance. The candidate comments did not contain that disclosure. My original conventions check was too general and allowed the missing disclosure to pass, so I revised it to require visible compliance with every communication requirement in repo-facts.

**Check rationale**

`conventions-followed | Repo-facts contribution policy read directly against the candidate claim comment and repro report | Pass only if the candidate comments visibly satisfy every communication requirement stated in repo-facts. Treat a repo-facts requirement that AI use must be disclosed as requiring the candidate comments to contain that disclosure; do not infer that disclosure is unnecessary because the comments do not mention AI. If the policy requires the tool and extent of assistance, both must appear. Fail if any required disclosure or other stated communication requirement is absent. | required`

I revised this check after `pkg-20` exposed an ambiguity in the original version. The stricter wording makes the evidence requirement explicit: when repo-facts requires an AI disclosure, the disclosure must actually appear in the candidate comments, including the required tool and extent information.

**Trade-offs**

The stricter `conventions-followed` check can reject a technically strong reproduction package when its upstream comments omit a repository-mandated disclosure. I accept that trade-off because this rubric evaluates whether a package is ready to post upstream, which includes following the repository's communication policy. I re-ran `pkg-20` after the revision and also sanity-checked other packages before the final full run.
