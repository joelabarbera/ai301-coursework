# Plan — Issue #72: verify_password raises UnknownHashError instead of returning False

Issue: https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

## Diagnosis

`verify_password()` currently calls `pwd_context.verify(plain_password, hashed_password)` directly and returns its boolean result.

The Unit 2 reproduction showed that when `hashed_password` is not a recognized bcrypt hash, Passlib does not return `False`. Instead, `pwd_context.verify()` raises `passlib.exc.UnknownHashError`, and that exception escapes from `verify_password()`.

Reproduction evidence:

> `XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False`

The direct reproduction also produced:

> `passlib.exc.UnknownHashError: hash could not be identified`

The reproduction identified the exception as originating from the call to `pwd_context.verify()` in `core/security.py`.

The existing function contract says `verify_password()` returns `True` when the password matches and `False` otherwise, so an unrecognized hash format should be handled by this helper rather than escaping to its caller.

## Scope

### In scope

- Update `verify_password()` in `core/security.py` so an unrecognized hash format results in `False` instead of an escaping `UnknownHashError`.
- Import the specific Passlib exception needed to handle this failure.
- Enable the existing regression test for Issue #72 by removing its `xfail` marker once the implementation satisfies the expected behavior.
- Run the focused regression test and relevant security tests to verify the change.

### Out of scope

- Changing password hashing algorithms or the configured `CryptContext`.
- Changing valid-password or wrong-password behavior.
- Refactoring unrelated authentication or JWT code.
- Adding new authentication features.
- Broad exception handling unrelated to the reproduced `UnknownHashError`.

## Files to touch

### `core/security.py`

Update `verify_password()` to handle `passlib.exc.UnknownHashError` from `pwd_context.verify()` and return `False` for an unrecognized hash.

### `tests/unit/test_security.py`

Remove the Issue #72 `xfail(strict=True)` marker from `test_verify_with_wrong_hash_format` so the existing regression test becomes a normal passing test.

No other files are expected to require changes.

## Approach

1. Import `UnknownHashError` from Passlib's exception module in `core/security.py`.

2. Keep the existing verification behavior for valid bcrypt hashes by continuing to call:

   `pwd_context.verify(plain_password, hashed_password)`

3. Wrap that verification operation so that `UnknownHashError` is caught specifically.

4. Return `False` when `UnknownHashError` is raised.

5. Do not catch unrelated exceptions. This keeps the change limited to the reproduced invalid-hash behavior instead of hiding other failures.

6. Remove the `xfail` marker from `test_verify_with_wrong_hash_format` because the test already expresses the required post-fix behavior:

   `assert result is False`

## Test plan

First, re-run the focused Unit 2 reproduction test:

`pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -v -rx`

Before the fix, this test reports XFAIL because the invalid hash causes `UnknownHashError`.

After the fix and removal of the `xfail` marker, expect the test to PASS because `verify_password("password", "not_a_valid_bcrypt_hash")` should return `False`.

Also re-run the direct reproduction:

`python -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"`

Before the fix, the call raises:

`passlib.exc.UnknownHashError: hash could not be identified`

After the fix, expect the command to print:

`False`

Then run the security unit tests:

`pytest tests/unit/test_security.py -v`

Expect the existing valid-password, incorrect-password, hashing, JWT, and Issue #72 regression tests to pass, confirming that handling an unrecognized hash did not regress existing security behavior.

## Risks and unknowns

The reproduced failure specifically identifies `UnknownHashError`, so the implementation should catch that exception rather than a broad `Exception`.

The focused regression test already defines the required behavior for the reproduced invalid hash. No change to the configured bcrypt hashing scheme is expected to be necessary.

If testing reveals another malformed-hash failure mode that raises a different exception, that should be evaluated separately rather than broadening this fix without evidence.

## Deviations

No deviations. The implementation matched the posted plan: `verify_password()` catches `UnknownHashError` and returns `False`, and the existing Issue #72 regression test was enabled by removing its `xfail` marker.
