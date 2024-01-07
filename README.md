# March-Madness-Predictions
Utilizing Feature Engineering and a Random Forest Regressor to predict NCAA March Madness 2023 Tournament game outcomes

## Introduction/Background
For years, I entered several NCAA March Madness basketball tournament bracket pools with my friends and could never correctly pick game outcomes to win amongst the group. A few years ago, I discovered a Kaggle competition with a data repository consisting of 40 files (223 MB in total) [**[1]**](#ref1), including files with game outcomes for every NCAA Division I basketball game played from 1985 to present day, weekly team rankings dating back to 2003, and team shooting percentages across all games during this time period, to name a few. During data exploration, I discovered an opportunity to gain a competitive edge against friends using machine learning, and I began developing features to train a model. For this project, I not only wanted to predict game winners, but I also wanted to predict how large large the margin of victory would be for each matchup.  

## Methods
### Feature Engineering
I pulled in data from www.kaggle.com/competitions/march-machine-learning-mania-2023/data and converted relevant files to pandas dataframes. Because data was in many different formats I had to construct columns that were uniform across dataframes. After formatting team columns and the target column (Score_differential) appropriately I created the following features: 

- Seed_diff: Difference in seed between teams competing in NCAA tournament games (integer values 1-16).
- Ranking_diff: Difference in ranking between teams competing in NCAA regular season games. This is derived from Massey Ratings and updated weekly.
- Tourney_games_diff: Difference in the number of tournament games participated in over the last 4 seasons between each team.
- Average_score_diff: Average score difference in all previous matchups between two competing teams.
- Percent_fg_diff: Difference in seasonal field goal percentage between teams at the time of their matchup.

### Model Selection
I used GridSearchCV and Mean Squared Error as a loss metric on a Random Forest Regressor to determine the best blend of hyperparameters for regression.

Most effective hyperparameters:

100 random trees in the forest
2 features used in bootstrapping
a minimum of 10 samples per leaf
a minimum of 32 samples required ot split a tree

## Observed Results
As shown in the analysis tab of the March_Madness_2023.xlsx file, the Mean Average Error across all tournament games was 9.18 points. Considering the chaotic nature of the tournament, this is a very accurate result. My model chose UCLA to win the tournament; however, the model was unable to capture injuries prior to the tournament - UCLA's best player was injured the game before the tournament began - which can lead to inaccurate assumptions on team performance throughout the tournament. In future years, I will create a separate binary classifier using similar features to predict win probabilities instead of spread values. This should lead to better bracket performance.

## Folders
#### Data - folder containing the following files:
- MNCAATourneyCompactResults: historical results (winning score/losing score) for all previous tournament games
- MRegularSeasonCompactResults: historical results (winning score/losing score) for all previous regular season games
- MNCAATourneyDetailedResults: historical in-depth game statistics (field goal pct., 3 point pct., etc.) for all previous tournament games
- MRegularSeasonDetailedResults: historical in-depth game statistics (field goal pct., 3 point pct., etc.) for all previous regular season games
- MNCAATourneySeeds: historical data aligning teams to their respective tournament seed
- MMasseyOrdinals_thru_Season2023_Day128: historical data containing weekly rankings for all eligible tournament teams
- SampleSubmission2023: template for final output file with predictions for every possible game
- MTeams: maps team names to team ID's

## Files
- March_Madness_2023.ipynb: Jupyter notebook containing all featuring engineering, model selection, and spread predicting code
- submission2023.csv: Output of Jupyter notebook, contains spread predictions for every potential 2023 March Madness matchup
- March_Madness_2023.xlsx: Contains the bracket created following submission2023.csv predictions and an analysis on model error in terms of point differentials

## References:
<a id="ref1"></a> [1] Jeff Sonas, Maggie, Will Cukierski. (2023). March Machine Learning Mania 2023. Kaggle. https://kaggle.com/competitions/march-machine-learning-mania-2023. 

