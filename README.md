# ⚽ FIFA World Cup 2026 — AI-Powered Team Performance & Match Analytics

> An end-to-end Data Analytics + AI project analyzing FIFA World Cup 2026 match data — from exploratory analysis and KPI computation to machine learning-based match outcome prediction.

**Program:** IBM SkillsBuild Data Analytics with AI Academic Internship (BharatCares / AICTE)

---

## 📌 Project Overview

This project performs a comprehensive analysis of FIFA World Cup 2026 match data to uncover patterns in team performance, goal scoring trends, and match outcomes. It combines Exploratory Data Analysis (EDA) with machine learning to provide data-driven insights and predictions.

## 🎯 Problem Statement

> *How can match-level statistics (possession, shots, saves, fouls, etc.) be leveraged to understand team performance patterns, identify key drivers of match outcomes, and predict whether the home team will win, lose, or draw?*

## 📋 Objectives

1. **Data Quality** — Clean and preprocess raw match data for reliable analysis
2. **Exploratory Data Analysis** — Understand scoring patterns, team performance, and match distributions
3. **KPI Analysis** — Compute and present key performance indicators
4. **Trend Analysis** — Identify scoring trends across tournament rounds and dates
5. **Driver Analysis** — Determine which match statistics most strongly associate with winning
6. **AI/ML Prediction** — Build a machine learning model to predict match outcomes
7. **Insights & Recommendations** — Translate findings into actionable, data-driven recommendations

---

## 📊 Dataset

| Attribute | Details |
|---|---|
| **Source** | Publicly available FIFA World Cup 2026 match data |
| **File** | `data/matches.csv` |
| **Records** | 104 matches |
| **Columns** | 42 features |
| **Tournament Period** | June 11 – July 19, 2026 |
| **Teams** | 48 national teams |
| **Venues** | 17 stadiums across North America |

### Key Columns

| Column | Description |
|---|---|
| `round` | Tournament stage (Group stage, Round of 32, Round of 16, etc.) |
| `date` | Match date |
| `home_team` / `away_team` | Participating teams |
| `home_score` / `away_score` | Final score |
| `home_possession` / `away_possession` | Ball possession percentage |
| `home_sot` / `away_sot` | Shots on target |
| `home_total_shots` / `away_total_shots` | Total shots attempted |
| `home_saves` / `away_saves` | Goalkeeper saves |
| `home_corners` / `away_corners` | Corner kicks |
| `home_fouls` / `away_fouls` | Fouls committed |
| `home_cards_yellow` / `away_cards_yellow` | Yellow cards |
| `attendance` | Match attendance |
| `venue` | Stadium name |
| `referee` | Match referee |

> **Note:** The dataset reflects match outcomes as they occurred during the tournament. All analysis is based on the data as recorded.

---

## 🛠️ Technologies Used

| Technology | Purpose |
|---|---|
| Python 3.12 | Core programming language |
| Pandas | Data manipulation and analysis |
| NumPy | Numerical computation |
| Matplotlib | Static visualizations |
| Seaborn | Statistical visualizations |
| Plotly | Interactive visualizations |
| Scikit-learn | Machine learning (classification) |
| Streamlit | Interactive dashboard |

---

## 🔄 Project Workflow

```text
Data Collection → Data Cleaning → EDA → KPI Analysis → Trend Analysis
    → Driver Analysis → ML Prediction → Insights → Recommendations
```

### Detailed Workflow

1. **Data Loading & Inspection** — Load CSV, inspect schema, data types
2. **Data Quality Check** — Identify missing values, duplicates, inconsistencies
3. **Data Cleaning** — Handle penalty shoot-out scores, convert types, create derived columns
4. **Exploratory Data Analysis** — 10+ visualizations covering teams, goals, matches
5. **KPI Analysis** — 12+ tournament KPIs computed from data
6. **Trend Analysis** — Time-based trends, round-wise patterns, scoring efficiency
7. **Driver Analysis** — Correlation analysis, feature importance for winning
8. **ML Prediction** — Logistic Regression + Random Forest for match outcome prediction
9. **Model Evaluation** — Accuracy, F1-score, Confusion Matrix, Feature Importance
10. **Insights Generation** — Auto-generated insights from analysis
11. **Risks & Opportunities** — Data-driven risk/opportunity assessment
12. **Recommendations** — Finding → Evidence → Implication → Action format

---

## ✨ Key Features

- ✅ Complete data cleaning pipeline (handles penalty shoot-out edge cases)
- ✅ 12+ Key Performance Indicators with KPI Dashboard
- ✅ 10+ professional visualizations (Matplotlib, Seaborn, Plotly)
- ✅ Team performance table with all 48 teams
- ✅ Trend analysis across tournament rounds and dates
- ✅ Driver analysis (correlation + feature importance)
- ✅ Machine Learning match outcome prediction
- ✅ Model evaluation with Confusion Matrix and Feature Importance
- ✅ Auto-generated data-driven insights
- ✅ Risks & Opportunities analysis
- ✅ Data-driven recommendations (Finding → Action)
- ✅ Interactive Streamlit dashboard

---

## 🤖 Machine Learning

| Attribute | Details |
|---|---|
| **Target** | Match Outcome: Win / Draw / Loss (from home team perspective) |
| **Features** | 22 match statistics (possession, shots, saves, corners, crosses, etc.) |
| **Models** | Logistic Regression, Random Forest Classifier |
| **Split** | 75% train / 25% test (stratified) |
| **Evaluation** | Accuracy, Precision, Recall, F1-Score, Confusion Matrix |
| **Feature Importance** | Random Forest feature importance visualization |

### Data Leakage Prevention
- `home_score` and `away_score` are **excluded** from features since they directly determine the outcome.
- Only match statistics (which are observable during play) are used as features.

---

## 💡 Key Insights

> All insights are generated from the actual dataset — no fabricated findings.

- 📊 The tournament featured 104 matches across 17 venues with 48 teams
- ⚽ Shots on Target is the strongest predictor of match outcomes
- 🏠 Home teams had a measurable advantage in win percentage
- 📈 Goal Difference is strongly correlated with overall tournament success
- 🎯 Scoring efficiency (goals per shot on target) varies significantly between teams
- 🤖 ML models demonstrate that match statistics contain predictive signal for outcomes

---

## 🚀 How to Run

### Prerequisites
- Python 3.8+
- pip

### Setup

```bash
# Clone the repository
git clone https://github.com/anand-cm140/FIFA-World-Cup-2026-Data-Analysis.git
cd FIFA-World-Cup-2026-Data-Analysis

# Install dependencies
pip install -r requirements.txt

# Run the Jupyter Notebook
jupyter notebook FIFA_World_Cup_2026_Analysis.ipynb
```

### Run the Dashboard

```bash
streamlit run app.py
```

---

## 📁 Project Structure

```text
FIFA-World-Cup-2026-Data-Analysis/
│
├── data/
│   └── matches.csv                          # Dataset (104 matches × 42 columns)
│
├── images/
│   ├── wins.png                             # Top 10 Teams by Wins
│   ├── goals_scored.png                     # Top 10 Teams by Goals Scored
│   ├── goals_conceded.png                   # Top 10 Teams by Goals Conceded
│   ├── goal_difference.png                  # Top 10 Teams by Goal Difference
│   ├── match_results.png                    # Match Result Distribution
│   ├── goals_per_match_distribution.png     # Goals per Match Histogram
│   ├── avg_goals_by_round.png               # Average Goals by Round
│   ├── highest_scoring_matches.png          # Top 10 Highest Scoring Matches
│   ├── scatter_plot.png                     # Goals Scored vs Wins
│   ├── correlation_heatmap.png              # Correlation Heatmap
│   ├── goals_trend_daily.png                # Daily Goals Trend
│   ├── results_by_round.png                 # Results by Tournament Round
│   ├── driver_analysis.png                  # Driver Analysis Chart
│   ├── confusion_matrix.png                 # ML Confusion Matrix
│   └── feature_importance.png               # ML Feature Importance
│
├── FIFA_World_Cup_2026_Analysis.ipynb       # Main analysis notebook
├── app.py                                   # Streamlit dashboard
├── requirements.txt                         # Python dependencies
├── README.md                                # Project documentation
├── LICENSE                                  # MIT License
└── .gitignore                               # Git ignore rules
```

---

## 📊 Sample Visualizations

### Top Teams by Wins
![Wins](images/wins.png)

### Match Results Distribution
![Match Results](images/match_results.png)

### Goals Scored vs Matches Won
![Scatter](images/scatter_plot.png)

---

## ⚠️ Limitations

1. **Dataset Size** — 104 matches is relatively small for ML, limiting model generalization
2. **No Player-Level Data** — Analysis is restricted to match-level aggregates
3. **Single Tournament** — Findings are specific to the 2026 World Cup and may not generalize
4. **Correlation ≠ Causation** — Statistical associations do not imply causal relationships
5. **In-Match Features** — ML uses in-match statistics, not pre-match prediction

---

## 🔮 Future Improvements

1. Incorporate historical World Cup data (1930–2022) for time-series analysis
2. Add player-level statistics for more granular performance analysis
3. Implement advanced ML models (XGBoost, Neural Networks) with larger datasets
4. Build real-time dashboards for live match analytics
5. Add expected goals (xG) data for sophisticated attacking performance evaluation
6. Implement cross-validation for more robust model evaluation

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<p align="center">
  <b>FIFA World Cup 2026 — AI-Powered Team Performance & Match Analytics</b><br>
  IBM SkillsBuild Data Analytics with AI Academic Internship (BharatCares / AICTE)
</p>
