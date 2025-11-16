# NBA Home Spread Prediction Using Machine Learning  
**Author:** Nikola Stojkovski  
**Last Updated:** June 13, 2025  

---

## 📌 Project Overview
This project applies machine learning to predict NBA home spreads and evaluate whether a data-driven model can outperform sportsbooks. It integrates traditional box score data, injury reports, and Reddit sentiment to assess how each contributes to predictive accuracy and simulated betting performance.

Despite the challenge posed by the sportsbook margin, this project demonstrates a complete end-to-end sports analytics pipeline involving data ingestion, feature engineering, model comparison, and real-world evaluation.

---

## 🎯 Objectives
- Build a reproducible pipeline for predicting NBA point margins.  
- Engineer features from **box scores**, **injury data**, and **Reddit sentiment**.  
- Train and compare models including Ridge, Random Forest, XGBoost, Gradient Boosting, and an Ensemble.  
- Use a **custom betting simulator** to evaluate results in a realistic wagering context.  
- Determine which data sources provide real predictive signal.

---

## 📊 Data Sources
- **NBA Box Scores** — processed into rolling averages for team and player performance.  
- **Injury Reports** — merged and aggregated to estimate impact of missing players.  
- **Reddit Sentiment** — scraped and analyzed using VADER, then smoothed over 7-day windows.

### Key preprocessing steps
- Filter to home games only  
- Create back-to-back game indicators  
- Construct 5-game rolling averages  
- Merge rolling averages with injury availability  
- Generate sentiment rolling averages  
- Remove highly collinear features  
- Chronological 80/20 train-test split to prevent leakage  

---

## 🤖 Modeling Approach
Four datasets were built:

1. **Box Only**  
2. **Box + Injuries**  
3. **Box + Reddit Sentiment**  
4. **Box + Injuries + Sentiment**

Each dataset was used to train:

- Ridge Regression  
- Random Forest  
- XGBoost  
- Gradient Boosting  
- Ensemble (mean of all four)

Additional techniques used:
- **TimeSeriesSplit** cross-validation  
- **GridSearchCV** for hyperparameter tuning  
- A custom evaluator that compares predicted margin vs. Vegas spread and sizes bets using a tiered unit system

---

## 📈 Results

### Predictive Accuracy
- Most models clustered around **49–51% accuracy**.  
- Tree-based models (XGBoost, Gradient Boosting) consistently outperformed Ridge.  
- **Model 3 (Box + Sentiment)** produced the strongest overall results.

### Betting Simulation
Best and worst ROIs:
- **Best ROI:** –2.08% (XGBoost, Model 3)  

Every model produced negative ROI after accounting for the sportsbook margin, illustrating the difficulty of generating profit in this domain.

### Key Takeaways
- Reddit sentiment added real signal.  
- Injury features—engineered naïvely—reduced performance.  
- Ensemble models did not consistently outperform the best individual models, indicating correlated errors.

---

## 🧠 What I Learned
- Sports betting markets are extremely efficient; box score data alone won’t beat them.  
- Sentiment helps when engineered correctly.  
- Injury valuation is a complex modeling problem requiring deeper player-level context.  
- Proper time-aware validation is essential in sports analytics.

---

## 🔧 Future Improvements
- Replace VADER with a **RoBERTa-based sentiment model**.  
- Add modern NBA analytics (Four Factors, pace-adjusted stats, luck-adjusted shooting, RAPM).  
- Build a robust injury-impact model using on/off data, usage rates, and replacement-level modeling.  
- Incorporate market-aware strategies such as closing-line value (CLV) prediction.
