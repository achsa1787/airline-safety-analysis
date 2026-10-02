# Should Travellers Avoid Airlines With Past Crashes?

Statistical analysis of airline safety, done as a group project (Group 2) for DS406/ST662 on the MSc Data Science at Maynooth University, April 2026.

People often say they'd avoid an airline that has had a crash. We wanted to test whether that actually makes sense, using safety records for 56 major airlines over two 15-year periods (1985–1999 and 2000–2014).

![Composite risk scores](images/09_risk_scores.png)

## Approach

1. **Fair comparison.** Big airlines fly more, so they naturally have more incidents. All counts were turned into rates per billion available seat-kilometres (ASK).
2. **Exploratory analysis.** Compared the two periods and looked at which airlines got safer or worse.
3. **Hypothesis testing.** The data is heavily right-skewed, so we used non-parametric tests:
   - **Wilcoxon signed-rank test:** did incident rates really drop between periods?
   - **Spearman rank correlation:** does a bad past predict a bad future?
4. **Composite risk score.** Combined recent incident, fatal accident and fatality rates (weights 0.25 / 0.40 / 0.35) into one 0–1 score, and grouped airlines into Low, Moderate and High risk.

## Key findings

| Question | Result |
|---|---|
| Did flying get safer? | **Yes.** Incidents fell 42.5%, fatal accidents 69.7%, fatalities 50.6%. Wilcoxon W = 799, **p = 0.0024** |
| Does past safety predict future safety? | **Not reliably.** Spearman ρ = 0.248, **p = 0.065** (not significant). Pearson r between periods is 0.05–0.40 |
| How risky are airlines today? | **51 of 56 (91%) are Low Risk.** Only Kenya Airways and Pakistan International scored High Risk |
| What drives high scores? | Often one catastrophic event (e.g. Malaysia Airlines' MH17 and MH370) rather than ongoing problems |

**Bottom line:** an airline's crash history on its own isn't a good reason to avoid it. The industry has improved a lot, and past records are a weak guide to the future once you account for how much each airline flies.

| Period comparison | Wilcoxon test |
|---|---|
| ![](images/03_period_comparison.png) | ![](images/07_wilcoxon_differences.png) |

## Repository layout

```
data/        airline-safety.csv (FiveThirtyEight)
notebooks/   airline_safety_analysis.ipynb   full analysis
images/      charts exported from the notebook
docs/        group report (PDF)
```

## How to run it

```bash
git clone https://github.com/achsa1787/airline-safety-analysis.git
cd airline-safety-analysis
pip install -r requirements.txt
cd notebooks
jupyter notebook airline_safety_analysis.ipynb
```

## Tools

Python, pandas, NumPy, SciPy (Wilcoxon, Spearman), Matplotlib, Jupyter

## Data

FiveThirtyEight [Airline Safety dataset](https://github.com/fivethirtyeight/data/tree/master/airline-safety) (CC BY 4.0). 56 airlines, no missing values.

📄 Full write-up: [docs/Airline_Safety_Report.pdf](docs/Airline_Safety_Report.pdf)
