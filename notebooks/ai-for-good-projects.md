# Data Science Projects

---

### MLP

[Kaggle (scoll down to "Submission")](https://www.kaggle.com/code/tianyimasf/mlp-alex-ma#Submission)

- Using Pytorch, predicting binary income class based on demographic info using MLP. Organized code and experimented with large and small models and long and short epochs. Drew the conclusion that a small model (2 hidden layers with 32 and 4 neurons respectively) trained with shorter (50) training epochs retains the same predictive power.
- Compared MLP performance to classical ML models and visualized various metrics including confusion matrix, precision-recall curve, ROC curve and AUC scores. Concluded that gradient boosting trees outperforms other models in all metrics where Catboost especially performs better than the more famous XGBoost model. 
- Examined feature importance using permutations, Salient Maps (Gradient-based) and SHAP values. Found that marital status, age, capital gain and education level are strong indicators of income class. Visualized the relationship between marital status and age to investigate interactions between the two, found that most people that earns less than 50k yearly are widows across all age groups. Further visualized the relationship between capital gain, education level and income class respectively and analyzed insights in the notebook.