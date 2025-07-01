# Codeforces Contest & User Data Analysis (2024)

## Project Overview
This project, conducted as part of a Data Science course at Universidad del Pacífico in the second semester of 2024, analyzes competitive programming data from the Codeforces platform using its official API. The focus is on contests held between July and December 2024, specifically those with "Hello," "Round," or "Good Bye" in their titles. By applying data extraction, wrangling, visualization, and statistical analysis, the project explores user participation, problem-solving patterns, and performance trends, providing insights into competitive programming behavior.

## Objectives
- Analyze user participation and performance across selected Codeforces contests.
- Examine problem-solving efficiency through submission times and problem difficulty.
- Investigate the relationship between users' prior ratings and their performance outcomes.
- Develop skills in API data extraction, data wrangling, and visualization using Python.

## Dataset
Data was extracted from the Codeforces API for contests between July and December 2024, filtered by titles containing "Hello," "Round," or "Good Bye." The following endpoints were used:
- **contest.list**: Lists all available contests.
- **contest.standings**: Provides contest standings and problem details.
- **contest.status**: Retrieves submission data.
- **contest.ratingChanges**: Tracks users' rating changes post-contest.
- **user.ratedList**: Supplies participant metadata.

### Data Organization
- Raw data for each of the 57 contests is stored in folders named `contest_[ID]/` (e.g., `contest_1995/`), containing CSV files: `standings_rows.csv`, `submissions.csv`, `rating_changes.csv`, `standings_problems.csv`, and `contest_rated_users.csv`.
- These files were consolidated into a single dataset, `base_final.csv`, with 48 columns and rows per participant.

### Dataset Structure
| Column              | Description                                                                 |
|---------------------|-----------------------------------------------------------------------------|
| `author_handle`     | Unique username of the participant.                                         |
| `finished_1` to `finished_8` | Binary indicators (1 = solved, 0/NaN = not solved) for problems 1–8. |
| `1_language` to `8_language` | Programming language used for each problem (e.g., C++20, Python 3). |
| `relative_time_1` to `relative_time_8` | Time (seconds) from contest start to submission for each problem. |
| `time_to_answer_1` to `time_to_answer_8` | Time between consecutive problem submissions.         |
| `rating_1` to `rating_8` | Difficulty rating of each problem.                             |
| `rating_achieved`   | Sum of ratings for problems solved by the participant.                     |
| `contest_name`      | Name of the contest (e.g., "Codeforces Round 961 (Div. 2)").              |
| `contest_start_time`| Contest start time (datetime format).                                      |
| `country`           | Participant’s country (may be missing).                                    |
| `city`              | Participant’s city (may be missing).                                       |
| `rating`            | Participant’s rating before the contest.                                   |
| `max_rating`        | Participant’s highest-ever rating.                                         |

## Methodology
### Data Extraction
- Used the `requests` library to query Codeforces API endpoints for contests from July to December 2024.
- Filtered contests by title keywords and stored raw data in per-contest folders as CSV files.

### Data Consolidation
- Developed a `consolidar_archivo` function to merge CSV files across 57 contests into five consolidated files.
- Handled empty files (e.g., missing `rating_changes.csv` for some contests) with error logging.

### Data Wrangling
- Extracted user handles and problem-solving status (`finished_n`) from nested JSON fields.
- Derived variables:
  - `n_language`: Programming language per problem, based on first correct submission.
  - `relative_time_n`: Time from contest start to submission.
  - `time_to_answer_n`: Incremental time between consecutive submissions.
  - `rating_n`: Problem difficulty ratings, aligned by problem type (A, B, C, etc.).
  - `rating_achieved`: Sum of ratings for solved problems.
- Converted UNIX timestamps to datetime format.
- Merged user metadata (`country`, `city`, `rating`, `max_rating`) and saved the final dataset as `base_final.csv`.

### Visualizations
The following visualizations were created using `matplotlib` and `seaborn`:
1. **Histogram of Submission Times**:
   - For Problem 1: Right-skewed distribution with a peak around 100 minutes.
   - Across all problems: Decreasing submission rates for later problems, with early peaks at 50–100 minutes.
2. **Kernel Density Plot of Maximum Ratings**:
   - Bimodal distribution with peaks at ~2100 and ~3000 points.
   - By rating group: Candidate Master+ (max_rating > 1900) dominates, indicating a competitive sample.
3. **Boxplots of Language vs. Time to Answer**:
   - Go, Kotlin 1.7, D, and Java 21 show faster solving times; PyPy 3 and PyPy 2 are slower.
   - Per-problem analysis reveals consistent language performance trends.
4. **Binscatter of Rating vs. Time to Answer**:
   - Average time peaks at the 2300–2605 rating bin, decreasing for higher ratings.
   - Similar trend for average time across all problems, with a low at 2950–3140.
5. **Linear Regression of Rating vs. Rating Achieved**:
   - Strong positive correlation: higher-rated users achieve higher `rating_achieved`.
   - Candidate Master+ group shows a steeper slope, reflecting stronger performance.

Each visualization includes a footnote on excluded missing or extreme values and a detailed interpretation.

### Causal Analysis
- A linear regression model was fitted to explore the relationship between `rating` and `rating_achieved`.
- Results show a positive correlation, with higher-rated users solving more difficult problems, though dispersion indicates variability in performance.

## Deliverables
- **Jupyter Notebook**: `[UPID]_hw1_2025_1.ipynb` contains all code for data consolidation, wrangling, visualization, and analysis, with markdown explanations.
- **Data Files**: Raw CSV files in `contest_[ID]/` folders and the consolidated `base_final.csv`.
- **Visualizations**: Labeled plots with interpretations, embedded in the notebook.
- **Requirements**: `requirements.txt` lists dependencies (`requests`, `pandas`, `matplotlib`, `seaborn`, `numpy`).

## Repository Structure
- **Branch**: `[UPID]_hw1_2025_1` (e.g., `123456_hw1_2025_1`)
- **Folder**: `hw1/[UPID]_hw1_2025_1/`
- **Files**:
  - `requirements.txt`: Python library dependencies.
  - `[UPID]_hw1_2025_1.ipynb`: Jupyter Notebook with analysis.
  - `base_final.csv`: Consolidated dataset.
  - `contest_[ID]/`: Folders with raw CSV files for each contest.

## Setup Instructions
1. **Clone the Repository**:
   ```bash
   git clone <repository_url>
   git checkout [UPID]_hw1_2025_1