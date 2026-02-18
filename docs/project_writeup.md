# Project 1: Home-Field Advantage in the NFL (2000-2023)

## 1) Problem Definition
### Research question
To what extent does home-field advantage influence NFL game outcomes, and how has that effect changed from 2000-2023?

### Why this question matters
Home-field advantage is one of the most cited ideas in sports analytics, but its strength may shift over time as league rules, travel practices, and game environments change. This question is useful for fans, analysts, and anyone building sports narratives from historical outcomes.

### Scope choice
This is an exploratory analysis, not a predictive model. The goal is to describe patterns and trends, then interpret them carefully.

## 2) Data Description and Understanding
### Data source
- Source: nflverse `games.csv`
- URL: https://github.com/nflverse/nfldata/raw/master/data/games.csv

### What each row represents
Each row is one NFL game.

### Key columns used
- `season`
- `game_type`
- `home_score`
- `away_score`
- `game_id`

### Sample size (explicit)
- Raw file: 7,276 games (1999-2025)
- After filtering to 2000-2023: 6,447 games
- Final analysis sample (regular season only): 6,175 games across 24 seasons
- Average games per season: 257.3 (range 248-272)
- Ties: 14 games (0.23%)

### What may be missing
The dataset does not directly encode mechanisms such as attendance intensity, detailed travel burden, team health, or coaching quality. These omissions matter when interpreting causes.

## 3) Cleaning and Preparation Decisions
This section emphasizes decisions and tradeoffs, not just steps.

### Decision A: Restrict to seasons 2000-2023
Why: long enough for trend analysis, while keeping focus on modern-era NFL conditions.

Tradeoff: excludes older historical context and avoids possible partial/incomplete latest-season effects.

### Decision B: Focus main claims on regular season
Why: regular season gives the most stable and comparable year-to-year sample size.

Important note: playoff rows in this dataset are labeled `WC`, `DIV`, `CON`, and `SB` (not `POST`), so the saved `games_post_2000_2023_clean.csv` is empty under the original filter logic. To avoid misrepresenting results, final claims are anchored to the clean regular-season sample.

### Decision C: Coerce scores to numeric and drop invalid rows
- Converted `home_score` and `away_score` with `errors="coerce"`
- Dropped rows with missing scores

Why: prevents hidden data-type failures when computing winners and margins.

Result: 0 rows removed in the regular-season sample, but this is still a necessary integrity check.

### Decision D: Encode outcomes and ties explicitly
- `home_win = 1` if home score > away score
- `home_win = 0` if home score < away score
- `home_win = NaN` for ties
- `home_tie` indicator created separately

Why: treating ties separately avoids biasing win-rate metrics.

### Decision E: Validate uniqueness
Checked `game_id.nunique() == len(df_reg)` (6,175 = 6,175), confirming one game per row.

## 4) Data Understanding and Visualization
### Visuals used
- Home win rate by season (`visuals/home_win_trend.png`)
- Home win rate + rolling trend (`visuals/rolling_avg.png`)
- Home margin distribution (`visuals/margin_distribution.png`)

### Why these visuals
- Seasonal line plot: reveals year-to-year variation and broader direction.
- Rolling trend line: isolates medium-term movement from seasonal noise.
- Margin distribution: adds context beyond binary win/loss outcomes.

### 5-year rolling average choice (why not 2- or 3-year?)
I selected a 5-year window because 2- and 3-year windows were still too sensitive to short-run volatility.

Observed smoothness (mean absolute year-to-year change in smoothed series):
- 2-year: 0.0147
- 3-year: 0.0112
- 5-year: 0.0051
- 7-year: 0.0050

Interpretation: 5-year keeps meaningful trend shifts visible (including 2020 disruption) while reducing short-term noise; 7-year adds little extra stability but over-smooths change.

## 5) Storytelling and Interpretation
### Core finding
Home teams won 56.26% of regular-season games in this sample, indicating a persistent home-field advantage.

### Trend finding
The effect appears weaker than in the early 2000s.

- Highest season: 2003 at 61.33%
- Lowest season: 2020 at 49.80%
- 2000-2008 average: 57.03%
- 2015-2023 average: 54.84%
- Difference: about -2.19 percentage points

### Margin context
Mean home score = 23.17, mean away score = 20.94, so average home margin is about +2.23 points.

### Interpretation statement
The best-supported claim is not that home-field advantage disappeared, but that its magnitude narrowed over time, with a major disruption around 2020 and partial rebound afterward.

## 6) Limitations, Assumptions, and Reflection
### Limits of causal interpretation
This project is descriptive. It identifies patterns but does not isolate causal drivers.

### Key limitations
- No control variables for team strength, QB quality, injuries, or coaching.
- No direct attendance variable.
- Neutral/international context not separately modeled in trend calculations.
- Postseason comparison not included in final claims due game-type label mismatch in the existing pipeline.

### Assumptions
- `game_id` uniquely identifies games.
- Score fields are valid after coercion and missing-value filtering.
- Seasonal aggregation is appropriate for a long-run league-level trend question.

### Reflection
The largest practical takeaway is that small percentage changes still matter at league scale but should not be overclaimed. This reinforces a central data-science principle: uncertainty and context are part of the result.

## 7) References and Transparency
### Data reference
- nflverse `games.csv`: https://github.com/nflverse/nfldata/raw/master/data/games.csv

### Tooling transparency
- Analysis was performed in Python with pandas/matplotlib/seaborn.
- This write-up includes explicit rationale for preprocessing and smoothing choices to make the decision process auditable.
