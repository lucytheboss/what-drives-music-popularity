# 🎧 What Drives Music Popularity?
### Behavioral Discovery & Underrated Track Analysis

Most popularity models ask:
> *“What predicts success?”*

This project asks a more practical question:
> **“When predictions fail, why?”**

We first model expected popularity using artist reputation and historical momentum.
Then we analyze **residuals (actual − predicted)** to uncover behavioral and exposure-driven effects that traditional models miss.

This approach reveals:
- hidden gems (underrated tracks)
- surprise hits
- genre-level discovery bias
- systemic exposure inequalities in recommendation systems

---

## 🚀 Key Insights

- Momentum explains baseline trends but not outcomes
- ~20% of tracks behave unexpectedly
- Niche genres are disproportionately underrated
- Mainstream genres are disproportionately amplified
- Popularity is influenced by platform discovery mechanics, not just artist merit

---

## 📊 Visual Highlights

### Popularity Distribution
![Popularity](assets/figures/discovery/fig13_popularity_distribution.png)

### Model Fit (Actual vs Predicted)
![Model Fit](assets/figures/discovery/fig14_actual_vs_predicted.png)

### Residual Distribution
![Residuals](assets/figures/discovery/fig15_residual_distribution.png)

### Underrated Genre Bias
![Underrated](assets/figures/discovery/fig18_underrated_genre_bias.png)

### Surprise Hit Genre Bias
![Surprise](assets/figures/discovery/fig19_surprise_genre_bias.png)

---

## 🧠 Method Overview

### Step 1 — Baseline Model
Predict expected popularity using:
- artist popularity
- follower count
- prior release performance (momentum)
- historical averages
- track duration

### Step 2 — Residual Analysis
Compute:
$residual = actual - predicted$

Residuals capture unexplained performance:
- positive → surprise hits
- negative → underrated tracks

### Step 3 — Segment & Diagnose
We profile these segments to uncover:
- genre patterns
- exposure gaps
- behavioral effects

---

## 📂 Repository Structure

```
data/
    raw/
    processed/
notebooks/
    01_data_audit.ipynb
    02_audio_features_librosa.ipynb
    03_build_base_aligned.ipynb
    04_exploratory_data_analysis.ipynb
    05_audio_modeling.ipynb
    06_discovery_and_underrated_track.ipynb
images/
    final presentation figures
reports/
    analysis_report.md
    analysis_report.pdf
```


---

## 📄 Detailed Report
👉 See full analysis write-up:
**reports/analysis_report.md**

---

## 🛠 Tech Stack
- Python
- Pandas
- scikit-learn
- Librosa
- Matplotlib / Seaborn
- Tableau (dashboard)

---

## 🎯 Why This Matters

Most recommendation systems optimize for predicted popularity.

But residual analysis reveals:
- overlooked content
- hidden opportunities
- systemic exposure bias

This behavioral perspective helps design:
- fairer ranking systems
- better discovery
- more diverse playlists
- improved user experience

---

## 👤 Author
Lucy Roh  
Behavioral Data Analytics • UX Research • Music Intelligence