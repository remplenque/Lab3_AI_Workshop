# Common AI recommendation audit

**Reject.** Choosing the forest setting and threshold on 2026 makes 2026 a selection set, so its score is optimistic, not an independent test.
Training ending in 2021 doesn't fix this: data is independent only if it was never used for a decision.
Evidence: `lab03_support_v3.py` line 112, `evaluate_scores()` → `choose_threshold(dev_scores, dev, ...)`, selects thresholds on dev only.
`outputs/run_manifest_v3.json` line 40: `"threshold_selection": "dev only; reused unchanged on train"`; `data/manifest_lab03_v3.json` lines 8–12 exclude 2026.
Our dev set has this role, so section 4 and the memo call dev figures optimistic and propose a frozen test on unused races.

## Truthful use / no-use record

Tool and use, or “No AI used for this lab”:
Claude (Anthropic, claude.ai, configured model `claude-opus-5-5`). Vicente and Baptiste used one shared chat on 26 Oct 2026, after our first complete run (commit `f7915d9`, 19:13). We used it for (a) a plan mapping the brief and rubric to each notebook section and file, (b) a review of our finished package, and (c) a first draft of this PROMPTS.md, including the audit wording above, which we checked against the cited files and lines.

If used, one actual suggestion (quote or faithful summary):
In the review, Claude said our `memo.md` (475 words with the table) printed about 6 lines over one page at 11 pt with 2.54 cm margins, and suggested cutting to about 400 words: drop the "No alert" table row, merge the first "How we compared" sentences, and remove the Baku origin clause and the repeated "do not adopt" sentence. It also noted that our executed notebook and README were modified but not committed, that the git history could not show the spec was written before the run, that README ended with a stray `# Lab3_AI_Workshop` line, and that "the other 435 alerts" in section 4 could be confused with the candidate's 435 FP.

What we accepted/rejected:
We accepted all of them in commit `043dfae` ("Apply review fixes and rerun notebook"). We cut and reworded the memo (475 → 386 words) without changing any figure. We added the commit-order note to `experiment_spec.md`, removed the stray README line, changed section 4 to "the remaining 435 of 580 alerts", then reran the notebook and committed everything.

Exact check performed and repository evidence:
`git diff f7915d9 043dfae -- memo.md`: every number in the new memo (94, 63, 57, 140 of 370; 931, 571, 580, 945 alerts; 681, 417, 435, 605 false; 230 of 370; 46 wet-tyre stops; Baku laps 39–47) is unchanged and matches `comparison_table.md` and notebook section 5 (`query-pattern3-events`, `query-pattern1-repeats`). After Restart + Run All (execution counts 1–17), `comparison_table.md` and all five `outputs/` files are byte-identical to `f7915d9` (none appear in the `043dfae` diff), so the rerun reproduced them exactly. Claude's re-render of the new `memo.md` fits one page on A4 and Letter (11 pt, normal margins), and we confirmed it in our own print preview.

One limitation relevant to this work:
Claude checked page length with its own Markdown-to-PDF rendering and can only check numbers against the files we give it. It cannot see whether the instructor has accepted access to the repository or confirm who wrote what. The candidate choice, analysis and interpretation in the notebook are ours, and were committed before this chat was used.

## Contributions

- Contributor 1 (Vicente Rodríguez), concrete action and related file/cell: wrote section 5 patterns 1–3 and the `query-pattern*` cells; applied the memo cuts in `memo.md`; final Restart + Run All and commit.
- Contributor 2 (Baptiste Vial), concrete action and related file/cell: wrote `experiment_spec.md` and section 4 with the `check-candidate-mechanism` cell; checked memo figures against `comparison_table.md`
