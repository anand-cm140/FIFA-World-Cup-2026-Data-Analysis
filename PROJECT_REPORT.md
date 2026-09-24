# FIFA World Cup 2026 — AI-Powered Team Performance & Match Analytics

## Project Report

**Program:** IBM SkillsBuild Data Analytics with AI Academic Internship  
**Conducted by:** BharatCares in association with AICTE

---

## Abstract / Executive Summary

This project presents a comprehensive data analytics and AI-driven analysis of the FIFA World Cup 2026 match data. Using a dataset of 104 matches across 48 teams, the project covers the entire data analytics pipeline — from data cleaning and exploratory analysis to KPI computation, trend identification, driver analysis, and machine learning-based match outcome prediction. The analysis reveals that shots on target is the strongest predictor of match outcomes, home teams enjoyed a measurable advantage, and goal difference is strongly correlated with overall tournament success. A Random Forest classifier was trained to predict match outcomes, demonstrating that match statistics contain meaningful predictive signal. The project concludes with data-driven recommendations for performance improvement and future analysis directions.

---

## 1. Introduction

The FIFA World Cup is the most prestigious international football tournament, bringing together national teams from across the globe. The 2026 edition, hosted across North America (United States, Canada, and Mexico), was the largest World Cup in history with 48 participating teams and 104 matches.

This project leverages data analytics and artificial intelligence to extract meaningful insights from the tournament's match data. The analysis goes beyond simple descriptive statistics to include predictive modeling, driver identification, and actionable recommendations.

### 1.1 Problem Statement

> *How can match-level statistics (possession, shots, saves, fouls, etc.) be leveraged to understand team performance patterns, identify key drivers of match outcomes, and predict whether the home team will win, lose, or draw?*

### 1.2 Objectives

1. Clean and preprocess raw match data for reliable analysis
2. Perform comprehensive Exploratory Data Analysis (EDA)
3. Compute and present Key Performance Indicators (KPIs)
4. Identify trends across tournament rounds and dates
5. Determine which match statistics most strongly associate with winning
6. Build a machine learning model to predict match outcomes
7. Generate data-driven insights and actionable recommendations

---

## 2. Dataset Description

| Attribute | Details |
|---|---|
| **Source** | Publicly available FIFA World Cup 2026 match data |
| **File Format** | CSV |
| **Records** | 104 matches |
| **Features** | 42 columns |
| **Tournament Period** | June 11 – July 19, 2026 |
| **Teams** | 48 national teams |
| **Venues** | 17 stadiums |

The dataset contains detailed match-level information including:
- Match metadata (date, round, venue, referee, attendance)
- Team information (home/away team, manager, captain, formation)
- Scores (home_score, away_score)
- Match statistics (possession, shots, shots on target, saves, fouls, corners, crosses, interceptions, offsides, cards)
- Notes (extra time, penalty shoot-outs)

### 2.1 Data Quality Issues Identified

- **Missing scores (4 matches):** Penalty shoot-out matches had null `home_score`/`away_score` values
- **Missing gameweek (32 rows):** Knockout-stage matches don't have gameweek assignments
- **Missing offsides (5 rows):** Some matches had missing offsides data
- **Attendance stored as string:** Required conversion to numeric

---

## 3. Data Preprocessing

The following cleaning steps were performed:

1. **Penalty shoot-out scores:** Extracted from the `score` string column (e.g., "1–1") and filled into `home_score`/`away_score` — restoring all 104 matches to the analysis
2. **Date conversion:** Converted `date` column to datetime format
3. **Attendance conversion:** Removed commas and converted to numeric
4. **Offsides imputation:** Filled missing values with column median
5. **Derived columns created:**
   - `total_goals` — Sum of home and away scores
   - `goal_difference` — Home score minus away score
   - `match_label` — "Home Team vs Away Team" string
   - `match_result` — Categorical: Home Win / Draw / Away Win

---

## 4. Exploratory Data Analysis

### 4.1 Team Performance Analysis

A comprehensive team performance table was computed for all 48 teams, including:
- Matches Played, Wins, Draws, Losses
- Goals Scored, Goals Conceded, Goal Difference
- Win Percentage, Average Possession, Average Shots, Average Shots on Target

### 4.2 Visualizations Created

| # | Visualization | Key Finding |
|---|---|---|
| 1 | Top 10 Teams by Wins | Top teams progressed deepest into knockout rounds |
| 2 | Top 10 Teams by Goals Scored | Attack-heavy teams achieved better tournament results |
| 3 | Top 10 Teams by Goals Conceded | High concession doesn't always indicate poor performance |
| 4 | Top 10 Teams by Goal Difference | GD is a robust summary of overall team performance |
| 5 | Match Result Distribution | Home teams won more matches than away teams |
| 6 | Goals per Match Distribution | Most matches produced 2–4 goals |
| 7 | Average Goals by Round | Single-match rounds have less reliable averages |
| 8 | Top 10 Highest Scoring Matches | Occasional high-intensity encounters produced 5+ goals |
| 9 | Correlation Heatmap | SOT positively correlated with goals; possession pairs are inversely correlated |
| 10 | Goals Scored vs Wins | Strong positive correlation (scatter with trend line) |

---

## 5. KPI Analysis

Twelve+ Key Performance Indicators were computed directly from the dataset:

| KPI | Value |
|---|---|
| Total Matches | 104 |
| Total Goals | 308 |
| Average Goals per Match | 2.96 |
| Total Teams | 48 |
| Total Venues | 17 |
| Home Win % | 48.1% (50 matches) |
| Away Win % | 28.8% (30 matches) |
| Draw % | 23.1% (24 matches) |
| Highest Scoring Match | Computed dynamically in notebook |
| Top Scoring Team | Spain |
| Best Defense | Computed dynamically in notebook |
| Best Goal Difference | Spain (+13) |

*Note: Some values are generated dynamically from the dataset when the notebook is executed. The values shown above reflect the current dataset.*

A Plotly KPI Dashboard was created for visual presentation of these indicators.

---

## 6. Trend Analysis

### 6.1 Goals Over Time
- Total goals per matchday track the tournament schedule, peaking during group stage
- Average goals per match provides a fairer comparison across rounds

### 6.2 Match Results by Round
- Draws are most frequent in the group stage
- Knockout rounds produce more decisive results

### 6.3 Possession Trends
- Home teams tend to have slightly higher average possession
- This is consistent with the observed home advantage effect

### 6.4 Scoring Efficiency
- Goals per shot on target varies significantly between teams
- High efficiency can compensate for fewer total shots

---

## 7. Driver Analysis

### Methodology
Point-biserial correlations were computed between match statistics and home win outcome to identify which factors most strongly associate with winning.

### Key Findings

1. **Shots on Target** — Strongest positive driver of winning
2. **Possession** — Moderate positive association with home wins
3. **Fouls** — Weak or negative association (excessive fouling indicates pressure)
4. **Goal Difference vs Win %** — Strong positive correlation confirms GD as a robust performance metric

> **Important:** These are correlations, not causal relationships. Confounding factors (team quality, opponent strength) also play a role.

---

## 8. AI/ML Methodology

### 8.1 Problem Formulation
- **Task:** Multi-class classification
- **Target:** Match outcome — Win, Draw, or Loss (from home team perspective)
- **Features:** 22 match statistics (excluding scores to prevent data leakage)

### 8.2 Feature Engineering
Features used: possession (home/away), shots on target, total shots, saves, corners, crosses, interceptions, fouls, yellow cards, red cards, offsides.

### 8.3 Models Implemented

| Model | Description |
|---|---|
| Logistic Regression | Linear baseline classifier (multinomial, max_iter=1000) |
| Random Forest | Ensemble tree classifier (200 trees, max_depth=10) |

### 8.4 Data Split
- Training: 75% (stratified by target)
- Testing: 25%
- Random state: 42 (for reproducibility)

### 8.5 Feature Scaling
- StandardScaler applied for Logistic Regression
- Random Forest used on unscaled features (tree-based methods don't require scaling)

---

## 9. Model Evaluation

### Metrics Used
- Accuracy
- Precision, Recall, F1-Score (per class and weighted average)
- Confusion Matrix
- Feature Importance (Random Forest)

### Results
Both models were evaluated and compared. The detailed classification reports and confusion matrices are generated in the notebook.

### Feature Importance
The Random Forest feature importance analysis reveals which match statistics are most predictive of outcomes, providing actionable insight into what matters most during a match.

---

## 10. Key Findings

1. **Shots on Target** is the single most important predictor of match outcomes
2. **Home advantage** is a measurable factor — home teams won more frequently
3. **Goal Difference** is strongly correlated with win percentage, making it a robust performance metric
4. **Scoring efficiency** varies significantly between teams
5. **Match statistics contain predictive signal** for outcomes, as demonstrated by the ML models
6. **Knockout rounds** tend to produce different goal-scoring patterns compared to the group stage
7. **Possession dominance** has a moderate but not overwhelming association with winning

---

## 11. Risks

| # | Risk | Impact |
|---|---|---|
| 1 | Small dataset (104 matches) | Limits ML model generalization |
| 2 | Defensive vulnerability in some advancing teams | May be exposed in knockout rounds |
| 3 | Home advantage bias in data | May overweight home team perspective |
| 4 | No player-level data | Cannot assess individual contributions |
| 5 | Single tournament data | Findings may not generalize to other World Cups |

---

## 12. Opportunities

| # | Opportunity | Potential Impact |
|---|---|---|
| 1 | Shot efficiency training | Better conversion → more wins |
| 2 | Defensive improvement focus | Lower concession → better GD → better outcomes |
| 3 | Performance benchmarking | Teams can compare against leaders in specific metrics |
| 4 | Predictive analytics expansion | More data → better models → real-time predictions |
| 5 | Historical integration | Multi-tournament trends and evolution tracking |

---

## 13. Data-Driven Recommendations

### Recommendation 1: Prioritize Shot Quality Over Volume
- **Finding:** Shots on target is the strongest predictor of winning
- **Evidence:** Feature importance analysis and correlation statistics
- **Implication:** Quality chances matter more than total shot attempts
- **Action:** Focus training on creating and finishing high-quality shooting opportunities

### Recommendation 2: Account for Home Advantage
- **Finding:** Home teams won a disproportionate share of matches
- **Evidence:** Match result distribution analysis
- **Implication:** Home advantage is a real and measurable factor
- **Action:** Factor home/away context into performance evaluations and predictions

### Recommendation 3: Balance Attack and Defense
- **Finding:** Goal Difference is strongly correlated with win percentage
- **Evidence:** Scatter plot analysis and correlation statistics
- **Implication:** One-dimensional teams (attack-only or defense-only) are less successful
- **Action:** Invest in both attacking and defensive capabilities

### Recommendation 4: Expand Dataset for Better Predictions
- **Finding:** ML model performance is limited by dataset size
- **Evidence:** Model evaluation results
- **Implication:** More data would improve prediction accuracy and reliability
- **Action:** Incorporate historical World Cup data (1930–2022) for future analysis

### Recommendation 5: Prepare for Knockout Intensity
- **Finding:** Knockout rounds may produce different goal-scoring patterns
- **Evidence:** Round-wise goal analysis
- **Implication:** Higher-stakes matches require different tactical preparation
- **Action:** Invest in set-piece preparation and defensive organization for knockout rounds

---

## 14. Limitations

1. **Dataset size (104 matches)** limits statistical power and ML model generalization
2. **No player-level data** — analysis is restricted to match-level aggregates
3. **Single tournament** — findings are specific to the 2026 World Cup
4. **Correlation ≠ Causation** — statistical associations do not prove causal relationships
5. **In-match features used for ML** — this is a classification of observed statistics, not a pre-match prediction system
6. **No external factors** — weather, injuries, tactical changes during matches are not captured

---

## 15. Future Scope

1. **Historical Data Integration** — Combine with World Cup data from 1930–2022 for trend analysis
2. **Player-Level Analytics** — Incorporate individual player statistics for granular analysis
3. **Advanced ML Models** — Implement XGBoost, LightGBM, or deep learning models
4. **Real-Time Dashboard** — Build live match analytics with streaming data
5. **Expected Goals (xG)** — Add xG metrics for more sophisticated performance evaluation
6. **Cross-Validation** — Implement k-fold cross-validation for more robust model assessment
7. **Sentiment Analysis** — Incorporate social media sentiment data as external features

---

## 16. Conclusion

This project demonstrates a complete data analytics pipeline applied to FIFA World Cup 2026 data. Starting from raw match data, the analysis progresses through data cleaning, exploratory analysis, KPI computation, trend identification, driver analysis, and machine learning prediction.

The key contributions of this project are:
- A clean, well-structured analysis of 104 World Cup matches
- Identification of shots on target as the top predictor of match outcomes
- A machine learning model that demonstrates predictive capability
- Actionable, evidence-based recommendations for performance improvement
- A clear framework for extending the analysis with additional data

---

## 17. Technologies Used

| Technology | Version | Purpose |
|---|---|---|
| Python | 3.12 | Core programming language |
| Pandas | 2.x | Data manipulation |
| NumPy | 1.x | Numerical computation |
| Matplotlib | 3.x | Static visualization |
| Seaborn | 0.13 | Statistical visualization |
| Plotly | 6.x | Interactive visualization |
| Scikit-learn | 1.x | Machine learning |
| Streamlit | 1.x | Interactive dashboard |

---

## 18. References / Dataset Source

- **Dataset:** FIFA World Cup 2026 match data (publicly available)
- **Repository:** [https://github.com/anand-cm140/FIFA-World-Cup-2026-Data-Analysis](https://github.com/anand-cm140/FIFA-World-Cup-2026-Data-Analysis)
- **Scikit-learn Documentation:** [https://scikit-learn.org/](https://scikit-learn.org/)
- **Pandas Documentation:** [https://pandas.pydata.org/](https://pandas.pydata.org/)
- **Plotly Documentation:** [https://plotly.com/python/](https://plotly.com/python/)

---

*This report was prepared as part of the IBM SkillsBuild Data Analytics with AI Academic Internship Program conducted by BharatCares in association with AICTE.*
