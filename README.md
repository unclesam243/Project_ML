# Project_ML

# ES -update to the project:
After receiving feedback on the initial implementation, several updates were made to improve the reliability of the pipeline while keeping the same sequential structure:

Replaced StandardScaler with RobustScaler on Time and Amount to better handle the extreme outliers in the Amount feature.
Replaced the single 80/20 split with 5-fold stratified cross-validation, allowing results to be reported as mean ± std across folds for a more honest performance estimate.
Formalised threshold selection — now searched from 0.01 to 0.99 in steps of 0.01, per model, per fold, on validation data only. The selected threshold is reported alongside all metrics.
Added calibration reliability diagrams for all four models to verify that predicted probabilities are meaningful and not distorted by class-weighted training.



The ablation study shows that MLP performance is sensitive to configuration but overall improvements are limited. The best configuration used a single hidden layer with 64 units, dropout of 0.3, and focal loss, achieving an AUPRC of approximately 0.66. Focal loss consistently outperformed weighted binary cross-entropy, likely due to better handling of class imbalance. However, deeper architectures did not improve performance and often led to increased variance across folds. Overall, the MLP did not outperform tree-based models such as Random Forest, which achieved significantly higher F1 scores.

# Risks_and Mitigation_Ryan_Adoremos_IPYNB
The implementation addresses each of the key risks through specific sections of the code. Risk 1 (AUPRC instability under cross-validation) is handled in the cv_auprc function under “Risk 1: Cross-Validation (AUPRC Variance)”, where Stratified K-Fold is used to compute the mean and standard deviation of AUPRC. The results (Random Forest: 0.8375 ± 0.0210; Logistic Regression: 0.7599 ± 0.0205) show that performance is consistent across different splits, meaning the model’s results are stable and not due to randomness. This is further supported by the “Bootstrap Confidence Intervals” section (bootstrap_ci function), where the 95% confidence interval for Random Forest (0.8055, 0.8674) confirms that the model’s performance remains reliable. Risk 2 (whether more complex methods like focal loss would improve results) is addressed through the combination of cross-validation and the “Risk 2: Threshold Sweep” section. The strong cross-validation results already show solid performance, and the threshold sweep demonstrates how precision, recall, and F1-score change with different thresholds, indicating that tuning the decision threshold has a meaningful impact. This supports the idea that more complex loss functions may not provide significant additional benefit. Risk 3 (high computational cost) is directly evaluated in the cross-validation block using time.time(), where the total runtime is about 474 seconds. This shows that even with a large dataset, the full evaluation process remains computationally feasible, confirming that the approach is practical to run.
