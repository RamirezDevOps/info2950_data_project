# INFO 2950 Data Project

## Project overview

This project examines the relationship between Joe Biden’s presidential approval rating and how often he is mentioned in political podcast titles and descriptions. The analysis combines Gallup approval ratings with Brookings podcast metadata by month, covering **February 2021–December 2024**. January 2021 and January 2025 are excluded because they are partial months of his presidency.

## Team members

- Anderson Ramirez — ar2527
- Jackson Rhamy — jtr84

## Research questions

1. What is the relationship between Biden’s presidential approval rating and his mention rate in political podcast metadata?
2. Does that relationship vary by political leaning, particularly between conservative and liberal podcasts?
3. Did Biden’s mention frequency decline over his presidency after accounting for changes in approval?

## Data sources

- [Gallup: Presidential Approval Ratings — Joe Biden](https://news.gallup.com/poll/329384/presidential-approval-ratings-joe-biden.aspx)
- [Brookings: Popular Political Podcast Dataset](https://politicalpodcastproject.shinyapps.io/dataset/)
- [Project raw CSV files](https://drive.google.com/drive/folders/1Qq1Ne2AHGYFrRtM5lEPPehE-ikWU0Dv6?usp=drive_link)

See [data/README.md](data/README.md) for filenames, variables, and processing notes. The latest preparation workflow is [Phase III data cleaning](phase3/README.md), with six exported CSVs included in `data/clean/`. The combined dataset now has **47 rows and 17 columns**; December 2022 has no approval observation, leaving 46 months for analyses requiring approval.

## Repository structure

```text
.
├── README.md
├── requirements.txt
├── phase1/
│   ├── README.md
│   └── Phase 1 Document.pdf
├── phase2/
│   ├── README.md
│   ├── Phase II.ipynb
│   ├── Phase II.pdf
│   └── preregistration.md
├── phase3/
│   ├── README.md
│   └── cleaning.ipynb
└── data/
    ├── README.md
    └── clean/
        ├── bidenApprovalRatingClean.csv
        ├── podcastDataCleaned.csv
        ├── monthlyPodcastData.csv
        ├── hunter_only_review.csv
        ├── showMonthlyData.csv
        └── combinedMonthlyProportions.csv
```

- [Phase 1](phase1/README.md): original dataset ideas, sources, and reviewer questions.
- [Phase 2](phase2/README.md): notebook with saved outputs, PDF report, and preregistration.
- [Phase 3](phase3/README.md): revised cleaning notebook, exported datasets, and reproduction instructions.
- [Data](data/README.md): cleaned dataset schemas and the link to the external raw files.

The original Phase 1 proposal explored election forecasting using prediction markets, polls, and election results. Phase 2 develops the approval-rating and podcast project described above. Phase 3 revises its data preparation following TA feedback, retaining episodes that mention both Hunter and another Biden, flagging Hunter-only episodes for review, calculating alternative rates that count those episodes, and exporting a show-by-month table. A separate Phase III analysis report is not currently included.

## Viewing and running the analysis

Open the [Phase III cleaning notebook](phase3/cleaning.ipynb) for the current preparation code and saved outputs, or use the included [cleaned CSVs](data/clean/). The [Phase II PDF](<phase2/Phase II.pdf>) and [notebook](<phase2/Phase II.ipynb>) preserve the earlier exploratory analysis and mention-counting rule.

To reproduce the current cleaning, use Python 3.12 or newer and follow the [Phase 3 setup instructions](phase3/README.md#running-locally). Place the raw CSVs in `data/raw/` and launch the notebook from `phase3/`; it writes to `data/clean/`. The raw-data directory is ignored by Git. For the older exploratory analysis, follow the separate [Phase 2 setup instructions](phase2/README.md#running-locally).

## AI assistance acknowledgment

OpenAI Codex, an AI coding assistant, was used to organize the repository, draft and update the README files from the supplied project materials, copy the notebook’s existing preregistration into a separate Markdown file, and update setup and dependency documentation. This README update documents the Phase III notebook and cleaned exports without changing or rerunning the notebooks. The Phase III notebook contains its own acknowledgment of Claude assistance during its revision. The team remains responsible for the submitted content.
