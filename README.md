# MarketingCampaigns
The goal of this project is to compare the performance of the classifiers (k-nearest neighbors, logistic regression, decision trees, and support vector machines).

## Problem Definition
   The data is related with direct marketing campaigns of a Portuguese banking institution.
   The marketing campaigns were based on phone calls. Often, more than one contact to the same client was required,
   in order to access if the product (bank term deposit) would be (or not) subscribed.

   There are two datasets:
      1) bank-full.csv with all examples, ordered by date (from May 2008 to November 2010).
      2) bank.csv with 10% of the examples (4521), randomly selected from bank-full.csv.
   The smallest dataset is provided to test more computationally demanding machine learning algorithms (e.g. SVM).

   The classification goal is to predict if the client will subscribe a term deposit (variable y).

## Goal
   Using Supervised binary classification, predict whether a client will subscribe to a term deposit (y: yes/no) based on their demographic, financial, and marketing-interaction data.

## Data Understanding
   I started with bank.csv (smaller) for initial modeling, and bank-full.csv for final comparisons.

Examine the target variable’s distribution (class imbalance is common — usually ~10–12% “yes”).
Review categorical vs. numeric features.

### Visualize pairwise numeric interactions:
![Pairwise numeric interaction](/images/pairplot.png)


## Data Preparation

  Prepared the dataset for modeling:

  Encoded categorical variables: use OneHotEncoder.

  Scaled numeric features: using StandardScaler (important for KNN, SVM, Logistic Regression).

  Train-test split: 80–20 split.

  Handled class imbalance: considered class_weight='balanced' (for logistic regression and SVM).

## Modeling

I decided to use StratifiedKFold instead of KFold  - Since the target (y) is highly imbalanced (most clients didn’t subscribe),
StratifiedKFold is the right choice for all models inside GridSearchCV. We want a stable, unbiased estimate of model performance.

### Trained and compared these models:

  - K-Nearest Neighbors (KNN)
  - Logistic Regression
  - Decision Tree
  - Support Vector Machine (SVM)

## GridSearch Results
-------------------------------------------------------------------------------------------------------------------------------
| Model                   | Test ROC-AUC | Recall (Yes) | Precision (Yes) | Key Insight                                        |
| ----------------------- | ------------ | ------------ | --------------- | -------------------------------------------------- |
| **SVM**                 | **0.892**    | 0.74         | 0.41            | Best overall predictor of who will say “yes.”      |
| **Logistic Regression** | 0.890        | 0.76         | 0.39            | Nearly as strong, easier to interpret.             |
| Decision Tree           | 0.86         | 0.79         | 0.32            | More “generous”—finds most yeses but wastes calls. |
| KNN                     | 0.83         | 0.12         | 0.61            | Poor recall—misses most potential customers.       |
-------------------------------------------------------------------------------------------------------------------------------

## Summary
The machine-learning models demonstrate that the bank’s marketing campaigns are moderately predictable — about 90% AUC, meaning the model can distinguish likely subscribers from non-subscribers with high reliability.
Using these models (SVM or Logistic Regression), the bank could target only the top 40–50% of clients and still capture ≈75% of all potential depositors, reducing wasted calls by more than half.

Campaign success strongly depends on engagement quality (call duration), communication channel (cellular), and previous positive outcomes, suggesting that focusing on warm leads and modern channels can materially improve deposit uptake.
  
