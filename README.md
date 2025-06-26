# PrivyML-


## Logistic Regression

| Metric        | Class 0 (denied) | Class 1 (approved) | Overall      |
| ------------- | ---------------- | ------------------ | ------------ |
| **Precision** | 0.63             | 0.96               |              |
| **Recall**    | 0.29 ❗️          | 0.99 ✅             |              |
| **F1-score**  | 0.40 ❗️          | 0.97 ✅             |              |
| **Accuracy**  |                  |                    | **0.9491** ✅ |

⚠️ Key Takeaways:
✅ The model is great at predicting approvals (class 1)

❌ It's poor at catching denials (class 0) — recall is just 0.29, meaning 71% of denials are missed

🔺 High overall accuracy is misleading here due to class imbalance (6175 vs 379)

