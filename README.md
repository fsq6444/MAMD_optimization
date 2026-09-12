This is the folder for Optimization of Membrane Distillation process.
1.1 Overview
This repository reproduces the full computational pipeline reported in the manuscript: data imputation, outlier screening, surrogate-model training and screening across nine regression algorithms, interpretability analysis (SHAP / PDP / ICE), and multi-objective inverse design by NSGA-II.
Python          3.12.3 
numpy           1.26.4
pandas          2.2.2
scipy           1.15.1
scikit-learn    1.5.1
xgboost         3.0.0
lightgbm        4.6.0
catboost        1.2.8
shap            0.49.1
pymoo           0.6.1
matplotlib      3.9.2
openpyxl        3.1.5
joblib          1.4.2

Data partitioning
The dataset is split once into training and test subsets with `train_test_split(test_size=0.2)`. The test set is touched only once, after all model selection is complete.

Cross-validation protocol 
Five-fold cross-validation uses `KFold(n_splits=5, shuffle=False)`. 
**The same folds are reused for every algorithm and every hyperparameter combination**, so between-model differences reflect algorithmic behaviour rather than resampling variability, and fold-level results are paired across models — a prerequisite for the Wilcoxon signed-rank comparisons reported in the Supporting Information.
`StandardScaler` is fitted on the full training set before cross-validation and applied unchanged within folds. This mirrors the procedure used to generate the published numbers and keeps the reported fold scores identical to `GridSearchCV.cv_results_`.

Choice of screening metric
