⚽ Premier League Fantasy Points Predictor

A machine learning pipeline that predicts Premier League player fantasy point output using underlying performance metrics — mirroring how real DFS pricing engines approach player valuation.

Rather than predicting goals and assists directly (which are noisy), this project models expected contribution from lower-level signals like xG, xA, shot quality, and progressive actions — the same signals a professional projection model would consume.


📌 Project Highlights


96.7% of predictions within ±5 fantasy points of actual output
R² = 0.95 on held-out test data
Calibration analysis to detect systematic pricing bias
Player projection tool with 80% confidence intervals
20+ engineered features including per-90 rates, efficiency ratios, and overperformance metrics



🗂️ Project Structure

premier-league-fantasy-predictor/
│
├── premier_league_predictor.ipynb   # Main notebook (all code + analysis)
└── README.md


🔧 Pipeline Overview

StepDescription1. Data GenerationSimulates a realistic PL season using statistical distributions (xG, xA, shots, etc.)2. EDADistribution analysis, xG vs goals scatter, correlation heatmap3. Feature EngineeringPer-90 rates, efficiency ratios, overperformance metrics, position encoding4. Model TrainingRidge Regression, Random Forest, Gradient Boosting with 5-fold CV5. Calibration AnalysisResidual plots to detect systematic bias across the scoring range6. Projection ToolInput any player's stats → get a point estimate + 80% CI


📊 Model Comparison

ModelMAER²CV MAERidge Regression1.7750.9541.827Random Forest1.8080.9551.965Gradient Boosting2.0110.9471.870


Ridge Regression edges out the others here — a good reminder that simpler models sometimes win on well-engineered features.




🔍 Key Findings


Minutes played is the single strongest predictor — a player who doesn't start is worth near zero
xG and xA per 90 outperform raw goals/assists for forward-looking projections — they're less noisy
xG overperformance (goals − xG) identifies clinical finishers — important for premium pricing
Residuals are normally distributed and centered at ~0, confirming the model is well-calibrated with no systematic bias



🧮 Player Projection Tool

The project_player() function takes any player's current season stats and returns:


A point estimate of their expected fantasy output
An 80% confidence interval based on the spread across Gradient Boosting estimators


pythonproject_player(
    name='Elite Striker',
    position='FW', age=27, minutes=2800,
    shots=98, shots_on_target=52, xg=14.2, xa=4.1,
    key_passes=62, progressive_passes=88,
    dribbles=71, aerial_wins=44, tackles=18, pass_accuracy=78.5
)

# Output:
# Projected Fantasy Points : 31.9
# 80% Confidence Interval  : [29.1, 34.2]


🚀 How to Run

1. Clone the repo

bashgit clone https://github.com/eyobedmerhawi/premier-league-fantasy-predictor
cd premier-league-fantasy-predictor

2. Install dependencies

bashpip install pandas numpy scikit-learn matplotlib seaborn

3. Open the notebook

bashjupyter notebook premier_league_predictor.ipynb

Or open directly in VS Code.


🛠️ Tech Stack


Python 3.x
pandas & NumPy — data manipulation
scikit-learn — modeling, feature scaling, cross-validation
matplotlib & seaborn — visualization



🔮 Extensions for Production


Add form weighting (rolling 5-game average) to capture hot/cold streaks
Incorporate opponent defensive strength as a contextual feature
Use Bayesian updating to refine projections as the season progresses
Model variance separately — some players are high-ceiling/high-floor vs stable but lower



👤 Author

Eyobed Gebregziabher

Computer Science @ Georgia State University

Built as a portfolio project demonstrating probabilistic modeling and DFS pricing methodology.
