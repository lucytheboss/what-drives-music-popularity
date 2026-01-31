# Behavioral Discovery Analysis of Music Popularity
### Understanding Why Some Songs Overperform or Underperform Expectations

---

## 1. Objective

Most popularity analyses focus on predicting success from artist reputation or historical trends.

However, prediction alone does not explain **why certain songs unexpectedly succeed or fail**.

This project investigates:

> **When popularity predictions are wrong, what behavioral or market factors explain the gap?**

To answer this, we:
1. Explore the dataset through EDA
2. Build a baseline popularity model
3. Analyze residuals to uncover discovery gaps and exposure biases

---

# 2. Exploratory Data Analysis (EDA)

## 2.1 Popularity Distribution
![Track Popularity Distribution](../images/eda/fig01_track_popularity_distribution.png)


Track popularity is broadly centered around mid-range values with long tails.

- Most songs cluster between 30–70
- Extreme hits and extreme failures are relatively rare

This suggests:
- popularity is noisy
- deterministic prediction is unlikely
- behavioral or contextual effects may play a strong role

---

## 2.2 Artist Strength vs Track Success
![Artist vs Track Popularity](../images/eda/fig03_artist_vs_track_popularity_regression.png)

Initial exploration shows:

- more popular artists tend to have higher-performing tracks
- follower count correlates with visibility
- recent success (momentum) carries forward

This confirms the presence of **cumulative advantage effects**:

> “successful artists become more successful”

However, large variability remains even within the same artist,
indicating that artist strength alone cannot fully explain outcomes.

---

## 2.3 Audio Feature Patterns
![Audio Feature Correlation Heatmap](../images/eda/fig07_audio_feature_correlation_heatmap.png)

Audio features (tempo, energy, brightness, rhythm strength) show:

- moderate correlations with popularity
- no single dominant predictor

This suggests:
- musical characteristics contribute partially
- but platform exposure and behavioral dynamics likely matter more

---

# 3. Baseline Modeling

## 3.1 Model Design

We trained a linear regression model to estimate **expected popularity** using:

- artist popularity
- follower count
- previous release performance
- historical average momentum
- track duration

These variables represent structural or historical signals available prior to release.

---

## 3.2 Training Setup & Evaluation Protocol
To ensure realistic evaluation and avoid information leakage, model training follows a strict separation between historical and future data.

**Data split**

- Train: 80% earlier releases (5,479 tracks (earlier releases))
- Test: 20% later releases (1,370 tracks (later releases, holdout))

This mimics a real-world scenario where popularity must be estimated **before a new track’s performance is observed**.

**Procedure**

- Features computed using only pre-release information
- Linear Regression (OLS) used as the baseline model
- Model fit on training data only
- Final metrics reported on the held-out test set

This prevents overfitting and ensures that performance reflects true predictive ability.

---

## 3.3 Model Fit
![Model Fit](../images/discovery/fig14_actual_vs_predicted.png)

The model captures general trends:

- strong artists tend to perform well
- momentum predicts continued success

However:

- significant residual variance remains
- many tracks deviate substantially from predictions

Conclusion:

> Popularity is only partially explained by reputation and history.

This motivates analyzing **prediction errors** rather than predictions alone.

---

## 3.4 Model Performance Metrics

We evaluate multiple model configurations on the held-out test set (n = 1,370).

| Model | Features | R² | MAE |
|--------|----------------------------|-------|-------|
| Audio only | audio features | 0.003 | 14.17 |
| Artist only | popularity + followers | 0.104 | 13.34 |
| Artist + momentum | history + prior releases | 0.198 | 12.07 |

**Key observations**

- Audio features alone explain virtually none of the variance
- Artist reputation explains ~10%
- Adding momentum improves prediction modestly
- Even the best model explains only ~20% of outcomes

**Interpretation**

Over **80% of popularity variance remains unexplained** by structural or historical signals.

This motivates analyzing **prediction errors (residuals)** rather than predictions alone.

---

## 3.5 Feature Contributions
To understand which factors drive expected popularity, we examine model coefficients and feature importance.

**Most influential predictors*

- Artist popularity
- Follower count
- Prior release momentum

**Secondary predictors**

- Track duration
- Audio characteristics (energy, brightness, rhythm strength)

Audio features show only moderate effects relative to historical reputation signals.

**Interpretation**

- Baseline popularity is primarily explained by exposure and reputation, while intrinsic musical characteristics play a smaller role.
- This supports the hypothesis that discovery mechanics, not only content quality, shape outcomes.

---

# 4. Residual-Based Discovery Analysis

## 4.1 Residual Definition
![Residual Distribution](../images/discovery/fig15_residual_distribution.png)

We compute: $residual = actual - predicted$


Interpretation:

- positive → surprise hit
- negative → underrated track

Residuals isolate behavioral or exposure-driven effects not captured by the model.

---

## 4.2 Residual Segmentation Method
Tracks are categorized using the distribution of prediction residuals:
$$residual=actual−predicted$$

We define segments using percentile thresholds:
- **Surprise Hits**: top 10% residuals
- **Expected**: middle 80%
- **Underrated**: bottom 10%

This approach isolates tracks that significantly overperform or underperform relative to expectation while remaining robust to noise.

Approximately **20% of tracks fall outside expected performance**, indicating systematic rather than purely random deviations.

---

## 4.3 Segmenting Tracks

Tracks are grouped into:

- Surprise Hits
- Expected
- Underrated

Approximately **20% of tracks fall outside expectations**.

This indicates substantial discovery opportunities rather than random noise.

---

# 5. Findings

## 5.1 Underrated Tracks
![Underrated Genre Bias](../images/discovery/fig18_underrated_genre_bias.png)

Underrated songs show:

- similar artist popularity
- similar followers
- similar momentum
- similar duration

Yet they perform significantly worse.

Key difference:

### Genre concentration

Underrated tracks over-index in:

- Classical
- Children’s
- Country
- Metal
- other niche genres

Interpretation:

> These tracks are not weaker — they are underexposed.

This suggests potential **discovery blind spots** in recommendation systems.

---

## 5.2 Surprise Hits
![Surprise Hit Genre Bias](../images/discovery/fig19_surprise_genre_bias.png)

Surprise hits show:

- average or slightly weaker artist history
- lower momentum than expected
- but strong overperformance

Key difference:

### Mainstream genre amplification

Overrepresented genres include:

- Pop
- Rock
- R&B

Interpretation:

> Mainstream genres receive disproportionate visibility or amplification.

---

# 6. Interpretation

Together, these patterns suggest:

Popularity is not purely merit-based.

Instead, success is shaped by:

- historical reputation
- platform exposure
- recommendation mechanics
- genre biases

Discovery systems appear to:

- amplify already mainstream content
- under-serve niche genres

This creates structural inequalities in visibility.

---

# 7. Product & UX Implications

These insights can inform:

- hidden gem surfacing features
- fair exposure ranking
- playlist diversification
- marketing prioritization
- improved cold-start handling
- more equitable discovery systems

Residual-based analysis provides a practical way to detect where recommendation systems may be missing value.

---

## 7.1 Product & System Opportunities
Residual analysis provides actionable signals for improving discovery systems.

**Potential applications**
- Re-rank recommendations using residual-adjusted scores
- Surface high-quality but underexposed “hidden gem” tracks
- Reduce popularity bias by boosting niche genres
- Diversify playlists to improve long-tail engagement
- Detect systematic exposure inequalities across categories
- Improve cold-start handling for new or smaller artists


These interventions can increase:
- catalog utilization
- fairness of exposure
- listener discovery
- overall engagement

Residuals therefore serve as a practical diagnostic tool for identifying **where recommendation systems leave value untapped**.

---

# 8. Limitations
Several constraints should be considered when interpreting results:

- Popularity scores are imperfect proxies for true listener preference
- Exposure data (playlist placement, recommendation impressions) is not directly observed
- Linear modeling assumes additive relationships and may miss nonlinear effects
- Findings are correlational and do not establish causality


Future work could incorporate:

- recommendation logs or exposure metrics
- nonlinear or ensemble models
- causal inference methods (A/B testing or quasi-experimental designs)

Despite these limitations, residual-based analysis remains a useful framework for identifying discovery inefficiencies.

---
# 9. Conclusion

Prediction explains part of popularity, but not all.

By focusing on **when predictions fail**, we uncover:

- overlooked opportunities
- unexpected successes
- systemic exposure effects

This behavioral perspective enables more effective and more equitable music discovery experiences.

---

## Repository Links

Notebooks:  
`/notebooks`

Slides:  
`reports/slides.pdf`

Project README:  
`../README.md`

Dashboard: Tableau (link)  