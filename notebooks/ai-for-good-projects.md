# Data Science Projects

---

### MLP

[Kaggle (scoll down to "Submission")](https://www.kaggle.com/code/tianyimasf/mlp-alex-ma#Submission)

- using a significantly smaller model that turned out to be as predictive as a big model
- shorter training epochs don’t meaningfully affect accuracy either
- compared popular classical ML models and gradient boosting trees (expectedly) outperformed the neural network, especially Catboost
- finally, examined feature importances using permutation, Salient Maps (Gradient-based) and SHAP values.
- discovered that most people earning less than 50k yearly are widows.

### GeoML: EuroSAT Land Cover Classification using CNN

[Kaggle](https://www.kaggle.com/code/tianyimasf/geoml-land-cover-cnn-classification)

- Using grid search, experimented with various batch sizes, workers, epochs, learning rates and pre-trained models. 
- Achieved 98.98% accuracy with Resnet50 Moco, 32 batch size, 1e-4 learning rate, and 15 epochs.