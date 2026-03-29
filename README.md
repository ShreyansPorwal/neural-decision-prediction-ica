# Neural Decision Prediction using ICA vs PCA

## Overview

This project builds a machine learning model to predict decision outcomes (success vs failure) from neural spike data recorded during a visual decision-making task in mice.

Using the Steinmetz et al. (2019) dataset, the goal was to understand how neuronal activity relates to behavioral responses and to evaluate appropriate dimensionality reduction techniques for modeling.

---

## Key Contributions

* Built a classification pipeline to predict decision outcomes from neural spike activity
* Performed extensive exploratory data analysis (EDA) on neuronal and stimulus features
* Compared **PCA vs ICA** based on statistical assumptions (linearity and normality)
* Identified **non-normal feature distributions**, motivating the use of ICA over PCA
* Implemented logistic regression models with performance evaluation across multiple sessions and subjects

---

## Dataset

* Source: Steinmetz et al. (2019) neuroscience dataset
* 18 experimental sessions across multiple mice
* Features include:

  * Left/right visual contrast
  * Brain regions
  * Neural spike counts
  * Trial timing
* Target:

  * `feedback_type` → Success (1) vs Failure (-1)

---

## Methodology

### 1. Data Processing

* Combined session-level `.rds` files into a unified dataset
* Aggregated spike activity by brain region and trial
* Engineered features such as contrast difference and regional spike statistics

### 2. Exploratory Data Analysis

* Analyzed stimulus distributions and class imbalance
* Investigated spike activity across brain regions and sessions
* Identified heterogeneity in neuronal behavior across subjects

### 3. PCA vs ICA Analysis

* Conducted:

  * **Shapiro-Wilk & Anderson-Darling tests** → non-normality detected
  * **Q-Q plots & histograms** → right-skewed distributions
  * **Pearson vs Spearman correlations** → mild non-linearity

Conclusion:

> Data violated normality assumptions → **ICA preferred over PCA**

---

## Modeling

### Model: Logistic Regression

* Separate models trained per mouse
* Features:

  * Contrast levels
  * Spike-based features
  * Brain region encodings
* Addressed class imbalance using oversampling

### Evaluation Metrics

* Accuracy
* Sensitivity (recall for failure class)
* Specificity
* AUC

---

## Results

* Accuracy: ~60–68%
* AUC: ~0.60–0.64
* High specificity (good at predicting success)
* Lower sensitivity due to class imbalance
* Consistent performance across training and test sets → minimal overfitting

---

## Key Insights

* Neural spike activity varies significantly across brain regions and subjects
* Higher spike activity is often associated with correct decisions
* Dataset exhibits strong heterogeneity → careful aggregation required
* Statistical assumption checks are critical when choosing dimensionality reduction methods

---

## Tech Stack

* R
* tidyverse, ggplot2
* caret, glmnet
* pROC
* fastICA

---

## Future Improvements

* Complete ICA-based modeling pipeline
* Explore more advanced models (Random Forest, Gradient Boosting)
* Improve class imbalance handling (SMOTE, class weighting)
* Cross-subject generalization modeling

---

## References

Steinmetz, N.A., Zatka-Haas, P., Carandini, M. et al.
*Distributed coding of choice, action and engagement across the mouse brain.*
Nature 576, 266–273 (2019)
