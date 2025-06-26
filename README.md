## PrivyML-


# Logistic Regression

| Metric        | Class 0 (denied) | Class 1 (approved) | Overall      |
| ------------- | ---------------- | ------------------ | ------------ |
| **Precision** | 0.63             | 0.96               |              |
| **Recall**    | 0.29 ❗️          | 0.99 ✅             |              |
| **F1-score**  | 0.40 ❗️          | 0.97 ✅             |              |
| **Accuracy**  |                  |                    | **0.9491** ✅ |

### ⚠️ Key Takeaways:
-✅ The model is great at predicting approvals (class 1)

-❌ It's poor at catching denials (class 0) — recall is just 0.29, meaning 71% of denials are missed

-🔺 High overall accuracy is misleading here due to class imbalance (6175 vs 379)

---

# Decision Trees

| Metric           | Class 0 (Denied) | Class 1 (Approved) | Comments                                         |
| ---------------- | ---------------- | ------------------ | ------------------------------------------------ |
| **Precision**    | 0.66 ✅           | 0.98 ✅             | Much better than Logistic Regression for Class 0 |
| **Recall**       | 0.66 ✅           | 0.98 ✅             | Class 0 recall stayed high                       |
| **F1-score**     | 0.66 ✅           | 0.98 ✅             | Class 0 is balanced now                          |
| **Accuracy**     | 0.9606 ✅         |                    | Better than before!                              |
| **Macro Avg**    | 0.82             |                    | Tells us both classes are treated fairly         |
| **Weighted Avg** | 0.96             |                    | Considers class imbalance; still very high       |

### 🧠 Summary
-> The decision tree is now able to understand the patterns behind who should be denied access just as well as it does for approvals, and it does so without being unfairly biased toward approvals. It’s smarter and more balanced.

---

# XGBoost

| Model                            | Class 0 Recall | Class 0 Precision | Accuracy    | Remarks                               |
| -------------------------------- | -------------- | ----------------- | ----------- | ------------------------------------- |
| Logistic Regression (no weights) | 0.29 ❌         | 0.63              | 94.9%       | Ignored rare class                    |
| Logistic (balanced)              | 0.89 ✅         | 0.38 ❗️           | 90.8%       | Caught more Class 0, but less precise |
| Decision Tree                    | 0.66 ✅         | 0.66 ✅            | 96.0%       | Good balance                          |
| **XGBoost**                      | **0.70 ✅**     | **0.78 ✅**        | **97.1% ✅** | Best performance so far               |

### ✅ Key Takeaways from Model Comparison:

**XGBoost outperforms all** models with the best balance between accuracy and rare class (Class 0) detection — making it ideal for production.
