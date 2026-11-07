# Data

The current [Phase III cleaning notebook](../phase3/cleaning.ipynb) combines Gallup approval ratings and Brookings political podcast metadata for **February 2021–December 2024**. Six exported CSVs are included in `clean/`. The combined dataset has **47 monthly observations and 17 columns**; December 2022 has no approval observation, leaving 46 months for analyses requiring approval.

## Raw data

[Download the project's raw CSV files from Google Drive](https://drive.google.com/drive/folders/1Qq1Ne2AHGYFrRtM5lEPPehE-ikWU0Dv6?usp=drive_link).

| Filename | Source | Contents |
| --- | --- | --- |
| `bidenApprovalRating.csv` | [Gallup](https://news.gallup.com/poll/329384/presidential-approval-ratings-joe-biden.aspx) | Approval ratings and polling dates |
| `podcast_full-dataset.csv` | [Brookings Popular Political Podcast Dataset](https://politicalpodcastproject.shinyapps.io/dataset/) | Episode titles, descriptions, dates, show names, and political leanings |

The raw files are hosted externally. For Phase III, place them in `data/raw/`, which is ignored by Git, and launch the notebook from `phase3/`. Create `data/clean/` before running; the notebook does not create its output directory. See the [Phase III setup instructions](../phase3/README.md#running-locally). Use the project snapshot to reproduce the saved results, since a new source download may differ.

The older Phase II notebook instead expects raw files alongside itself in `phase2/` and writes its outputs there. Its [setup instructions](../phase2/README.md#running-locally) and saved results describe the earlier cleaning rule.

## Included cleaned datasets

The following counts describe the included Phase III exports. Running the cleaning notebook overwrites these files; some are also used as intermediate saving points.

| File in `data/clean/` | Rows × columns | Contents |
| --- | --- | --- |
| [bidenApprovalRatingClean.csv](clean/bidenApprovalRatingClean.csv) | 47 × 2 | `Date` (first day of month), `Approval_Proportion` |
| [podcastDataCleaned.csv](clean/podcastDataCleaned.csv) | 56,042 × 9 | `Show Name`, `Full Date`, `Title`, `Description`, `Partisan Leaning`, `Biden_mention`, `Biden_mention_incl_hunter`, `Hunter_only`, `Month` |
| [monthlyPodcastData.csv](clean/monthlyPodcastData.csv) | 47 × 6 | `Month`, `Total_episodes`, `Biden_episodes`, `Biden_episodes_incl_hunter`, `Mention_Proportion`, `Mention_Proportion_InclHunter` |
| [hunter_only_review.csv](clean/hunter_only_review.csv) | 554 × 8 | Flagged Hunter-only episodes; same fields as the cleaned episode table except `Month` |
| [showMonthlyData.csv](clean/showMonthlyData.csv) | 4,033 × 6 | `Show Name`, `Partisan Leaning`, `Month`, `Episodes`, `Biden_episodes`, `Show_Mention_Proportion` |
| [combinedMonthlyProportions.csv](clean/combinedMonthlyProportions.csv) | 47 × 17 | Approval ratings, monthly mention rates, political-leaning comparisons, and month counter |

Episode, show-by-month, and monthly-podcast `Month` fields use `YYYY-MM`; `Date` in the approval export and `Month` in the combined export use `YYYY-MM-DD` with the first day of the month. Empty approval values represent missing data.

## Combined dataset columns

| Column | Description |
| --- | --- |
| `Month` | Month, represented by its first day |
| `Total_episodes` | Number of included episode records |
| `Biden_episodes` | Number of records with a positive main Biden mention indicator |
| `Mention_Proportion` | `Biden_episodes / Total_episodes` |
| `Mention_Proportion_InclHunter` | Mention proportion also counting Hunter-only episodes |
| `Approval_Proportion` | Average monthly approval as a proportion |
| `Conservative_Mention` | Main mention proportion for `More Conservative` podcasts |
| `Moderate_Mention` | Main mention proportion for `Moderate` podcasts |
| `Liberal_Mention` | Main mention proportion for `More Liberal` podcasts |
| `Unknown_Mention` | Main mention proportion for podcasts with `Unknown` leaning |
| `Liberal_Conservative_Difference` | `Liberal_Mention - Conservative_Mention` |
| `Conservative_Mention_InclHunter` | Conservative mention proportion counting Hunter-only episodes |
| `Moderate_Mention_InclHunter` | Moderate mention proportion counting Hunter-only episodes |
| `Liberal_Mention_InclHunter` | Liberal mention proportion counting Hunter-only episodes |
| `Unknown_Mention_InclHunter` | Unknown-leaning mention proportion counting Hunter-only episodes |
| `Liberal_Conservative_Difference_InclHunter` | `Liberal_Mention_InclHunter - Conservative_Mention_InclHunter` |
| `Month_Number` | Counter from 1 (February 2021) to 47 (December 2024); December 2022 remains month 23 |

Approval and mention proportions use a 0–1 scale. Difference columns can be negative: a positive liberal-minus-conservative difference means a higher liberal mention proportion; a negative value means a higher conservative mention proportion.

## Processing notes

- Gallup percentages are converted to proportions. The two cross-month polling periods are assigned to their midpoint months; multiple polls within a month are averaged equally.
- December 2022 retains a missing approval value. January 2021 and January 2025 are excluded as partial months. The month counter is created before any missing approval observation is excluded from analysis.
- Podcast cleaning fills missing descriptions with empty strings and removes 144 exact duplicate rows, as recorded in the notebook. Records with matching show, date, and title but different descriptions are retained. Filtering to the study period leaves 56,042 episode records.
- Mentions use a case-insensitive, whole-word “Biden” match in the title or description, counting an episode once. `Biden_mention_incl_hunter` counts any such match. `Hunter_only` flags episodes containing “Hunter Biden” with no remaining whole-word “Biden” after that phrase is removed from both fields. The main `Biden_mention` sets only these flagged episodes to zero, retaining episodes that also contain another Biden mention.
- There are 13,360 main-measure mentions and 554 Hunter-only episodes. The review export and notebook sample inspection document uncertain cases; the flag is a text-matching rule, not a guarantee that Joe Biden is never discussed indirectly.
- All episodes, including Hunter-only episodes, remain in the denominators. Episode counts are aggregated overall and by source-provided political leaning, then left-joined to monthly approval data. `Unknown` episodes contribute to overall totals and have their own rate.
- Combined monthly rates weight episodes equally, so frequently publishing shows contribute more records. `showMonthlyData.csv` contains observed show-by-leaning-by-month groups and their main mention rates, supporting subsequent equal-show averages and leave-one-show-out comparisons. It does not include zero-episode groups or Hunter-inclusive show rates.

These measures describe mentions in metadata, not spoken mentions, sentiment, or listening time. The sample covers selected popular podcasts, and text matching may miss indirect references or count other uses of the surname. See the [Phase III notebook](../phase3/cleaning.ipynb) for current preparation details and the [Phase II notebook](<../phase2/Phase II.ipynb>) and [PDF report](<../phase2/Phase II.pdf>) for earlier exploratory results under the original mention rule.
