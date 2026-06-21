# Submission Checklist — Data Science in Cyber Final Project

Deadline: **Friday, 10 July 2026, 23:59**. Submission = public GitHub repo link emailed to the examiner.

---

## 0. Before you touch git — fill in the placeholders

- [ ] **Report title page** (`Phishing_Critical_Evaluation_Report.pdf`): replace
      `Itay / Student ID: ____________` and the repo URL. *(The PDF is final output —
      regenerate it from the notebook/report builder if you need to edit these, or just
      note your ID is correct before exporting.)*
- [ ] **README.md**: nothing to edit unless you rename files.
- [ ] Confirm this is submitted as an **individual** project (the brief requires it). Your
      regular lab partner should submit their own; do not share the same repo or files.

## 1. Sanity-check the notebook runs clean

- [ ] Fresh environment: `pip install -r requirements.txt`
- [ ] `jupyter notebook phishing_critical_repro.ipynb` → **Kernel ▸ Restart & Run All**
- [ ] All cells run with no errors; figures render; XGBoost accuracy ≈ 0.871.

## 2. Create the public GitHub repo

- [ ] On GitHub: **New repository** → name e.g. `phishing-critical-repro` → **Public** →
      *do not* initialise with a README (you already have one).
- [ ] Copy the repo URL it gives you.

## 3. Push from this folder

Run from inside the unzipped submission folder:

```bash
git init
git add .
git commit -m "Critical reproduction & stress-test of shreyagopal phishing detector"
git branch -M main
git remote add origin https://github.com/<your-username>/phishing-critical-repro.git
git push -u origin main
```

- [ ] If `git push` rejects large files, confirm none exceed 100 MB
      (the largest here is ~4 MB — you are fine; GitHub's hard limit is 100 MB/file).

## 4. Verify the repo looks right on GitHub

- [ ] README renders with the structure tree and the three findings.
- [ ] `phishing_critical_repro.ipynb` previews (GitHub renders notebooks inline).
- [ ] `Phishing_Critical_Evaluation_Report.pdf` opens.
- [ ] `DataFiles/` and `original_source/` are present.
- [ ] Repo is **Public** (Settings → check visibility), so the examiner can open it.

## 5. Email the examiner

- [ ] Send the repo link to the address provided by the examiner.
- [ ] Suggested body: project title, your name + ID, one-line summary
      ("reproduce + critically evaluate the shreyagopal phishing-URL detector"), and the link.

## 6. Be ready for the optional oral

The staff may ask you to explain the work live. Be able to talk through, without notes:

- [ ] **Why 86% is misleading** — the three findings (source leakage, prevalence, contamination).
- [ ] **Cross-source leakage** — why drawing positives and negatives from different corpora
      lets `URL_Length` act as a source label (UNB median 101 chars vs PhishTank 57).
- [ ] **Base-rate maths** — precision(π) = π·TPR / [π·TPR + (1−π)·FPR]; why precision falls
      to ~0.10 at 1% prevalence while recall is unchanged.
- [ ] **Train/test contamination** — why a coarse binary space duplicates rows, and what the
      109 contradictory feature vectors mean (irreducible error floor).
- [ ] **Correlation choice** — why Spearman over Pearson here (binary/ordinal features).

---

### Quick file inventory

| File | Purpose |
|------|---------|
| `phishing_critical_repro.ipynb` | Executable analysis (data loading → EDA → models → 3 experiments) |
| `Phishing_Critical_Evaluation_Report.pdf` | 8-section written report |
| `requirements.txt` | Dependencies (tested versions noted inline) |
| `README.md` | Project description, links, dataset source, run instructions |
| `DataFiles/` | Committed datasets (modelling half is self-contained) |
| `original_source/` | Author's unmodified files, for verifiable comparison |
