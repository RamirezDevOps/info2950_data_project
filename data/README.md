# Data

The project combines Gallup approval ratings and Brookings political podcast metadata by month. The analysis-ready combined dataset has **47 monthly observations and 10 columns**, as documented in the notebook, covering February 2021 through December 2024.

## Raw data

[Download the project’s raw CSV files from Google Drive](https://drive.google.com/drive/folders/1Qq1Ne2AHGYFrRtM5lEPPehE-ikWU0Dv6?usp=drive_link).

| Filename expected by the notebook | Source | Contents |
| --- | --- | --- |
| `bidenApprovalRating.csv` | [Gallup](https://news.gallup.com/poll/329384/presidential-approval-ratings-joe-biden.aspx) | Approval ratings and polling dates |
| `podcast_full-dataset.csv` | [Brookings Popular Political Podcast Dataset](https://politicalpodcastproject.shinyapps.io/dataset/) | Episode titles, descriptions, dates, show names, and political leanings |

CSV files are hosted externally and are not included in this repository. For local execution, place both source CSVs in `phase2/` and launch the notebook from there. The notebook uses filenames relative to its working directory; it does not automatically read from this `data/` folder. See [setup instructions](../phase2/README.md#running-locally).

## Generated datasets

Running the notebook writes these files to its working directory (`phase2/` with the documented setup). Intermediate files are overwritten as cleaning progresses.

| Filename | Contents |
| --- | --- |
| `bidenApprovalRatingClean.csv` | Monthly approval proportions |
| `podcastDataCleaned.csv` | Cleaned episode records and mention indicators |
| `monthlyPodcastData.csv` | Monthly episode counts and mention proportions |
| `combinedMonthlyProportions.csv` | Combined approval and podcast summaries |

## Combined dataset columns

| Column | Description |
| --- | --- |
| `Month` | Month, represented by its first day |
| `Total_episodes` | Number of included episode records |
| `Biden_episodes` | Number of records with a positive Biden mention indicator |
| `Mention_Proportion` | `Biden_episodes / Total_episodes` |
| `Approval_Proportion` | Average monthly approval as a proportion |
| `Conservative_Mention` | Mention proportion for `More Conservative` podcasts |
| `Moderate_Mention` | Mention proportion for `Moderate` podcasts |
| `Liberal_Mention` | Mention proportion for `More Liberal` podcasts |
| `Unknown_Mention` | Mention proportion for podcasts with `Unknown` leaning |
| `Liberal_Conservative_Difference` | Liberal mention proportion minus conservative mention proportion |

Approval and mention proportions use a 0–1 scale. A positive liberal-minus-conservative difference means a higher liberal mention proportion; a negative value means a higher conservative mention proportion.

## Processing notes

- Gallup percentages are converted to proportions. Polls are assigned to months, using representative dates in the midpoint month for two cross-month polling periods, and multiple polls within a month are averaged equally.
- December 2022 retains a missing approval value. January 2021 and January 2025 are excluded as partial months.
- Podcast cleaning fills missing descriptions with empty strings and removes 144 exact duplicate rows, according to the notebook. Records with matching show, date, and title but different descriptions are retained.
- A mention is a case-insensitive, whole-word “Biden” match in the title or description. The code sets the indicator to zero if either field contains “Hunter Biden”; those records remain in the episode totals.
- Episode records are aggregated by month, overall and by source-provided political leaning, then joined to monthly approval data.

These measures describe mentions in metadata, not spoken mentions, sentiment, or listening time. The sample covers selected popular podcasts, and frequently publishing shows contribute more records. See the [notebook](<../phase2/Phase II.ipynb>) and [PDF report](<../phase2/Phase II.pdf>) for the full cleaning process and limitations.
