# Phase 3: Revised data cleaning

[cleaning.ipynb](cleaning.ipynb) prepares Gallup approval ratings and Brookings political podcast metadata for the Biden approval and podcast mention project. It includes saved outputs and exports six CSVs to [data/clean/](../data/clean/). A separate Phase III analysis notebook or report is not currently included in this repository.

## Changes since Phase 2

- Count episodes mentioning both Hunter and another Biden in the main `Biden_mention` measure, rather than setting all episodes mentioning Hunter Biden to zero.
- Flag episodes with no remaining whole-word “Biden” after removing “Hunter Biden” as `Hunter_only`, and save them for review.
- Calculate alternative overall and political-leaning mention rates that count Hunter-only episodes as mentions. All episodes remain in the denominators under both rules.
- Save each show's monthly mention proportion so subsequent analyses can give shows equal weight and compare results when individual shows are omitted.
- Add `Month_Number` from 1 to 47 before dropping any missing approval observations, preserving each month's position in time.

The exports cover February 2021–December 2024: 56,042 episode records, including 13,360 main-measure Biden mentions and 554 flagged Hunter-only episodes. The combined dataset has 47 rows and 17 columns. December 2022 retains a missing approval value, leaving 46 usable months for analyses requiring approval. See the [data documentation](../data/README.md) for schemas and processing details.

## Running locally

Use **Python 3.12 or newer** because the notebook contains f-string syntax requiring Python 3.12+. The cleaning notebook imports pandas, NumPy, and DuckDB. From the repository root:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install pandas numpy duckdb jupyterlab
mkdir -p data/raw data/clean
```

The root [requirements.txt](../requirements.txt) lists the broader Phase II analysis dependencies; the command above installs the packages used by this cleaning notebook. Neither setup is a complete lockfile for the original environment.

Download the two raw files from the [project Google Drive folder](https://drive.google.com/drive/folders/1Qq1Ne2AHGYFrRtM5lEPPehE-ikWU0Dv6?usp=drive_link) and place them as follows:

```text
data/
├── raw/
│   ├── bidenApprovalRating.csv
│   └── podcast_full-dataset.csv
└── clean/
```

`data/raw/` is ignored by Git. Launch JupyterLab from `phase3/` so the notebook's `../data/` paths resolve:

```bash
cd phase3
jupyter lab cleaning.ipynb
```

Run all cells in order. The notebook expects the output directory to exist and overwrites the six CSVs in `data/clean/`, including intermediate versions of some files as cleaning progresses. Use the supplied raw snapshot to reproduce the saved outputs; a fresh source download may differ.

## Exported files

| File in `data/clean/` | Rows | Contents |
| --- | ---: | --- |
| `bidenApprovalRatingClean.csv` | 47 | Monthly approval proportions |
| `podcastDataCleaned.csv` | 56,042 | Cleaned episodes, mention flags, and month |
| `monthlyPodcastData.csv` | 47 | Monthly episode totals and both mention rates |
| `hunter_only_review.csv` | 554 | Episodes flagged as Hunter-only for manual review |
| `showMonthlyData.csv` | 4,033 | Observed show-by-leaning-by-month groups and main mention rates |
| `combinedMonthlyProportions.csv` | 47 | Approval, overall and leaning mention rates, differences, and month counter |

The combined mention rates weight episodes equally. The show-by-month export enables later equal-show averages; it does not change the combined rates or include Hunter-inclusive show rates. The notebook prepares data and does not fit the preregistered regressions. The [Phase II preregistration](../phase2/preregistration.md) records the earlier analysis plan.

This documentation update did not change or rerun the notebook. Its AI acknowledgment describes Claude assistance during the Phase III revision; repository documentation assistance is acknowledged in the [main README](../README.md#ai-assistance-acknowledgment).
