# BBS Customer & Marketing Analytics
## Team Assignment 1 — 2026
### What Makes an Influencer Post Work?

**Team members:** Giulia Lorelli, Francesco Gambera, Romain Derguini, Israa Ismail, Iolanda Costa

---

## Overview

This project analyses a dataset of 600 influencer posts on behalf of **Pulse Digital**, a fictional influencer marketing agency. The goal is to identify which post characteristics — caption content, sentiment, platform, influencer profile — drive three key performance outcomes: engagement, click-through, and comments.

The analysis is conducted entirely in Python using a Jupyter Notebook, progressing through four research questions (Q0–Q4).

---

## Dataset

**File:** `Team_Assignment_1_Data_2026.csv` (semicolon-delimited)

**Key variables:**

| Variable | Type | Description |
|---|---|---|
| `Engagement_Rate` | Continuous (%) | % of audience that engaged with the post |
| `Click_Through` | Binary (0/1) | Whether the post drove traffic to the brand site |
| `Comment_Count` | Count (integer ≥ 0) | Number of comments on the post |
| `Caption_Sentiment` | Continuous | Sentiment score of the caption |
| `ZCaption_Length` | Continuous (standardised) | Standardised caption length |
| `Topic_*_Positive/Negative` | Binary | LDA-derived topic presence flags |
| `Platform` | Categorical | Instagram or TikTok |
| `Post_Type` | Categorical | Video or Image |
| `Product_Category` | Categorical (3 levels) | Beauty & Skincare, Fashion & Apparel, Tech & Gadgets |
| `Influencer_Tier` | Categorical | Nano / Micro / Macro / Mega |
| `Follower_Count_K` | Continuous | Follower count in thousands |
| `Influencer_Age` | Continuous | Age of the influencer |

---

## Project Structure

```
├── BBS_CMA_Team_Assignment2__1_.ipynb   # notebook by GL+ II (latest version)
├── BBS_CMA_Team_Assignment1.ipynb       # Orginal Work by GL/Earlier draft
├── Team_Assignment_1_Data_2026.csv      # Dataset 
```

---

## Analysis

### Q0 — Data Preparation
- Missing value check and descriptive statistics
- Dummy coding for `Product_Category` (reference: Beauty & Skincare)
- Standardisation of `Caption_Length` → `ZCaption_Length`
- Distribution plots for all three dependent variables
- Multicollinearity check via VIF (all values < 5)

### Q1 — Engagement Rate (OLS Linear Regression)
- Dependent variable: `Engagement_Rate` (continuous)
- Model: Ordinary Least Squares
- Outputs: regression summary, coefficient plot (significant predictors highlighted)

### Q2 — Click-Through (Logistic Regression)
- Dependent variable: `Click_Through` (binary)
- Model: Logit
- Outputs: log-odds coefficients, marginal effects, coefficient plot

### Q3 — Comment Count (Count Regression)
- Dependent variable: `Comment_Count` (non-negative integer)
- Model selection: Poisson vs Negative Binomial based on overdispersion test (var/mean ratio)
- Overdispersion confirmed → Negative Binomial used
- Outputs: regression summary, coefficient plot

### Q4 — Interaction Effects
- Base model: Q1 (Engagement Rate — OLS)
- Interaction 1: `Topic_CTA_Positive × Platform` — Does a positive CTA work differently on Instagram vs TikTok?
- Interaction 2: `Post_Type × Caption_Sentiment` — Does sentiment matter more for videos or images?
- Model comparison: baseline vs interaction model (R², Adjusted R², AIC)
- Output: interaction plot (CTA × Platform)

---

## Dependencies

```bash
pip install pandas numpy matplotlib seaborn statsmodels scipy
```

The notebook is designed to run on **Google Colab**. Data is loaded via `google.colab.files.upload()`.

---

## How to Run

1. Open `BBS_CMA_Team_Assignment2__1_.ipynb` in Google Colab
2. Run the setup cell to install dependencies
3. When prompted, upload `Team_Assignment_1_Data_2026.csv`
4. Run all cells in order (Cell → Run All)

---

## Notes

- Use `BBS_CMA_Team_Assignment2__1_.ipynb` — including VIF checks, richer markdown commentary, interaction analysis
- `BBS_CMA_Team_Assignment1.ipynb` is an earlier draft kept for reference
- Marketing implications sections in Q2, Q3, and the Executive Summary are placeholders to be completed before final submission