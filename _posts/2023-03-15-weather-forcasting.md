---
title: Extreme Weather Forcasting Contest
tags:
  [
    Weather Forcasting,
    Data Preprocessing,
    Gradient Boosting,
    Decision Tree,
    Bayesian Optimization,
  ]
style: fill
color: light
description: Long range extreme weather forcasting for fighting climate change.
---

## Background

The WiDS Datathon 2023 focuses on a prediction task involving forecasting sub-seasonal temperatures (temperatures over a two-week period, in our case) within the United States. They used a pre-prepared dataset consisting of weather and climate information for a number of US locations, for a number of start dates for the two-week observation, as well as the forecasted temperature and precipitation from a number of weather forecast models. Each row in the data corresponds to a single location and a single start date for the two-week period. The task is to predict the arithmetic mean of the maximum and minimum temperature, for each location and start date.

## Motivation

This is my official first full data science project(and this is my first technical blog! Yay!) I was looking for data science activties to join, and I got to know that Stanford is hosting a Women in Data Science conference, along with their datathon which is branded as open to all levels. This is a great execuse to get access to a well-curated, structured dataset, with a good question, and just start to get hands dirty. Besides, climate change is an important issue so I want to give it a try.

## Solution

My solution first preprocess the data. It first solve location discrepencies by scaling the longitude and latitutde, then one-hot encoding categorical data, splitting date feature into 3 numerical variables, filling missing values, removing outliers and power transforming skewed data. Finally, I run Adverserial Validation to check if for each variable the training data distribution matches the test data distribution, then removed a couple features where there is a concept drift.

For training I used an algorithm for gradient boosting on decision trees: [Catboost](https://arxiv.org/abs/1706.09516), optimized by Bayesian Optimization, which in one sentence picks the next parameter value based on the performance of previous parameter value. In the end I also visualized feature importance to gain further insights into the trained model.

Finally, the training RMSE for our model is 0.40107, 0.39942 for the validation set, and 1.222 for the test set. It's on top 50% in the competition.

## Challenges

My challenges in building this solution is in data preprocessing. Specifically, I was learning the correct way to:

- Tranform skewed data
- Remove outliers
- Check if distributions of training set are similar to test set

The first challenge to transform skewed data is to determine whether it's feasible in this contest. If the training data is transformed to be used for training, then the test set also needs to be transformed before making predictions. After verifying that this is indeed the case, I made sure that the test set is given to us to be used. Then, I found the variables that's skewed, and investigated different transform methods, including Min Max Scaler, log and power transform, and used KDE plot to verify the findings and results. Because some of the data is negative, log transform can't be used, and power transform looked better.

For removing outliers, I used Tukey's method. I compared different implementations, and picked one that looked the most clean and intuitive to me.

For checking if distributions of training set are similar to test set, I tried the algorithm suggested in this [medium article](https://medium.com/@praveenkotha/how-to-find-whether-train-data-and-test-data-comes-from-same-data-distribution-9259018343b), except its last(4th) step is incorrect: a classifier needs to be trained using cross validation on the entire dataset, instead of the training data, because the label of the training data will be homogeneously 1. Based on this reason, I adopted [this implementation](https://www.kaggle.com/code/kooaslansefat/wids-2023-woman-life-freedom) of the algorithm and it works perfectly.

## Non-technical Challenge

Before all the technicals happened, there is also a non-technical challenge, which by no means is easier and actually took me some time. Before data preprocessing, I felt the need to understand the meanings of the data given, so I actually spent a lot of my time looking through the documentation on the Kaggle website. In their Data tab the descriptions are only halvely complete. For example, almost half of the variables have name postfixed by a number, but the documentation never explained the meaning of the numbers -- maybe it's days, but then why they have different range? It left me very confused. In the end, I gained some understandings, but not complete. I'd imagine this might get easier as one gradually gains expertise in climate science, or simply have start the project from scratch and thus have access to the data source.

## Future Steps

The data is well-preprocessed, however, the model isn't fine-tuned. One future step could be to fine-tune the model and maybe try different optimizers like Adam.

Secondly, there are more models that could fit this dataset. I can choose some of those, compare the results and use the essemble method to improve RMSE.

## Source Code

Since a lot happened in the source code, I'm not attaching any code snippet here. If you are interested in checking it out, [here](https://github.com/tianyimasf/kaggle/blob/main/wids-datathon-tianyi-yukyung-and-irsa.ipynb) is the full code for this project.

That's all! Hope you enjoyed, and feel free to comment below if you have any thoughts!
