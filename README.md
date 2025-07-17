## Aave Wallet Credit Scoring System
This project estimates creditworthiness scores (ranging from 0 to 1000) for Ethereum wallet addresses based on their transaction behaviors within the Aave protocol. It utilizes feature engineering, semi-supervised learning, and XGBoost modeling to classify wallets as reliable or risky and assign scores accordingly.

# Project Overview
The system analyzes on-chain transactional data from Aave (in JSON format) and outputs a credit score per wallet address. The scores can be used to:

Understand risk levels of wallets

Detect anomalous or bot-like behaviors

Improve lending protocols or fraud detection systems

# Methodology
# 1. Feature Engineering
Transaction data is first parsed and transformed into meaningful behavioral features:

Transaction count

Average and total transferred amount

Unique action types

Wallet activity duration

Activity rate (transactions per day)

Bursty behavior flag: a heuristic to detect highly active accounts

These features are used as the foundation for training the credit scoring model.

# Bursty Behavior Logic
A wallet is flagged as bursty (bot-like) if its average activity rate exceeds 10 transactions/day.

# 2. Semi-Supervised Modeling (XGBoost)
We simulate labeled data based on bursty behavior:

Bursty wallets are labeled as 0 (risky)

Others are labeled as 1 (safe)

A binary classifier (XGBoost) is trained using these weak labels. The predicted probabilities for being "safe" are scaled to a 0–1000 credit score.

📊 3. Visualization
A distribution plot of credit scores is generated to visually inspect the wallet classification landscape.

# System Architecture

[JSON File]
    |
    v
[Feature Engineering]
    |
    v
[Heuristic Labeling (bursty logic)]
    |
    v
[XGBoost Model Training]
    |
    v
[Score Generation (0–1000)]
    |
    v
[Score Distribution Plot + CSV Output]
# Processing Flow

Input: Load JSON data of Aave transactions.

Data Transformation: Convert timestamps, parse amounts, and group transactions by wallet address.

Feature Engineering: Generate numerical features summarizing wallet behavior.

Label Simulation: Use bursty logic to label wallets as safe or risky.

Model Training: Fit an XGBoost classifier on the features and simulated labels.

Scoring: Use prediction probability to compute credit scores.

Output:

A csv format with wallet addresses and scores.

A barplot showing distribution of credit scores.

# Requirements
Python 3.8+
Libraries:
pandas
numpy
xgboost
matplotlib
seaborn
scikit-learn

