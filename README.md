## PrivyML-


---

## 📌 Problem Statement

In many large organizations like Amazon, employees frequently request access to internal resources (tools, data, services). Approving or denying such access manually can be slow, inconsistent, and prone to human error.

The **goal** of this project is to **predict whether an employee should be granted access to a requested resource** based on historical access patterns. Using machine learning models, we aim to automate the decision process to improve speed, consistency, and security.

### 💡 Why This Matters:

* 🚫 Prevent unauthorized access to sensitive systems
* ✅ Ensure fast approvals for legitimate requests
* 🔁 Reduce workload on access control teams
* 📊 Leverage patterns in manager behavior, roles, departments, and resources to make predictions

---


## 💾 Dataset Description

The dataset comes from the **[Amazon Employee Access Challenge](https://www.kaggle.com/competitions/amazon-employee-access-challenge)** on Kaggle. It contains **historical records of access requests** made by Amazon employees and whether they were **approved or denied**.

Each row represents one access request made by an employee.

### 📐 Features:

| Column Name  | Description                                                       |
| ------------ | ----------------------------------------------------------------- |
| `resource`   | ID of the internal resource being requested                       |
| `mgr_id`     | Unique ID of the manager associated with the employee             |
| `role_id`    | ID of the employee’s role                                         |
| `role_title` | Title of the role (e.g., Engineer, Analyst)                       |
| `role_code`  | Internal code for the employee’s role                             |
| `dept`       | Department to which the employee belongs (e.g., Finance, Sales)   |
| `event_code` | Encodes the nature of the access request event                    |
| `group`      | ID of the security group involved                                 |
| `target`     | **Label** — whether the access was approved (`1`) or denied (`0`) |

> 🧪 **Note:** The dataset is anonymized, and categorical values are encoded as integers or codes.

### ⚠️ Class Imbalance:

* Class `1` (Approved): \~94%
* Class `0` (Denied): \~6%

This imbalance makes **recall for Class 0 (denied requests)** a critical metric in model evaluation.

---





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

### 📊 Classification Report (XGBoost Model)

| Metric        | Class 0 (Denied) | Class 1 (Approved) | Macro Avg | Weighted Avg |
|---------------|------------------|--------------------|-----------|---------------|
| **Precision** | 0.78             | 0.98               | 0.88      | 0.97          |
| **Recall**    | 0.70             | 0.99               | 0.84      | 0.97          |
| **F1-score**  | 0.74             | 0.98               | 0.86      | 0.97          |
| **Support**   | 379              | 6175               | —         | 6554          |

**Overall Accuracy**: `0.9711` ✅
---

# Model Comparison

| Model                              | Class 0 Recall | Class 0 Precision | Accuracy  |
| ---------------------------------- | -------------- | ----------------- | --------- |
| Logistic Regression *(no weights)* | 0.29           | 0.63              | 94.9%     |
| Logistic Regression *(balanced)*   | 0.89           | 0.38              | 90.8%     |
| Decision Tree                      | 0.66           | 0.66              | 96.0%     |
| **XGBoost**                        | **0.70**       | **0.78**          | **97.1%** |

### 🧠 Key Insights:
- XGBoost achieved the best balance between precision and recall for the minority class, with the highest overall accuracy.

- The balanced Logistic Regression boosted recall significantly but at the cost of precision.

- Decision Tree offered a good trade-off, performing decently across all metrics with simpler interpretability.

---


## 🔧 Logistic Regression - Hyperparameter Tuning Report

We performed hyperparameter tuning on the Logistic Regression model to improve its performance on our classification task. The tuning was done using GridSearchCV with cross-validation.

### ✅ Best Parameters Found:

```json
{
  "C": 1,
  "class_weight": "balanced",
  "penalty": "l2",
  "solver": "lbfgs"
}
```

### 📈 Best Cross-Validation Score:

```
0.7443 (approx. 74.43% average accuracy)
```

### 🔍 Explanation of Parameters:

* **C = 1**: Controls regularization strength; a balanced value that prevents overfitting.
* **class\_weight = 'balanced'**: Automatically adjusts weights inversely proportional to class frequencies to handle class imbalance.
* **penalty = 'l2'**: Applies L2 regularization to simplify the model and prevent overfitting.
* **solver = 'lbfgs'**: An efficient optimization algorithm suited for small to medium-sized datasets and supports L2 penalty.

---

### 📝 Conclusion:

With these optimized parameters, the model shows improved balance and generalization, especially helpful for imbalanced datasets. This configuration is used for final evaluation on the test set.

---


## 🌳 Decision Tree - Hyperparameter Tuning Summary

We tuned a Decision Tree classifier using cross-validation to find the best-performing configuration.

### ✅ Best Parameters:

```json
{
  "class_weight": null,
  "criterion": "gini",
  "max_depth": 10,
  "min_samples_split": 5
}
```

### 🔍 Parameter Meaning (Layman Terms):

* **criterion = 'gini'**: Chooses the best questions to split the data cleanly.
* **max\_depth = 10**: Limits the tree to 10 questions deep to avoid overfitting.
* **min\_samples\_split = 5**: A split is made only if 5 or more samples are present.
* **class\_weight = None**: No class balancing applied — all classes treated equally.

---


## ⚡ XGBoost - Hyperparameter Tuning Summary

We used **RandomizedSearchCV** to optimize XGBoost hyperparameters efficiently.

### 🛠 Tuning Configuration:

* **Search Method**: `RandomizedSearchCV`
* **Candidates Tried**: 20 random hyperparameter combinations
* **Cross-Validation Folds**: 5-fold
* **Total Fits**: 20 × 5 = **100 model runs**

### 🔍 Why This Matters:

* RandomizedSearchCV helps explore a wide range of parameter combinations **faster than GridSearch**.
* 5-fold cross-validation ensures each setting is **reliably tested** on multiple slices of the data.
* This process helps find a robust and high-performing model without overfitting.

---

