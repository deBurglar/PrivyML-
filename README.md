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
Accuracy: 0.9711626487641135

Classification Report:
               precision    recall  f1-score   support

           0       0.78      0.70      0.74       379
           1       0.98      0.99      0.98      6175

    accuracy                           0.97      6554
   macro avg       0.88      0.84      0.86      6554
weighted avg       0.97      0.97      0.97      6554
