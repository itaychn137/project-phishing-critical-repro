# Submission Checklist — Data Science in Cyber Final Project

Deadline: **Friday, 10 July 2026, 23:59**. Submission = public GitHub repo link emailed to the examiner.

**Submission type: pair.** The lecturer approved pair submissions for this project. Both authors
(Itay Cohen — 328316591, Yarin Saraga — 330744392) appear on the title page. Working split: each
member builds their own project solo, then the pair cross-reviews and corrects each other's work;
Yarin is lead on the other joint project.

---

## 0. Before you touch git — placeholders

- [x] **Report title page** (`Phishing_Critical_Evaluation_Report.pdf`): now shows both authors
      and IDs (`Itay Cohen — 328316591 · Yarin Saraga — 330744392`) and the real repo URL. The PDF
      was re-exported from the editable `Phishing_Critical_Evaluation_Report.docx` — edit the DOCX
      and re-export if anything else changes.
- [ ] **README.md**: nothing to edit unless you rename files.

## 1. Sanity-check the notebook runs clean

- [ ] Fresh environment: `pip install -r requirements.txt` (Colab: the first cell clones the repo
      and `cd`s into it, so the relative `DataFiles/` paths resolve automatically).
- [ ] Open `phishing_critical_repro.ipynb` → **Kernel ▸ Restart & Run All**.
- [ ] All cells run with no errors; **9 figures** render. Accuracy checkpoints:
      `0.871` (author's 17 features) · `0.875` (5 created domain features alone) · `0.977` (combined).
- [ ] Notebook now includes the Colab setup cell (top) and the **3a. Feature creation** cell
      (lexical features from the raw `Domain`) inside the Feature Engineering section.

## 2. GitHub repo (already created — public)

- [x] Repo exists and is public: `https://github.com/itaychn137/project-phishing-critical-repro`.
- [ ] Confirm visibility is still **Public** (Settings → check), so the examiner can open it.

## 3. Push the updated files

Run from inside your local clone:

```bash
git add phishing_critical_repro.ipynb \
        Phishing_Critical_Evaluation_Report.pdf \
        Phishing_Critical_Evaluation_Report.docx \
        SUBMISSION_CHECKLIST.md
git commit -m "Pair submission: title page, Colab setup cell, feature-creation step"
git push origin main
```

- [ ] Confirm no file exceeds 100 MB (the largest here is ~4 MB — fine).

## 4. Verify the repo looks right on GitHub

- [ ] README renders with the structure tree and the three findings.
- [ ] `phishing_critical_repro.ipynb` previews (GitHub renders notebooks inline) and shows figures.
- [ ] `Phishing_Critical_Evaluation_Report.pdf` opens; title page shows both authors + IDs + repo URL.
- [ ] `DataFiles/` (incl. `5.urldata.csv`) and `original_source/` are present.
- [ ] Repo is **Public**.

## 5. Email the examiner

- [ ] Send the repo link to the address provided by the examiner.
- [ ] Suggested body: project title; both authors + IDs (Itay Cohen 328316591, Yarin Saraga 330744392);
      one-line summary ("reproduce + critically evaluate the shreyagopal phishing-URL detector"); the link.

## 6. Be ready for the optional oral

The staff may ask you to explain the work live. Be able to talk through, without notes:

- [ ] **Why 86% is misleading** — the three findings (source leakage, prevalence, contamination).
- [ ] **Cross-source leakage** — why drawing positives and negatives from different corpora
      lets `URL_Length` act as a source label (UNB median 101 chars vs PhishTank 57).
- [ ] **Five trivial features ≈ the pipeline** — the new 3a result: 5 lexical domain features alone
      reach 0.875, so the gain isn't phishing structure, it's the same source confound amplified.
- [ ] **Base-rate maths** — precision(π) = π·TPR / [π·TPR + (1−π)·FPR]; why precision falls
      to ~0.10 at 1% prevalence while recall is unchanged.
- [ ] **Train/test contamination** — why a coarse binary space duplicates rows, and what the
      109 contradictory feature vectors mean (irreducible error floor).
- [ ] **Correlation choice** — why Spearman over Pearson here (binary/ordinal features).

---

### Quick file inventory

| File | Purpose |
|------|---------|
| `phishing_critical_repro.ipynb` | Executable analysis (data loading → EDA → feature creation → models → 3 experiments → error analysis) |
| `Phishing_Critical_Evaluation_Report.pdf` | 8-section written report (final, submit this) |
| `Phishing_Critical_Evaluation_Report.docx` | Editable report source (re-export the PDF from here) |
| `requirements.txt` | Dependencies (tested versions noted inline) |
| `README.md` | Project description, links, dataset source, run instructions |
| `DataFiles/` | Committed datasets (modelling half is self-contained) |
| `original_source/` | Author's unmodified files, for verifiable comparison |
