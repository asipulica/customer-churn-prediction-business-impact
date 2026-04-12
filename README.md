
## What the Notebook Does
This notebook builds a customer churn prediction model on a Netflix customer dataset (5,000 customers, 14 features) to identify which subscribers are likely to cancel their subscription.

## Dataset Overview
The data is nearly perfectly balanced — 2,515 churned customers (50.3%) vs. 2,485 who stayed (49.7%) — which is ideal for classification, as it avoids the need for resampling techniques.
Key features include age, watch hours, days since last login, subscription type (Basic/Standard/Premium), region, device, payment method, number of profiles, and average watch time per day.

## Key Finding: What Drives Churn
The most telling result is the behavioural difference between churned and retained customers (Cell 48):

odel Results
Two models were trained:
1. Logistic Regression

Accuracy: 83.1%
Precision: 85.1% | Recall: 83.1% | F1: 82.9%
Confusion matrix: correctly identified 710 churners, but missed 37 and falsely flagged 216 retained customers

A reasonable baseline, but the 216 false positives (predicting churn when the customer stayed) are a notable weakness.
2. Random Forest (200 trees)

Confusion matrix at default threshold: 729 true negatives, 740 true positives, only 17 false positives and 14 false negatives
This is a dramatic improvement over Logistic Regression

Threshold Optimisation
The notebook then searches for the best classification threshold by maximising F1 score across all probability cut-offs (0 to 1). The best result:

Optimal threshold: 0.51
F1 score: 0.980 (98.0%)
At this threshold: 732 true negatives, 738 true positives, only 14 false positives, 16 false negatives

This means the Random Forest, tuned to a 0.51 threshold, correctly classifies 98% of customers, with very few errors in either direction.

Summary for Report
The Random Forest model significantly outperforms Logistic Regression for predicting Netflix customer churn. The analysis reveals that engagement metrics — particularly watch hours and days since last login — are the strongest predictors of churn, far more so than subscription price. Customers who churn watch approximately 66% fewer hours and log in half as frequently as those who stay. The optimised model achieves a 98% F1 score, making it highly reliable for identifying at-risk customers before they cancel.
