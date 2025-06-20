# 🏠 Housing-Price Prediction ― 26 US Cities

| | |
|---|---|
| **Instances** | 339 651 |
| **Attributes** | 11 (incl. target) |
| **Size** | 24 MB CSV |
| **Task** | Supervised regression |
| **Missing values** | Yes (must be handled) |
| **Target** | `price` (float) |

---

## 1.  Dataset snapshot

| Name | Description | Type |
|------|-------------|------|
| `date` | Timestamp of record | str *(parsed → datetime)* |
| `location` | City / district | str |
| `type` | House type | str |
| `block` | Block number | str |
| `street` | Street name | str |
| `storey_range` | Storey band | str |
| `area_sqm` | Size of house | float |
| `flat_model` | Vintage code (A … K) | str |
| `commence_date` | Year licensed | int |
| `Quality_Index` | Air-quality score | int |
| `price` | **Target** — price of house | float |

<details>
<summary>Why this dataset?</summary>

* Large enough to need efficient pipelines (339 k rows).  
* Contains realistic quirks: missing values, irrelevant columns, high-cardinality categoricals.  
* Evaluation focuses on *generalisation* — the test split is a random 20 %.
</details>

---

## 2.  Quick results

| Model | Features used | Train R² | Test R² | Train RMSE | Test RMSE |
|-------|---------------|:-------:|:------:|-----------:|----------:|
| Linear Reg. | `area_sqm`, `commence_date` | 0.481 | 0.475 | 80 778 | 81 119 |
| Linear Reg. | **All** | 0.685 | 0.679 | 62 960 | 63 784 |
| Decision Tree | **All** | **0.999** | 0.895 | **2 262** | 36 315 |
| CatBoost | **All** | 0.987 | **0.979** | 12 832 | **16 214** |
| Neural Net | `area_sqm`, `commence_date` | 0.502 | 0.496 | 79 135 | 79 538 |
| Neural Net | **All** | 0.705 | 0.679 | 60 885 | 63 736 |

**Best test performance:** <br>
CatBoost regressor (RMSE ≈ \$16 k, R² ≈ 0.979) strikes the best balance of accuracy and generalisation.  
Decision Trees memorise the training data (R² ≈ 1.0) but generalise less stably.

> **Metric definitions**  
> *RMSE* = √MSE, in dollars.  
> *R²* = coefficient of determination (1 = perfect).

---

