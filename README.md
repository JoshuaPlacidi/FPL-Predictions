# Predicting Fantasy Football Teams Using Machine Learning
*By minimising human bias and focusing on football statistics can a machine learning model be trained to consistantly predict high performing fantasy football teams?*

## Premise
This is a statistical study analysing the performance of varouis regression based machine learning algoirthms in their ability to predict the performance of fantasy football players in the English Premier League. In this study data structure and formatting, machine learning regression algorithms and optimisiation algorithms are all experimented with in order to create a final system capable of selecting a high performing fantasy football team for a given set of matches.

This project is conducted in the Fantasy Premier League enviroment, the offical fantasy football application of the Premier League, information of the rules of the game can be found [here](https://www.premierleague.com/news/1252542).

## Results overview
An overview of the final results of the study are summarised here for convience. This file continues, outlining the pipeline of the system and concluding with an indepth analysis of the study and results.

The final system was tested on the 2019/20 Premier League season (gameweeks 4-29) with positive results collected.

## Approach

Linear regression models were used to generate predictions for the number of fantasy points each player would score for a given week. An optimal performing team was then selected from the generated predictions using linear optimisation. The selected team must abide by all [FPL restrictions](https://fantasy.premierleague.com/help/rules). The performance of the selected team was then analysed comparing the real score to the score the system predicted, here we are concerned with maximising actual performance rather then reducing the error between predicted and actual performance (though the more accurate the model the better).

## Data
Data was sourced from the official FPL API via the [vaastav repository](https://github.com/vaastav/Fantasy-Premier-League). Statistics from the past 4 seasons of the Premier League were combined into a single csv with a unique entry for each player for each game they played. A rolling dataset was then constructed where for each entry the sum of statistics from the prevouis *n* weeks were summed. The optimal value of n was found by testing the accuracy of the models with *n* values from 1 to 9.

// Insert Image

Results showed that *n = 3* gave the smallest error in predictions. So given a player and a game, performance statistics (goals scored, assists, minutes played ect...) from the players 3 prior games are used to make predictions for the given game.

## Prediction Models

Four regression aglorithms were compared in their ability to accurately model fantasy football performance. FPL players are split into four position groups: goalkeepers, defenders, midfielders and forwards. To generate accurate predictions individual models were created for each position. Each algorithm was trained and tested on positional rolling datasets measuring the accuracy using k-fold cross validation (k=10) and the following results were generated:

// Insert Image

The results showed that linear regression dominates for each positional subset. Linear regression positional models were fine tuned to optimise performance for each position and then finialised. The accuracy of the final positional models was test again using k-fold cross validtion (k=10) with model accuracy being recorded:

// Insert Image

The results show that all models achieved an average prediction error of less than 2 points.

## Selecting Optimal Teams

