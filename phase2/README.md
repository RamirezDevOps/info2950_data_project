# Phase 2: Exploratory analysis and hypotheses

## Files

- [Phase II.ipynb](<Phase II.ipynb>): analysis notebook with saved outputs.
- [Phase II.pdf](<Phase II.pdf>): PDF report containing the analysis and preregistration.
- [preregistration.md](preregistration.md): hypotheses, proposed analyses, and reviewer questions copied from the notebook.
- [Data documentation](../data/README.md): raw-data link, filenames, and variable descriptions.

The notebook and report cover research questions, data collection and cleaning, data descriptions, limitations, exploratory analysis, and preregistration. The analysis uses 47 months from February 2021 through December 2024. December 2022 remains missing for approval ratings and is excluded in the planned regressions.

The exploratory analysis includes summary statistics, plots, Pearson and Spearman correlations, and variance inflation factors. The two preregistered regressions are proposed analyses; they are not fitted in this notebook.

## Relationship to Phase 3

This notebook preserves the Phase II workflow and its original 10-column combined dataset. It sets the mention indicator to zero whenever either metadata field contains “Hunter Biden,” including episodes that also mention Joe Biden. The [Phase III cleaning notebook](../phase3/README.md) revises that rule, adds Hunter-only review and alternative mention measures, and exports a 17-column combined dataset plus a show-by-month table to `data/clean/`. Use those exports for the current data preparation; the saved Phase II results describe the earlier rule.

## Running locally

Use **Python 3.12 or newer** because the notebook contains f-string syntax requiring Python 3.12+. From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements.txt
python -m pip install jupyterlab
```

Download the [raw CSV files](https://drive.google.com/drive/folders/1Qq1Ne2AHGYFrRtM5lEPPehE-ikWU0Dv6?usp=drive_link) and place these two files alongside the notebook in `phase2/`:

```text
phase2/
├── Phase II.ipynb
├── bidenApprovalRating.csv
└── podcast_full-dataset.csv
```

Launch JupyterLab from `phase2/` so the notebook’s relative CSV paths resolve:

```bash
cd phase2
jupyter lab "Phase II.ipynb"
```

Run all cells in order. The notebook writes or overwrites `bidenApprovalRatingClean.csv`, `podcastDataCleaned.csv`, `monthlyPodcastData.csv`, and `combinedMonthlyProportions.csv` in its working directory (`phase2/` with this setup). These are Phase II outputs; this notebook does not read from or write to `data/clean/`. Phase III uses a separate [setup and export workflow](../phase3/README.md#running-locally).

The requirements file preserves the specified Statsmodels version; other analysis dependencies are unpinned. It is not a complete lockfile for the original environment. The notebook and PDF were left unchanged during this documentation update, and the analysis was not rerun.
