# BBS Customer & Marketing Analytics


---

## Team Assignment 1 — 2026
### What Makes an Influencer Post Work?

---
 
## Team & Contributions
 
| Team Member |
|---|
| Iolanda Costa |
| Romain Derguini |
| Francesco Gambera |
| Israa Ismail |
| Giulia Lorelli |
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

---

## Team Assignment 2 — 2026
### BrandPulse Analytics: Decoding Three Brands

---

## Team & Contributions

| Team Member |
|---|
| Israa Ismail |
| Romain Derguini |
| Iolanda Costa |
| Giulia Lorelli |
| Francesco Gambera |

---

## Overview

This project analyses a dataset of 600 social media posts across three brands — **LumoraBeauty**, **FitPulse**, and **TechNest** — on behalf of **BrandPulse Analytics**. The goal is to decode what drives post engagement using NLP-derived features (sentiment, topic classification, emoji usage) alongside brand-level characteristics.

The analysis is conducted entirely in Python using a Jupyter Notebook, progressing through six research questions (Q0–Q6).

---

## Dataset

**File:** `Team Assignment 2 Data 2026.csv`  
**Source:** Provided by BBS / Dr. Umut Konuş (2026)

| Variable | Type | Description |
|---|---|---|
| `Post_ID` | Integer | Unique post identifier |
| `Brand` | Categorical | LumoraBeauty, FitPulse, or TechNest |
| `Handle` | String | Brand social media handle |
| `Post_Text` | String | Full text of the social media post |
| `Total_Followers` | Integer | Brand's total follower count |
| `Total_Posts_LastYear` | Integer | Number of posts published in the last year |
| `Num_Likes` | Integer | Number of likes on the post |
| `Num_Comments` | Integer | Number of comments on the post |
| `Num_Reposts` | Integer | Number of reposts/shares |

---

## Project Structure

```
├── CMA2_final.ipynb                    # Final merged notebook (use this one)
├── CMA_2-2.ipynb                       # Earlier draft (Israa)
├── CMA_2II.ipynb                       # Earlier draft (team)
├── Team Assignment 2 Data 2026.csv     # Dataset
├── Team Assignment 2 Data 2026.xlsx    # Dataset (Excel format)
└── README.md
```

---

## Analysis

### Q0 — Data Loading & Preparation
- Load and inspect the 600-post dataset (9 columns, 0 nulls)
- Confirm equal brand distribution: 200 posts per brand
- Install dependencies: `TextBlob`, `emoji`, `vaderSentiment`, `transformers`

### Q1 — Sentiment Analysis (TextBlob)
- Derived variable: `Sentiment_Score` (polarity: −1 to +1)
- Most posts cluster around 0–0.25 — slightly positive, right-skewed
- FitPulse and LumoraBeauty are more positive than TechNest (bimodal distribution)
- Limitation: TextBlob does not interpret emojis or detect sarcasm

### Q2 — Topic Classification (Zero-Shot, Hugging Face)
- Model: `facebook/bart-large-mnli`
- Labels: Informative, Entertaining, Promotional
- Informative content dominates all three brands (70–86%)
- LumoraBeauty most informative (85.5%); FitPulse most balanced

### Q3 — Paralinguistic / Emoji Analysis
- Derived variables: `Emoji_Count`, `Emoji_Desc`, `Emoji_List`, `Emoji_Sentiment` (VADER)
- TechNest uses the most emojis on average (2.56); FitPulse the fewest (2.30)
- Emoji choice is brand-distinctive: ✨💛🌸 (LumoraBeauty), 💪🔥 (FitPulse), 💻⚡ (TechNest)
- Correlation between emoji count and text sentiment is near zero (r = 0.02)

### Q4 — Drivers of Engagement (OLS Regression)
- Outcome variables: `Num_Likes` and `Num_Comments`
- Model: OLS (justified by large engagement counts where normal approximation holds)
- Key findings: `Emoji_Count` and `Total_Followers` are consistently significant predictors
- Each additional emoji ≈ +335 likes and +24 comments
- Informative and Promotional posts suppress engagement vs Entertaining (reference category)
- Sentiment alone is not significant once other variables are controlled for

### Q5 — Brand Differences (Interaction Effects & Separate Models)
- Interaction terms tested: Sentiment × Brand, Promotional × Brand
- Separate OLS models estimated per brand to compare coefficients
- **FitPulse**: strongest sentiment effect (+501 likes per unit); Entertaining content dominates
- **LumoraBeauty**: strongest emoji effect (+632 per emoji); Informative posts drive more likes
- **TechNest**: weakest sentiment effect; functional/practical content works best
- Promotional posts suppress FitPulse engagement but show modest lift for LumoraBeauty

### Q6 — Managerial Implications & Conclusions
- Top universal drivers: emoji density, follower base, entertaining content format
- Brand-specific strategies derived from separate model results
- Limitations flagged: NLP accuracy, no causal identification, 600-post snapshot

---

## Dependencies

```bash
pip install pandas numpy matplotlib statsmodels textblob emoji vaderSentiment transformers datasets tqdm
```

---

## How to Run

1. Open `CMA2_final.ipynb` in Google Colab
2. Run the setup cell to install dependencies
3. When prompted, upload `Team Assignment 2 Data 2026.csv`
4. Run all cells in order (Cell → Run All)

---

## Reference

Cameron, A.C. & Trivedi, P.K. (1998). *Regression Analysis of Count Data.*  
Econometric Society Monograph No. 30, Cambridge University Press.

Lewis, M. et al. (2019). *BART: Denoising Sequence-to-Sequence Pre-training for Natural Language Generation, Translation, and Comprehension.* arXiv:1910.13461.

---

## AI Use Disclaimer

This project was completed with the assistance of AI tools (Claude by Anthropic) for the following purposes:
- Code debugging and syntax support
- Markdown formatting and documentation
- Reviewing and structuring written commentary

All analytical decisions — including model selection, variable choice, interpretation of results, and marketing implications — were made by the team. AI was not used to generate or replace any core analysis or regression outputs.

This disclaimer is included in accordance with BBS guidelines on the responsible use of AI in academic work.