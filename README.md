[![Open In Colab](https://github.com/HaoshuiYu/logreg-volatility-pipeline/blob/main/log_reg_vol.ipynb)
## Logistic Regression Volatility Signal
This project implements a logistic regression model to estimate the probability of a positive forward return using return- and volatility-based features. The emphasis is on building a clean end-to-end modeling pipeline and evaluating probabilistic outputs rather than maximizing raw prediction accuracy. At this stage, the pipeline uses ASML (semiconductor company) as the target asset, with SMH used as the semiconductor sector average proxy; these inputs can be replaced to apply the method to other assets/sectors.

## Objective
The goal of this project is to practice constructing and validating a classification model for financial time series data, with particular focus on probability ranking and calibration behavior.

## Overview
The repository contains a single Jupyter notebook that walks through the full modeling process, including data preparation, feature engineering, model fitting, and evaluation.

## Pipeline Stages
The notebook follows these high-level stages:
- Data acquisition and preparation
- Feature engineering
- Label construction
- Model fitting and selection
- Evaluation and sanity checks

## Evaluation
Model performance is assessed using:
- Log loss to measure probabilistic accuracy  
- Rank-based diagnostics to evaluate ordering quality  
- Calibration buckets to compare predicted probabilities against realized outcomes  

The evaluation is intended to understand the reliability and structure of the model’s probability outputs rather than to demonstrate trading profitability.

## Notes and Limitations
- This project is exploratory and intended for learning purposes  
- The feature set is intentionally simple  
- Transaction costs, execution effects, and position sizing are not modeled  

## Future Work
- Expansion of the feature set  
- Comparison with alternative classifiers  
- Regime-aware evaluation and robustness checks  

## Findings
On the test set, the logistic regression model performs slightly better than a simple base-rate baseline. For example, test log loss improves from 0.6019 (baseline) to 0.5828 (model), and the Brier score improves from 0.2057 (baseline) to 0.1975 (model). This suggests the features provide some signal, but the improvement is modest.

The probability ranking looks reasonable: when predictions are split into 10 buckets, the average predicted probability increases bucket-by-bucket (“Rank check: PASS”). However, calibration is still imperfect (mean absolute calibration error ≈ 0.0677), and some buckets show noticeable gaps between predicted probability and realized hit rate.

As a sanity check, when the labels are shuffled, the model no longer beats the baseline on the test set, which is consistent with the idea that any real signal is small but not purely random noise.


For these reasons, the signal exists but is only weakly predictive of prices when applied to the equity asset ASML.

