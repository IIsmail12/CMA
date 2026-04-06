# BBS Customer & Marketing Analytics
## Team Assignment 1 — 2026
### What Makes an Influencer Post Work?


---
 
## Team & Contributions
 
| Team Member | Role |
|---|---|
| Giulia Lorelli | Code & Analysis |
| Israa Ismail | Code & Analysis |
| Francesco Gambera | Code & Analysis |
| Iolanda Costa | Analysis, Interpretation, Slides & Presentation |
| Romain Derguini | Analysis, Interpretation, Slides & Presentation |
 
---
 
## Overview
 
This project analyses a dataset of 600 influencer posts on behalf of **Pulse Digital**, a digital influencer marketing agency. The goal is to identify which post characteristics — caption content, sentiment, platform, and influencer profile — drive three key performance outcomes: engagement, click-through, and comment volume.
 
The analysis is conducted entirely in Python using a Jupyter Notebook, progressing through four research questions (Q0–Q4).
 
---
 
## Dataset
 
**File:** `Team_Assignment_1_Data_2026.csv`  
**Source:** Provided by BBS / Dr. Umut Konuş (2026)
 
| Variable | Type | Description |
|---|---|---|
| `Engagement_Rate` | Continuous (%) | % of audience that engaged with the post |
| `Click_Through` | Binary (0/1) | Whether the post drove traffic to the brand site |
| `Comment_Count` | Count (integer ≥ 0) | Number of comments on the post |
| `Caption_Sentiment` | Ordinal 1–5 | NLP sentiment score of the caption |
| `ZCaption_Length` | Continuous | Standardised caption length (z-score) |
| `Topic_*_Positive/Negative` | Binary | Zero-shot classification topic flags |
| `Platform` | Binary | 0=Instagram, 1=TikTok |
| `Post_Type` | Binary | 0=Static Photo, 1=Short Video/Reel |
| `Product_Category` | Nominal (3 levels) | 0=Beauty & Skincare, 1=Fashion, 2=Tech |
| `Influencer_Tier` | Binary | 0=Micro (≤50k), 1=Macro (>50k) |
| `Follower_Count_K` | Continuous | Follower count in thousands |
| `Influencer_Age` | Continuous | Age of the influencer |
 
---
 
## Project Structure
 
```
├── BBS_CMA_Team_Assignment1_V1.2.ipynb  # Final version by Francesco (use this one)
├── BBS_CMA_Team_Assignment1_GL.ipynb    # Giulia Lorelli's earlier draft
├── BBS_CMA_Team_Assignment1_II.ipynb    # Israa Ismail's earlier draft
├── Team_Assignment_1_Data_2026.csv      # Dataset
└── README.md
```
 
---
 
## Analysis
 
### Q0 — Data Preparation
- Missing value check and descriptive statistics
- Dummy coding for `Product_Category` (reference group: Beauty & Skincare)
- Distribution plots for all three dependent variables
- Multicollinearity check via VIF (all values < 5 — no issue)
 
### Q1 — Engagement Rate (OLS Linear Regression)
- Dependent variable: `Engagement_Rate` (continuous)
- Model: Ordinary Least Squares
- Key findings: TikTok and Short Video are strongest drivers; Micro-influencers outperform Macro on engagement rate
- Outputs: regression summary, coefficient plot
 
### Q2 — Click-Through (Logistic Regression)
- Dependent variable: `Click_Through` (binary)
- Model: Logit with Average Marginal Effects
- Key findings: Scarcity-framed promo deals (+39.2%), positive CTA (+19.6%), Macro influencers (+16%) drive clicks
- Outputs: log-odds coefficients, marginal effects table, coefficient plot
 
### Q3 — Comment Count (Negative Binomial Regression)
- Dependent variable: `Comment_Count` (non-negative integer)
- Model selection: overdispersion test confirmed var/mean ratio of 41.39 → Negative Binomial chosen over Poisson
- Key findings: TikTok (+38 comments), Short Video (+27 comments), positive CTA (+17 comments)
- Outputs: regression summary, marginal effects, coefficient plot
 
### Q4 — Interaction Effects
- Base model: Q1 (Engagement Rate — OLS)
- Interaction 1: `Topic_CTA_Positive × Platform` — Does a CTA work differently on Instagram vs TikTok?
- Interaction 2: `Post_Type × Caption_Sentiment` — Does sentiment impact videos differently than photos?
- Result: neither interaction significant (p=0.815, p=0.750) — confirmed via AIC comparison and ANOVA F-test (p=0.928)
- Takeaway: positive CTA is platform-agnostic; keep strategy simple
- Output: interaction plot (CTA × Platform), model comparison table
 
---
 
## Dependencies
 
```bash
pip install pandas numpy matplotlib seaborn statsmodels scipy
```
 
---
 
## How to Run
 
1. Open `BBS_CMA_Team_Assignment1_V1.2.ipynb` in Google Colab
2. Run the setup cell to install dependencies
3. When prompted, upload `Team_Assignment_1_Data_2026.csv`
4. Run all cells in order (Cell → Run All)
 
---
 
## Reference
 
Cameron, A.C. & Trivedi, P.K. (1998). *Regression Analysis of Count Data.*  
Econometric Society Monograph No. 30, Cambridge University Press.
 
---
 
## AI Use Disclaimer
 
This project was completed with the assistance of AI tools (Claude by Anthropic, Antigravity by google) for the following purposes:
- Code debugging and syntax support
- Markdown formatting and documentation
- Reviewing and structuring written commentary
 
All analytical decisions — including model selection, variable choice, interpretation of results, and marketing implications — were made by the team. AI was not used to generate or replace any core analysis or regression outputs.
 
This disclaimer is included in accordance with BBS guidelines on the responsible use of AI in academic work.