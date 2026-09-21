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

[The agreement score of each run you did, in order. A single run is a complete answer if
only one run occurred. **The last score in your list must match the agreement line in the
`eval-run.txt` you committed** — that file is the record of your final run.]

**Issue analysis**

[One scored issue, identified by id (`issue-01` through `issue-20`; the `calib-`
issues are not scored). State your rubric's decision, the gold label, and the
reasoning that produced your rubric's result.]

**Check rationale**

[One check from the `rubric.md` uploaded to `tools/issue-select/`, quoted as it is
currently written, with the reasoning behind its current form.]

**Trade-offs**

[What the quoted check gives up. Any one of these is a complete answer: an issue whose
result it changes, a canary you re-ran with `--only`, a case you accept it will miss, or a
stated reason nothing changed elsewhere. "Nothing changed, and here is how I know" earns
the point in full when the reason follows.]

---

## Selection rationale

Graded on whether all three are answered, in your own words. Not on how good the
reasoning is, and not on length — a short honest answer to each earns the full marks.
This is also the basis for the claim comment you write in Unit 2.

**Selection rationale**

[Answer all three:

1. The issue's fit to your interests and to the time available.
2. What the verdict identified correctly, and what you weighed that the rubric could
   not.
3. The anticipated difficulty in claiming it.]

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/issue-select/`.
