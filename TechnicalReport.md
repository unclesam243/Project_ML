## Project Overview: Credit Card Fraud Detection

### Objective

This project focuses on the development and evaluation of machine learning models for the detection of fraudulent credit card transactions. The primary objective is to accurately identify fraudulent transactions while minimizing false positives, a critical consideration given the inherent class imbalance of financial fraud datasets. This endeavor involves exploring and comparing various machine learning and deep learning methodologies to ascertain optimal performance.

### Dataset Description

The dataset employed is the "ULB Credit Card Fraud Detection" dataset, comprising anonymized transaction data from European cardholders. It includes the following features:

*   **`V` features (V1-V28)**: These represent the principal components resulting from a PCA transformation, thereby anonymizing sensitive transaction details. These features are crucial inputs for the predictive models.
*   **`Time`**: Records the elapsed time in seconds since the initial transaction in the dataset. This temporal information is valuable for identifying time-dependent fraud patterns.
*   **`Amount`**: Denotes the monetary value of the transaction.
*   **`Class`**: The binary target variable, where `0` signifies a legitimate transaction and `1` indicates a fraudulent transaction.

**Key Dataset Characteristics:**
*   **Highly Imbalanced**: Fraudulent transactions constitute a minuscule proportion (approximately 0.172%) of the total dataset, posing a significant challenge for model development.
*   **Anonymized Features**: The `V` features are pre-processed via PCA, limiting direct interpretation but providing essential numerical inputs.
*   **Temporal Aspect**: The `Time` feature enables chronological data splitting, preventing data leakage and ensuring a realistic evaluation of model performance over time.

### Methodology

The project methodology is structured as follows:

1.  **Data Loading & Verification**:
    *   Initializes a pandas DataFrame by loading `creditcard.csv`.
    *   Conducts preliminary data integrity checks, including dataset shape verification, transaction and fraud count validation, and assessment for missing values.

2.  **Exploratory Data Analysis (EDA)**:
    *   Performs an initial examination of the dataset to understand its characteristics.
    *   Visualizes the class distribution (legitimate vs. fraudulent transactions).
    *   Analyzes the distribution of `Amount` and `Time` features for both legitimate and fraudulent transactions to identify potential distinguishing patterns.

3.  **Data Preprocessing**:
    *   Prepares the raw data for model consumption.
    *   Addresses missing values by row-wise deletion (if any are present).
    *   Separates the feature matrix (X) from the target variable (y, the `Class` column).
    *   Applies `RobustScaler` to scale features, particularly `Amount` and `Time`, to mitigate the influence of outliers.
    *   Utilizes `StratifiedKFold` for cross-validation to ensure consistent representation of the minority class across all folds, which is crucial for imbalanced datasets.
    *   Implements a dedicated `find_best_threshold` function to optimize the classification threshold based on the F1-score, determined independently for each model and fold using the validation set.

4.  **Model Training & Evaluation**:
    Four distinct machine learning and deep learning models are trained and rigorously evaluated:

    *   **Logistic Regression (Linear Baseline)**:
        *   Serves as a fundamental linear baseline to establish a minimum performance benchmark.
        *   Employs `class_weight='balanced'` to address the class imbalance issue.
        *   Evaluated through a 5-fold stratified cross-validation strategy.

    *   **Random Forest**:
        *   An ensemble method leveraging multiple decision trees for enhanced predictive power.
        *   Incorporates `class_weight='balanced'` to manage class disparity.
        *   Analyzes feature importances, averaged across cross-validation folds, to identify key predictive variables.
        *   Evaluated through a 5-fold stratified cross-validation strategy.

    *   **XGBoost**:
        *   A high-performance gradient boosting framework renowned for its efficacy in tabular data challenges.
        *   Utilizes `scale_pos_weight` for effective handling of class imbalance.
        *   Evaluated through a 5-fold stratified cross-validation strategy.

    *   **Multi-Layer Perceptron (MLP) / Deep Learning**:
        *   A neural network architecture (`FraudMLP` class) incorporating dense layers, Batch Normalization, ReLU activation functions, and Dropout for regularization.
        *   Implemented using the PyTorch deep learning framework.
        *   Leverages `BCEWithLogitsLoss` with an adjusted `pos_weight` parameter to address class imbalance.
        *   Training incorporates early stopping based on validation F1-score performance and averages predictions across multiple random seeds to enhance result stability and robustness.
        *   Evaluated through a 5-fold stratified cross-validation strategy.

5.  **MLP Ablation Study**:
    *   A systematic investigation into the impact of varying MLP architectures (e.g., number of hidden layers) and loss functions (`weighted_bce` vs. `focal_loss`) on model performance (primarily AUPRC).
    *   The objective is to identify the optimal MLP configuration for this specific fraud detection task.

6.  **Risk Analysis**:
    *   **Cross-Validation AUPRC Variance**: Quantifies the stability of AUPRC scores across folds for different models.
    *   **Bootstrap Confidence Intervals**: Provides a robust estimate of model performance uncertainty.
    *   **Threshold Sensitivity**: Analyzes how precision, recall, and F1-score vary with different classification thresholds.
    *   **Cost-Sensitive Analysis**: Quantifies the financial impact of false positives and false negatives, providing a business-oriented performance metric.

7.  **Final Comparison & Visualization**:
    *   Presents a summary table comparing the mean and standard deviation of key metrics (AUPRC, F1, Precision, Recall, Threshold) for all models.
    *   Generates Precision-Recall (PR) curves to visualize trade-offs between precision and recall across models.
    *   Displays Confusion Matrices for each model at their respective optimal thresholds.
    *   Includes Reliability Diagrams (Calibration Plots) to assess how well predicted probabilities align with actual outcomes, highlighting potential calibration issues due to class-weighted training.

### Key Metrics

*   **AUPRC (Area Under the Precision-Recall Curve)**: The primary metric for evaluating models on imbalanced datasets, as it focuses on the positive class.
*   **AUROC (Area Under the Receiver Operating Characteristic Curve)**: A common metric for binary classification.
*   **F1-Score**: The harmonic mean of precision and recall.
*   **Precision**: The proportion of correctly identified positive predictions (TP / (TP + FP)).
*   **Recall**: The proportion of actual positives that were identified correctly (TP / (TP + FN)).
*   **Threshold**: The decision boundary used to classify transactions as fraud or legitimate.
*   **Calibration Error**: Measures how well predicted probabilities reflect actual event frequencies.
