# NFL-Draft-Prediction-Project
- Author: Jacob Wang
- Created: 11/26/2022

![NFL_Draft_logo svg](https://user-images.githubusercontent.com/112730629/221983779-bf19c33f-053b-40bc-b332-4b248ef790e5.png)


## Project Description: Using NFL Draft Combine player performance data from 2009-2019, create a machine learning model to predict as accurately as possible whether or not a player will be drafted to an NFL team. 

# Data Dictionary 

Column Name | Description
---|---
Year | Year player is entering draft
Player| Player name
Age| Age of the player
School | School player attended
Height | Player height (meters)
Weight | Player weight (kg)
Sprint_40yd | Player's official 40-yd dash time (seconds)
Vertical_Jump | Player's max vertical jump (cm)
Bench_Press_Reps | Player's max # of 225lb bench press reps
Agility_3cone | Player's official 3-cone time (seconds)
Shuttle | Player's official shuttle run time (seconds)
Drafted..tm..rnd.yr | Team, round, and year player was drafted (or not drafted)
BMI| Player's body mass index
Player Type | Player's specialty (offense/defense)
Position Type | Player's position type
Position | Player's position
Drafted | Was the player drafted? (Yes/No)

# Explanatory Visuals

## Overview of Feature Correlation
![nflHeatMap](https://user-images.githubusercontent.com/112730629/204176763-d917852a-9212-43e8-b2d6-ef0651b2c23b.png)
* Many strong relationships between our features, most have to do with weight and event times 
* Weight and longer event times/bench press reps very strongly positively correlated 

## 40-yd Dash Times vs. Drafted
![40timevsDrafted](https://user-images.githubusercontent.com/112730629/204178480-8b1ef4e6-4c46-4abd-8300-2b804b1d8296.png)
* Players who were drafted were, on average, a little quicker than those who were not drafted
* Fast 40-yd dash time alone did not guarantee a draft pick 

## 40-yd Dash Time by Position Type
![40byPosType](https://user-images.githubusercontent.com/112730629/204183687-c2cd59c9-31d9-4db0-8b38-a4e1b0e40cce.png)
* Defensive backs and running backs/receivers were quickest, followed by linebackers and special teams
* Defensive linemen were much quicker than offensive linemen 

## Bench Press Reps vs BMI by Draft Status
![benchBMIdrafted](https://user-images.githubusercontent.com/112730629/204183934-c919ee67-ebc7-4728-b5ec-1a1cdd6887f3.png)
* Naturally, as BMI increased, so did bench press reps
* Those with above average bench press reps for their BMI tended to get drafted over others 

# Classification Modeling
* Tested out and tuned several different classification models to see which models had strongest performance 
  - KNeighbors
  - Decision Tree
  - Random Forests
  - Logistic Regression
  - adaBoost
  - LightGBM
  - XGBoost
  - Gradient Boosting
* Applied principal component analysis (PCA) to data in order to determine whether better results could be obtained with dimension reduction. However, all classification metrics declined as a result of PCA.  
* Evaluating classification models
  - NFL teams prioritize minimizing false positives (bad draft picks) so other than general model accuracy our most relevant metric is precision
  - Top 3 performers:
    - Tuned adaBoost Model - Precision: 0.81, Recall: 0.93, Testing accuracy: 0.83, f1-score: 0.87
    - Tuned XGBoost Model - Precision: 0.79, Recall: 0.98, Testing accuracy: 0.83, f1-score: 0.87
    - Baseline GradientBoost Model - Precision: 0.80, Recall: 0.97, Testing Accuracy: 0.82, f1-score: 0.88

# Recommended Production Model: 
* The Tuned adaBoost Model would best suit the business needs of NFL teams looking to improve their draft results. 
* While other models had similar precision scores as the Tuned adaBoost model, this model outperformed the other models in the rest of classification metrics such as recall, f-1 score, and testing accuracy. 
* The Tuned adaBoost model minimized false positives as much as possible and still had a respectable recall score, allowing NFL teams to also minimize the amount of missed good draft picks. 
