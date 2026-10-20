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

See [data/README.md](data/README.md) for filenames, variables, and processing notes.

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
└── data/
    └── README.md
```

- [Phase 1](phase1/README.md): original dataset ideas, sources, and reviewer questions.
- [Phase 2](phase2/README.md): notebook with saved outputs, PDF report, and preregistration.
- [Data](data/README.md): documentation and the link to the raw files.

The original Phase 1 proposal explored election forecasting using prediction markets, polls, and election results. Phase 2 develops the approval-rating and podcast project described above.

## Viewing and running the analysis

Open the [Phase II PDF](<phase2/Phase II.pdf>) to read the report, or the [notebook](<phase2/Phase II.ipynb>) to inspect the code and saved outputs.

To run locally, use Python 3.12 or newer, install [requirements.txt](requirements.txt), and download the two raw CSVs linked above. See [Phase 2 setup instructions](phase2/README.md#running-locally) for the commands and file placement.

## AI assistance acknowledgment

OpenAI Codex, an AI coding assistant, was used to organize the repository, draft the README files from the supplied project materials, copy the notebook’s existing preregistration into a separate Markdown file, and update setup and dependency documentation. The notebook and PDF contents were preserved unchanged during this organization work. The team remains responsible for the submitted content.
