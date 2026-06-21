# Phishing Website Detection — Critical Reproduction & Stress-Test

Final project for **Data Science in Cyber** (Dr. Uri Itai). This repository reproduces a
published phishing-URL classifier and critically evaluates whether its reported
performance reflects a genuine phishing detector or an artefact of how the dataset was
built and evaluated.

## Project description

The selected source trains several models (Decision Tree, Random Forest, MLP, XGBoost,
autoencoder) on 17 hand-coded URL features and reports a headline **86.4% XGBoost
accuracy**. We reproduce that number and then test three of its load-bearing assumptions:

1. **Cross-source leakage** — legitimate and phishing URLs are drawn from different
   corpora, so the dominant feature (`URL_Length`, ~0.86 importance) encodes the *source*
   rather than phishing. Visible in the raw URLs before extraction.
2. **Artificial class balance** — the synthetic 50/50 split flatters every metric; at a
   realistic ~1% phishing prevalence, precision collapses from ~0.92 to ~0.10 with the
   model unchanged.
3. **Train/test contamination** — the coarse binary feature space duplicates ~91% of rows;
   ~96% of test rows have an identical twin in training. De-duplicating drops honest
   accuracy to ~0.73, and ~14% of feature vectors carry both labels (an irreducible floor).

**Conclusion:** the accuracy reproduces but does not support the claim of a usable
detector. Recommended as a methodology cautionary study, not for deployment.

## Selected source

- Article / tutorial & original GitHub repository:
  https://github.com/shreyagopal/Phishing-Website-Detection-by-Machine-Learning-Techniques

## Dataset source

- **Phishing URLs:** PhishTank verified online list (`DataFiles/2.online-valid.csv`, 2020 snapshot).
- **Legitimate URLs:** University of New Brunswick benign URL list
  (`DataFiles/1.Benign_list_big_final.csv`).
- **Modelling table:** `DataFiles/5.urldata.csv` — 10,000 rows (5,000 / 5,000), 17 features
  + label. Committed here, so the modelling half is fully self-contained.

> The original *feature-extraction* notebook does **not** reproduce today: it depends on
> the Alexa rank API (discontinued May 2022), live WHOIS lookups (time-dependent), and live
> fetches of 2020 PhishTank URLs (now dead). Failed lookups default to the "phishing"
> value, a further source of bias. We document this rather than work around it.

## Repository contents

```
.
├── phishing_critical_repro.ipynb          # complete, executable analysis notebook
├── Phishing_Critical_Evaluation_Report.pdf # written report (8 sections)
├── requirements.txt
├── README.md
├── DataFiles/                             # committed datasets (sources + final table)
│   ├── 1.Benign_list_big_final.csv        # UNB legitimate source
│   ├── 2.online-valid.csv                 # PhishTank phishing source
│   ├── 3.legitimate.csv  4.phishing.csv   # per-class extracted features
│   └── 5.urldata.csv                      # final 10k-row modelling table
└── original_source/                       # the author's ORIGINAL files, unmodified,
    ├── README_original.md                 #   kept verbatim so every critique is verifiable
    ├── URLFeatureExtraction.py
    ├── URL Feature Extraction.ipynb
    ├── Phishing Website Detection_Models & Training.ipynb
    └── XGBoostClassifier.pickle.dat
```

The `original_source/` folder contains the author's work **unchanged**; all of our analysis
lives in the root notebook and report, so a reader can diff claims against the source.

## Execution instructions

```bash
# Python 3.10+
pip install -r requirements.txt

# from the repository root (so the relative DataFiles/ path resolves)
jupyter notebook phishing_critical_repro.ipynb
# Run all cells top to bottom. A fixed seed (SEED = 12) makes results reproducible.
```

All analysis runs from the committed `DataFiles/5.urldata.csv`; no network access or
external API keys are required.
