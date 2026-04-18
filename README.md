# Project_ML

# ES -update to the project:
After receiving feedback on the initial implementation, several updates were made to improve the reliability of the pipeline while keeping the same sequential structure:

Replaced StandardScaler with RobustScaler on Time and Amount to better handle the extreme outliers in the Amount feature.
Replaced the single 80/20 split with 5-fold stratified cross-validation, allowing results to be reported as mean ± std across folds for a more honest performance estimate.
Formalised threshold selection — now searched from 0.01 to 0.99 in steps of 0.01, per model, per fold, on validation data only. The selected threshold is reported alongside all metrics.
Added calibration reliability diagrams for all four models to verify that predicted probabilities are meaningful and not distorted by class-weighted training.



The ablation study shows that MLP performance is sensitive to configuration but overall improvements are limited. The best configuration used a single hidden layer with 64 units, dropout of 0.3, and focal loss, achieving an AUPRC of approximately 0.66. Focal loss consistently outperformed weighted binary cross-entropy, likely due to better handling of class imbalance. However, deeper architectures did not improve performance and often led to increased variance across folds. Overall, the MLP did not outperform tree-based models such as Random Forest, which achieved significantly higher F1 scores.
