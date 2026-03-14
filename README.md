# 🎵 Spotify Track Popularity Analysis

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-2.0-150458?style=flat&logo=pandas)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-1.3-F7931E?style=flat&logo=scikit-learn)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)

> An end-to-end data analysis and machine learning project to discover **what makes a Spotify song popular** — using 114,000 real tracks from Kaggle.

---

## 📌 Table of Contents
- [Overview](#overview)
- [Dataset](#dataset)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Phase 1 — Data Cleaning](#phase-1--data-cleaning)
- [Phase 2 — EDA & Visualization](#phase-2--eda--visualization)
- [Phase 3 — Statistical Insights](#phase-3--statistical-insights)
- [Phase 4 — Machine Learning](#phase-4--machine-learning)
- [Key Findings](#key-findings)
- [Tech Stack](#tech-stack)

---

## Overview

This project analyzes 114,000 Spotify tracks to answer:
- Which audio features drive song popularity?
- Do explicit songs perform better than non-explicit ones?
- Can we predict whether a song will be popular based on its audio features?

---

## Dataset

- **Source:** [Kaggle — Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
- **Size:** 114,000 tracks × 20 features
- **Features include:** `danceability`, `energy`, `loudness`, `valence`, `tempo`, `acousticness`, `instrumentalness`, `speechiness`, `popularity`, `track_genre`, and more

---

## Project Structure

```
spotify-popularity-analysis/
│
├── dataset.csv                  # Raw dataset from Kaggle
├── spotify_analysis.ipynb       # Main analysis notebook
└── README.md                    # Project documentation
```

---

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/spotify-popularity-analysis.git
cd spotify-popularity-analysis

# Install dependencies
pip install numpy pandas matplotlib seaborn scikit-learn scipy
```

Then open `spotify_analysis.ipynb` in Jupyter or VS Code.

---

## Phase 1 — Data Cleaning

- Removed 3 rows with missing values
- Dropped duplicate `track_id` entries
- Filtered outliers: removed songs over 10 minutes and tracks with `tempo = 0`
- Engineered new feature: `duration_sec` from milliseconds
- Converted `explicit` boolean to integer for ML compatibility

**Final clean dataset: 89,035 tracks**

---

## Phase 2 — EDA & Visualization

- Popularity distribution is **right-skewed** — most songs cluster near 0
- Analyzed top 10 genres by average popularity
- Built a correlation heatmap across all audio features
- Scatter plot of Energy vs Danceability colored by Popularity
- Boxplot comparing Explicit vs Non-Explicit track popularity

---

## Phase 3 — Statistical Insights

### Genre Insights

| Metric | Genre |
|---|---|
| Most Popular | **K-pop** |
| Most Danceable | **Kids** |
| Most Energetic | **Death-metal** |
| Happiest (Valence) | **Salsa** |

### Feature Correlations with Popularity

| Feature | Relationship |
|---|---|
| `loudness` | ✅ Strongest positive correlation |
| `instrumentalness` | ❌ Strongest negative correlation |

### Hypothesis Test — Explicit vs Non-Explicit

Used an **independent samples T-test** to test whether explicit songs are significantly more popular.

| Group | Avg Popularity |
|---|---|
| Explicit | 36.92 |
| Non-Explicit | 32.90 |

- **T-statistic:** 16.35
- **P-value:** < 0.0001
- ✅ **Result:** Statistically significant — explicit songs are measurably more popular

---

## Phase 4 — Machine Learning

### Goal
Binary classification: predict whether a track is **popular** (popularity ≥ 50) or not.

### Model
**Random Forest Classifier** with `class_weight='balanced'` to handle class imbalance (76% not popular / 24% popular).

### Features Used
`danceability`, `energy`, `loudness`, `speechiness`, `acousticness`,
`instrumentalness`, `liveness`, `valence`, `tempo`, `duration_sec`, `explicit`

### Results

| Metric | Score |
|---|---|
| ROC-AUC | **0.7093** |
| Train/Test Split | 80% / 20% |

### Top 3 Predictive Features
1. `duration_sec` — song length is the strongest predictor
2. `valence` — emotional positivity influences popularity
3. `loudness` — louder masters tend to perform better

> 💡 **Interesting finding:** Despite being statistically significant in Phase 3, `explicit` was the **least important** feature in the Random Forest — demonstrating that statistical significance ≠ predictive power.

---

## Key Findings

1. **Loudness correlates most with popularity** — radio-ready masters sound louder
2. **Instrumental tracks are least popular** — vocals drive streams
3. **Explicit songs are statistically more popular** (p < 0.0001), but audio features are weak overall predictors
4. **K-pop dominates popularity** — driven by massive, coordinated global fanbases
5. **ROC-AUC of 0.71** — respectable given that popularity depends heavily on non-audio factors like marketing, artist fame, and timing
6. **Audio features alone have limited predictive power** — suggesting external factors (playlisting, social media, artist fanbase) matter more than the sound itself

---

## Tech Stack

| Tool | Purpose |
|---|---|
| `NumPy` | Numerical operations & array manipulation |
| `Pandas` | Data loading, cleaning & transformation |
| `Matplotlib` | Custom visualizations & plots |
| `Seaborn` | Statistical visualizations & heatmaps |
| `Scikit-learn` | Machine learning model & evaluation |
| `SciPy` | Hypothesis testing (T-test) |

---

## Author

Made by **AMAN KUMAR DAYAL**
📧 amandayal91@gmail.com
🔗 [LinkedIn](www.linkedin.com/in/aman-kumar-dayal-545baa319) | [GitHub](https://github.com/amandayal3)

---

*Dataset sourced from Kaggle. Project built for educational and portfolio purposes.*
