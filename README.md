# 🧠 Airbnb Price Prediction – Model Report & Analysis

---

## 🧾 Business-Driven EDA (Company Questions)

As part of an initial **data analysis task**, I answered key company-level questions using EDA:

- ✅ What is the distribution of price and reviews?
- ✅ Which room types are most popular?
- ✅ What factors influence minimum nights and availability?
- ✅ How are listings distributed across neighbourhoods?
- ✅ Are instant bookings or verified hosts more common?

> 📊 These questions helped shape a **business-first understanding** of the dataset.

---

## 🔬 Deep Exploratory Data Analysis (EDA)

After answering the business questions, I proceeded with **deeper technical EDA** to prepare for modeling.

- **Distributions:** Visualized histograms and boxplots of `price`, `minimum nights`, `reviews`, etc.
- **Categorical Analysis:** Used countplots and boxplots on `room type`, `cancellation policy`, `neighbourhood group`, etc.
- **Scatter Plots:** Examined `price` vs key numerical features.
- **Correlation Heatmap:** Helped identify feature relationships and reveal suspiciously strong links.

---

## 🚨 Target Leakage Warning (Critical)

### 🔍 Summary:
During model building, a serious case of **target leakage** was identified:

- Feature **`service fee`** had an **extremely high correlation** with `price` (≈ 0.998).
- The model initially achieved **R² ≈ 0.99**, which was too good to be true.
- Removing `service fee` caused R² to drop to near zero → confirming the **leakage**.

### ⚠️ Why It's a Problem:
- `service fee` is calculated **from** the target (`price`) → it's **not allowed** in real ML pipelines.
- Using it leads to **inflated performance**, **invalid models**, and **false expectations**.

### 📌 Final Decision:
> 🚫 **Modeling is halted here** due to target leakage.  
> ✅ However, all steps until this point (EDA, prep, insights) are still **valuable and reusable** for future clean datasets.

---

## 🧹 Preprocessing Summary

- Outlier removal with IQR.
- Missing value imputation.
- Label encoding on categorical columns.
- StandardScaler applied to numeric columns.
- Datetime parsing & feature engineering on `last review`.

---

## 🤖 Modeling Attempt (Linear Regression)

- Used `train_test_split` and trained a linear regression model.
- Detected data leakage through suspiciously high R² score.
- Removed the leaky column → R² dropped → **confirmed leakage**.
- **No further models were developed** to avoid misleading results.

---

## 📚 Learning & Future Precaution

### What I Learned:
- Always check **correlation matrix early** in the modeling phase.
- Be cautious of **derived business features** that may leak the target.
- Very high scores (R² ≈ 1.0) are often a **red flag**, not a success.

### How I’ll Avoid This Next Time:
- Always inspect `.corr(numeric_only=True)` on `X` vs `y`.
- Ask yourself: _Can this feature exist without knowing the target?_
- Leverage both **domain understanding** and **statistical validation**.

---

## 📦 Final Note

> ❗ This project is not meant for deployment.  
> 🧠 However, it serves as an excellent **case study in EDA, preprocessing, and real-world ML pitfalls** like target leakage.  
> The full pipeline (except modeling) is **reusable** and can support cleaner Airbnb datasets.
