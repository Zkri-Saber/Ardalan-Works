# Adaptive Ensemble Feature Selection and Genetic Algorithm-Tuned Ensemble Model for Robust Heart Disease Prediction

## Methodology

### Step 1: Dataset Collection & Integration

**1.1 Select Global Datasets**

- **Sources:**
  - UCI: Cleveland, Statlog, Hungarian, Long Beach VA
  - Kaggle: Framingham, Heart Failure, Cardiovascular Disease

- **Ensure:**
  - Common clinical features such as age, cholesterol, chest pain, blood pressure
  - Harmonized column names for unified analysis

**1.2 Preprocessing**

- Handle missing values:
  - KNN Imputer for numerical features
  - Mode or correlation-based imputation for categorical features
- Detect and remove outliers:
  - Isolation Forest or Z-score method
- Normalize features:
  - MinMaxScaler or RobustScaler

---

### Step 2: Ensemble Feature Selection (EFS)

**2.1 Apply Multiple Feature Selection Techniques**

- **Filter Methods:** Information Gain, Chi-Square, Fisher Score  
- **Embedded Methods:** LASSO, Random Forest Feature Importance  
- **Wrapper Methods:** Recursive Feature Elimination (RFE)

**2.2 Ensemble the Feature Ranks**

- Normalize feature importance scores to a 0–1 scale  
- Combine using mean rank aggregation or majority voting  
- Experiment with top-k feature subsets (e.g., top 5, 7, 10)

---

### Step 3: Handle Class Imbalance

**3.1 Analyze Class Distribution**

- Calculate the class imbalance ratio

**3.2 Apply Adaptive Sampling**

- If imbalance ratio < 1:3 → Use SMOTE + Tomek Links  
- If severe imbalance → Use ADASYN  
- Apply sampling inside cross-validation folds to prevent data leakage

---

### Step 4: Model Design

**4.1 Base Classifiers**

- Random Forest  
- XGBoost  
- LightGBM  
- Logistic Regression

**4.2 Genetic Algorithm for Hyperparameter Optimization**

- Use GA to optimize model parameters  
- **Fitness Function:** F1-score or AUC on validation set  
- **Genetic Operations:**
  - Selection: Tournament Selection
  - Crossover: Uniform or One-point Crossover
  - Mutation: Random Bit Flip or Gaussian Noise
- Perform k-fold cross-validation in each generation

---

### Step 5: Ensemble Learning

**5.1 Build Final Ensemble**

- Use Soft Voting or Stacking  
- For Stacking: use Logistic Regression as meta-learner  
- Compare ensemble performance vs. individual base models

---

### Step 6: Evaluation Metrics

**6.1 Model Performance**

- Accuracy  
- Precision  
- Recall (Sensitivity)  
- Specificity  
- F1-Score  
- ROC-AUC  
- PR-AUC (critical for imbalanced data)

**6.2 Robustness Testing**

- Inject Gaussian noise to simulate sensor/data collection noise  
- Use SHAP to test feature importance stability

---

### Step 7: Explainability Analysis

**7.1 SHAP Analysis**

- **Global:** Determine overall feature importance  
- **Local (Instance-level):** Explain why a specific patient was classified as high-risk

---

### Step 8: Cross-Dataset Generalization (Optional)

- Train on one dataset (e.g., UCI)
- Test on a different dataset (e.g., Kaggle or holdout portion of the unified dataset)
- Evaluate the model’s generalization and transferability across sources
