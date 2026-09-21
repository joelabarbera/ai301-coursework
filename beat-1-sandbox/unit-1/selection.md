# Unit 1 — Issue Selection

Path: `beat-1-sandbox/unit-1/selection.md`

Record of the issue carried into Unit 2, and of the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in
the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the
wrong label is not graded.

---

## Selected issue

**Issue link**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72

**Verdict output**

[Your skill's live-mode output for this issue, pasted verbatim and ending with the
fenced JSON verdict block. A summary does not satisfy this field.]

**The verdict must record `accept` for this issue.** Choose an issue your own skill
accepts. If your skill rejects every candidate you try, that is a signal about your
rubric rather than about the issues: revise it and re-run — retries are unlimited and a
partial re-run costs about $0.20 — or run the skill on different candidates. Output
recording `reject` for the issue you chose earns no credit for this field.

```
#72 — verify_password raises UnknownHashError instead of returning False
  - Scope: single root-caused bug (passlib exception escaping in
    core/security.py), named files, named xfail test to unmark, 1–2h estimate,
    good first issue+tier-1 labels from a collaborator → pass
  - Unclaimed: no assignee; the only cross-referenced PR is a different repo's
    (foojanbabaeeian/ai301-coursework-Fozhan) unrelated coursework PR that
    merely mentions "issue #72" — it doesn't touch core/security.py and isn't a
    real linked fix → pass 
  - Verdict: accept

 [
    {
      "item": "https://github.com/codepath/pathreview-ai301-fa26-s1/issues/72",
      "checks": [
        {"name": "Maintainer active", "grade": "pass", "evidence":
  "Default-branch commit on 2026-09-16, 5 days before capture date 
  2026-09-21."},
        {"name": "Repo in use", "grade": "pass", "evidence": "Repo not archived;
  pushedAt 2026-09-16T21:48:27Z, within 90 days."},
        {"name": "Scope fits", "grade": "pass", "evidence": "Issue names exact 
  bug (UnknownHashError escaping in core/security.py), expected behavior (return
  False), files, and the xfail test to unmark; opened by a COLLABORATOR with 
  good-first-issue/tier-1 labels."},
        {"name": "Issue unclaimed", "grade": "pass", "evidence": "assignees: [] 
  and the only cross-referenced PR is an unrelated repo 
  (foojanbabaeeian/ai301-coursework-Fozhan#1) that only mentions '#72' in its 
  title, touching no files in core/security.py."},
        {"name": "Contribution policy allows course workflow", "grade": "pass",
  "evidence": "docs/CONTRIBUTING.md states no AI restriction; repo's own commits
  are Claude co-authored."}
      ],
      "verdict": "accept"
    },
```

---

## Eval iterations

Quote source text directly in each field below. Paraphrase does not satisfy them.

**Run history**

15/20
4/5
1/1
17/20
5/7
7/7
20/20

**Issue analysis**

issue-15 — My rubric's decision was reject, and the gold label was reject. The issue looked approachable because it had a good first issue label, but its history showed prolonged discussion, multiple contributors attempting it, and abandoned or closed implementation attempts. I updated the Scope fits check so that this history counts as evidence that an apparently simple issue may actually have unresolved scope.

**Check rationale**

Scope fits — "Pass when the issue identifies one coherent outcome or concrete bug and provides enough information or maintainer-curated scope signals for a contributor to begin investigating or implementing it."

I used this wording because my earlier versions of the check were too strict about issue size and caused bounded issues like issue-01, issue-04, and issue-19 to be rejected. The current check focuses on whether there is one coherent, actionable outcome instead of assuming that a short description, multiple files, or technical complexity makes an issue unsuitable.

**Trade-offs**

This check gives up some simplicity because scope cannot be judged only by issue length or a good-first-issue label. I re-ran issue-01, issue-04, issue-05, issue-10, issue-15, issue-19, and issue-20 with --only as canaries. The final version accepted the three bounded issues and continued rejecting the four scope failures, giving 7/7 on that targeted run.

---

## Selection rationale

1. Issue #72 fits my interests because it is a small Python backend bug, which is close to the type of backend work I want more experience with. The estimated 1–2 hour scope also fits the time I have available.

2. The verdict correctly identified that the repository is active, the issue is unclaimed, and the bug has a specific expected behavior and location in the codebase. I also considered that the issue is smaller than the other accepted candidates and is closer to my existing Python/backend experience, which made it a better first contribution for me.

3. I expect claiming it to be fairly straightforward because there is no current assignee or active PR fixing the bug. The main difficulty will be understanding the existing security code and reproducing the malformed-hash behavior before making the fix.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
