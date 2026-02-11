# DTSC-2301-Project-1
Exploratory data science project focused on problem definition, data cleaning, visualization, and interpretation for DTSC-2301 (Data Science Foundations).

# Home-Field Advantage in the NFL (2000–2023)

## Course  
**DTSC-2301 — Data Science Foundations**  
University of North Carolina at Charlotte  

---

## Project Overview

This project investigates the research question:

> **To what extent does home-field advantage influence NFL game outcomes, and how has its impact changed from 2000–2023?**

Rather than building a predictive model, this analysis focuses on:

- Defining a clear, well-scoped exploratory question  
- Cleaning and preparing real-world game-level data  
- Using visualization to identify trends and patterns  
- Interpreting findings while acknowledging limitations and uncertainty  

The goal is to understand whether playing at home meaningfully affects win probability and whether that effect has strengthened, weakened, or remained stable over time.

---

## Dataset

**Source:** nflverse — Game-Level Data (1999–present)  
**CSV File:**  
https://github.com/nflverse/nfldata/raw/master/data/games.csv  

The dataset contains detailed game-level information for NFL games, including:

- Season and week  
- Home and away teams  
- Final scores  
- Game location  
- Playoff indicators  
- Additional contextual variables  

Each row represents a single NFL game.

For this project, the analysis focuses on **regular season games from 2000 through 2023**.

---

## Project Objectives

This project aims to:

1. Quantify overall home win percentage.
2. Analyze trends in home-field advantage over time.
3. Compare regular season vs playoff home advantage.
4. Identify seasons where home advantage strengthened or declined.
5. Reflect on structural changes in the league (rule changes, travel patterns, crowd effects, COVID seasons).

---

## Methods

The project workflow includes:

- Data cleaning and filtering (2000–2023 seasons)
- Handling missing or incomplete records
- Creating derived variables (e.g., home win indicator)
- Aggregating win rates by season
- Visualizing trends using `matplotlib` and `seaborn`
- Interpreting patterns within historical and league context

No predictive modeling is performed. The emphasis is on exploratory analysis and thoughtful interpretation.

---

## How to Run

1. Clone this repository.
2. Install required packages:
3. (Optional but recommended) Create and activate a virtual environment:
4. Open the project in Jupyter:
5. Navigate to the `notebooks/` directory and run:
    - `00_setup.ipynb` (data loading and initial sanity checks)
    - Followed by exploratory notebooks for analysis and visualization

---

## Key Focus Areas

- Exploratory Data Analysis (EDA)
- Visualization-driven reasoning
- Clear communication of insights
- Discussion of limitations and ethical considerations
- Transparency in data sources and assumptions

---

## License

This repository is licensed under the MIT License.


## Notes

This project is part of DTSC-2301 and emphasizes process, reasoning, and communication over prediction accuracy. The goal is to demonstrate thoughtful analytical judgment and clear storytelling using real-world sports data.

The analysis intentionally prioritizes interpretation, transparency, and reflection. Conclusions drawn from the data are discussed with appropriate caution, acknowledging uncertainty, assumptions, and contextual factors that may influence observed trends.

