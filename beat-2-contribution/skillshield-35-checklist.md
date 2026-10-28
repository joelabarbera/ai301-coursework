# SkillShield #35 Checklist

Issue: [obielin/skillshield#35](https://github.com/obielin/skillshield/issues/35)
Claim comment: [posted 2026-10-28](https://github.com/obielin/skillshield/issues/35#issuecomment-6482544239)
PR promised by: about 2026-11-04 (one week from the claim)

Steps 1–3 follow SkillShield's CONTRIBUTING.md quick start.

## 1. Fork and clone

- [ ] `gh repo fork obielin/skillshield --clone && cd skillshield`
- [ ] `git checkout -b fix/sg-006-rug-pull`

## 2. Set up Python

- [ ] Make a virtual environment with Python 3.10–3.12:
      `python3.11 -m venv .venv && source .venv/bin/activate`. CI checks style on 3.11.
- [ ] Install the dev dependencies: `pip install -e ".[dev]"`

## 3. Reproduce the gap

- [ ] Run `pytest tests/test_redteam.py -v` and confirm `12-rug-pull` is listed under `KNOWN_GAPS`.
- [ ] Scan `tests/fixtures/redteam/malicious/12-rug-pull.md` and confirm it comes back **SAFE**.
- [ ] Remove `12-rug-pull` from `KNOWN_GAPS` and confirm that test now **fails**. That's the
      "fails without the change" evidence.
- [ ] Write down the commands and their output for the Reproduction Process section of
      `contribution-story.md`.

## 4. Implement the fix

- [ ] Read "Adding or changing a detection rule" and "Test samples must be safe" in CONTRIBUTING.md.
- [ ] Extend `_RUG_PULL_PATTERNS` in `src/skillshield/rules.py` so SG-006 catches download or
      fetch instructions that then replace, overwrite or update this file, these instructions,
      or the skill.
- [ ] Add at least 2 new true-positive tests, plus the near-miss "Download the latest dataset
      from https://example.com/data.csv", which must not be flagged.
- [ ] Keep test samples safe: only example.com URLs, no real payloads.
- [ ] Don't rename or change any existing rule IDs.

## 5. Run the required checks

- [ ] `pytest`
- [ ] `ruff check src tests`
- [ ] `black --check src tests` (line length is 100)
- [ ] Add a dated Implementation Notes entry to `contribution-story.md`.

## Before the PR

- [ ] Check the issue for a reply or assignment from @obielin. A PR on an unassigned issue is
      welcome either way.
- [ ] Open the PR by about 2026-11-04, as promised in the claim.
