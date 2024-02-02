---
name: "Long Range Extreme Weather Forecasting: working with climate data"
image: ../assets/images/corr_heatmap_WiDS.png
description: Long range extreme weather forcasting to fight climate change.
date: 2023-03-18
layout: post
index: 4
---

# Long Range Extreme Weather Forecasting

![leader board](../../assets/images/WiDS_leaderboard.PNG)

The WiDS Datathon 2023 asks participants to using machine learning combined with traditional physics based model predictions to forecast long range sub-seasonal temperatures (mean temperature over a two-week period) within regions in the US. The provided dataset consists of climate data for a number of US locations, starting dates for the two-week observation from 2014 to 2016, and temperatures and precipitations forcasts using physics based models. Each row in the data corresponds to a single location and a single start date for the two-week period.

To solve this problem, I applied data cleaning, mainly adjusting data distributions. Then, I used the current best boosting tree model: CatBoost, and Bayesian Optimization to find the best performat model. In the end, I analyzed the feature importances.

If you are interested in further documentation, I have a blog detailed [my solution](/blog/weather-forcasting) to this problem.

Correlation Heatmap visualizations I produced in my analysis:

![heatmap](../../assets/images/corr_heatmap_WiDS.png)

[Kaggle Notebook](https://www.kaggle.com/code/tianyimasf/wids-datathon-tianyi-yukyung-and-irsa) | [Github](https://github.com/tianyimasf/kaggle/blob/main/wids-datathon-tianyi-yukyung-and-irsa.ipynb)
