---
name: "Fitbit Tracker Usage Analysis: the Techniques"
tools:
  [data analysis, data visualization, regression analysis, business case study]
image: ../assets/images/total_steps.png
description: An exaustive list of techniques I used to analyze Fitbit Tracker usage data
---

![Personal Step Preference](../assets/images/steps_preference.png)

# What to expect in this blog

This is going to be a slightly technical blog, just because it'll focus on the techniques I used to analyze the dataset and extract relationships and insights. There won't be any math, though, only numbers produced by a technique, what the technique does, what the numbers mean, and what's the code for it. The code is usually one-liners since R is just that cool (? jk. or am I? :p)

I thought it would be useful to just boom boom boom, get a ton of helpful techniques out there, for reference purposes. So here we go.

[Complete R Notebook for reference](https://www.kaggle.com/code/tianyimasf/fitbit-usage-trend-analysis-viz-regression)

# Exploratory Analysis

Not a lot to see here. Of course, first of all load tidyverse.

A list of common functions and short descriptions:

- head(): to see the complete first 5 rows of the dataframe, no matter how many columns there are/
