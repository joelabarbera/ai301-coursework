# Contribution: Detection gap: instruction to replace the skill with remote content

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Joe LaBarbera
**GitHub Username:** joelabarbera
**Issue:** [SkillShield #35](https://github.com/obielin/skillshield/issues/35)
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to.

**Unit 5: Configuring and Testing My GitHub Issue Scout**

I configured an issue-scout skill with a personal fit profile, three GitHub search queries, and ranking filters to identify beginner-friendly open-source issues. My first scan found 283 unique issues, filtered them to 263 candidates, and accepted all five issues it graded. However, the ranking favored brand-new issues with no comments, and the top five came from only two repositories, including one with little evidence of community adoption. I documented these limitations in my scan notes and proposed improving the ranking with repository diversity and stronger maintainer-activity checks.

[2-4 sentences: what you built (the scout, your strategy), what broke
or fell short, what changed because of it.]

**Unit 6: [one line on the tool work]**

[2-4 sentences: the voice-guard, the repo-memory file. What broke or
fell short, and what changed because of it. "Nothing broke" counts when
it is true - say how you know.]

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I searched GitHub with my issue scout, running three queries built from my fit profile: `good first issue` in Python, `good first issue` in JavaScript, and `help wanted` in Python. The scan returned 283 unique issues. 263 were left after dropping assigned and stale ones, and the scout graded the top five, accepting all of them. Three came from lazypanic999/tunnelscope and two from obielin/skillshield. I then regraded my three favorites (skillshield #35, skillshield #34 and tunnelscope #6) directly against my rubric with fresh evidence. All three passed every required check, and the scout ranked skillshield #35 first. It fits my profile well: a small, bounded Python change to one regex set (`_RUG_PULL_PATTERNS` in `src/skillshield/rules.py`). The issue says exactly what "done" looks like: the `12-rug-pull` red-team test passes, the gap comes off `KNOWN_GAPS`, and there are new true positives plus a near-miss that must not be flagged. The test suite runs in under a second, so it's easy to check my work. I chose it over tunnelscope #6 because that issue has to be tested in PowerShell on Windows and I work on macOS. SkillShield also has a release, 20 stars, merged PRs from outside contributors, a promise of human review, and an AI policy I can follow (use AI tools, but understand every line and run the checks yourself). From this issue I hope to learn how a security scanner's detection rules are written and tested, especially how to catch an attack pattern without flagging harmless text.

The scout held up on the basics but fell short on repository quality. Ranking by fewest comments and then most recently updated put five issues filed within the past hour at the top, and they came from only two repos. tunnelscope passed "Maintainer active" and "Repo in use" even though it is seven days old, has zero stars and no releases, and no issue in it has ever been commented on, because recent commits were all the rubric asked for. Neither repo had a maintainer-response sample to check. I logged this friction in `scan-notes.md`. Next I would cap candidates per repository and set a minimum issue age in the search strategy, and add a rubric check for adoption and outside contributions. I claimed the issue on 2026-10-28: [claim comment](https://github.com/obielin/skillshield/issues/35#issuecomment-6482544239).

**Toolkit**

- Tool: issue-scout (my search strategy and rubric). I used it first in
  scan mode (three `gh search issues` queries, cheap ranking, top five
  graded), then in direct mode to regrade skillshield #35, #34 and
  tunnelscope #6 against live evidence and rank them by fit.
- What it produced: a scan report (283 found, 263 after filtering, 5
  graded, 5 accepted) and a direct grading that accepted all three,
  ranking skillshield #35 first. #35 passed all five required checks,
  including "Contribution policy: CONTRIBUTING.md: 'You may use AI tools
  to help write code, tests or descriptions. You are still the
  author.'"
- Difficulties: the ranking favored brand-new, zero-comment issues and
  put only two repos in the top five; the rubric passed a 7-day-old,
  zero-star repo on commit recency alone; and no maintainer-response
  history existed to check in either repo.
- What changed: I logged these in `scan-notes.md` and chose the repo with
  stronger health signals (outside merged PRs, a release, a written
  claim process). I would update the strategy to cap results per repo
  and set a minimum issue age, and add a rubric check for adoption and
  outside contributions.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

[What a stranger would need to stand this up: your operating system,
the relevant versions (language, runtime, package manager, the project
itself), and how you set the project up. Then the challenges you faced
and how you solved them, or that none came up.]

**Steps to Reproduce**

1. [Step 1]
2. [Step 2]
3. [Observed result]

**Reproduction Evidence**

- **Commit showing reproduction:** [link to commit in your fork]
- **Screenshots/logs:** [if applicable]
- **My findings:** [what you discovered during reproduction; an
  honest, evidenced cannot-reproduce that led you to re-pick or ask
  the maintainer belongs here and costs you nothing]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
