# DTSC-2301 Project 1
## Home-Field Advantage in the NFL (2000-2023)

### Course
DTSC-2301 Data Science Foundations, UNC Charlotte

## 1) Problem Definition
### Research question
To what extent does home-field advantage influence NFL game outcomes, and how has that effect changed from 2000-2023?

### Why this question matters
Home-field advantage is one of the most common claims in sports analytics, but its magnitude may shift over time due to league, travel, and game-environment changes. This question is relevant to analysts, fans, and anyone making data-based sports claims.

### Scope
This project is exploratory analysis, not prediction.

## 2) Data Description and Understanding
### Data source
- Source: nflverse `games.csv`
- URL: https://github.com/nflverse/nfldata/raw/master/data/games.csv

### What each row represents
Each row is one NFL game.

### Key variables used
- `season`
- `game_type`
- `home_score`
- `away_score`
- `game_id`

### Sample size
- Raw file: 7,276 games (1999-2025)
- After filtering to 2000-2023: 6,447 games
- Final analysis sample (regular season only): 6,175 games across 24 seasons
- Average games per season: 257.3 (range 248-272)
- Ties: 14 games (0.23%)

### What the data does not directly capture
The dataset does not directly include attendance intensity, detailed travel burden, injuries, or team/coaching quality controls. Those missing factors matter for causal interpretation.

## 3) Cleaning and Preparation Decisions
### Decision A: Restrict to seasons 2000-2023
Why: long enough for trend analysis while staying focused on the modern NFL era.

Tradeoff: excludes older historical context and avoids potential incomplete-latest-season effects.

### Decision B: Focus main claims on regular season
Why: regular season gives stable year-to-year comparability and large sample size.

Important note: playoff rows are labeled `WC`, `DIV`, `CON`, and `SB` (not `POST`), so the current postseason export logic produces an empty file. Final claims are therefore anchored to the clean regular-season sample.

### Decision C: Coerce scores to numeric and drop invalid rows
- Converted `home_score` and `away_score` with `errors="coerce"`
- Dropped rows missing either score

Why: ensures win/loss and margin calculations are valid.

Result: 0 rows removed from the regular-season sample, but this remains an important integrity check.

### Decision D: Encode wins and ties explicitly
- `home_win = 1` if home score > away score
- `home_win = 0` if home score < away score
- `home_win = NaN` for ties
- Separate `home_tie` indicator

Why: ties should not be incorrectly treated as losses.

### Decision E: Validate one row per game
`game_id.nunique() == len(df_reg)` (6,175 = 6,175), confirming unique game rows.

## 4) Data Understanding and Visualization
### Visual 1: Home win rate by season
![Home win rate by season](./visuals/home_win_trend.png)

### Visual 2: Home win rate with rolling trend
![Home win rate with 5-year rolling average](./visuals/rolling_avg.png)

### Visual 3: Home scoring margin distribution
![Distribution of home margin](./visuals/margin_distribution.png)

### Why these visuals
- Seasonal trend line shows year-to-year movement.
- Rolling trend line separates medium-term signal from seasonal noise.
- Margin distribution adds context beyond binary win/loss outcomes.

### Why a 5-year rolling average (not 2- or 3-year)?
I used 5-year smoothing because 2- and 3-year windows were still too volatile for stable trend interpretation.

Observed smoothness (mean absolute year-to-year change in the smoothed series):
- 2-year: 0.0147
- 3-year: 0.0112
- 5-year: 0.0051
- 7-year: 0.0050

Interpretation: 5-year preserves meaningful shifts (including the 2020 disruption) while reducing short-run noise. A 7-year window adds little extra smoothing but can over-smooth changes.

## 5) Storytelling and Interpretation
### Core finding
Home teams won 56.26% of regular-season games in this sample, indicating a persistent home-field advantage.

### Trend finding
Home-field advantage appears weaker than in the early 2000s.

- Highest season: 2003 at 61.33%
- Lowest season: 2020 at 49.80%
- 2000-2008 average: 57.03%
- 2015-2023 average: 54.84%
- Difference: about -2.19 percentage points

### Margin context
Mean home score = 23.17, mean away score = 20.94, so average home margin is about +2.23 points.

### Interpretation statement
The data supports a narrower claim: home-field advantage has not disappeared, but its magnitude appears to have narrowed over time, with a strong disruption around 2020 and partial rebound afterward.

## 6) Limitations, Assumptions, and Reflection
### Limits
This is descriptive analysis, not causal inference.

### Key limitations
- No controls for team strength, QB quality, injuries, or coaching.
- No direct attendance variable.
- Neutral/international game context not separately modeled.
- Postseason comparison not included in final claims due game-type label mismatch in current pipeline.

### Assumptions
- `game_id` uniquely identifies games.
- Score fields are valid after coercion and missing-value filtering.
- Seasonal aggregation is appropriate for this league-level trend question.

### Reflection
Small percentage-point changes can still matter at league scale, but conclusions must be constrained by uncertainty and omitted variables.

## 7) References and Transparency
### Data reference
- nflverse `games.csv`: https://github.com/nflverse/nfldata/raw/master/data/games.csv

### Tooling transparency
- Analysis performed in Python using pandas, matplotlib, and seaborn.
- Decisions in preprocessing and smoothing are explicitly justified to keep the workflow auditable.

## Repository Notes
- Primary analysis notebooks: `notebooks/00_setup.ipynb`, `notebooks/01_home_field_eda.ipynb`, `notebooks/02_interpretation.ipynb`
- Supplemental long-form write-up: `docs/project_writeup.md`

## License
This repository is licensed under the MIT License.
