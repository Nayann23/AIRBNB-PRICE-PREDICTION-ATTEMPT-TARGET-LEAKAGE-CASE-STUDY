# 🧠 Airbnb Price Prediction – Model Report & Analysis

---

## 🚨 Target Leakage Warning (Critical)

### 🔍 Summary:
A serious case of **target leakage** was discovered during model development.

- Feature **`service fee`** was found to have an **extremely high correlation** with the target `price` (`corr ≈ 0.998`).
- This leakage led to an **unrealistically high R² (~0.99)**.
- Removing this feature brought R² down to ~0.0, confirming the leakage.
  
### ⚠️ Why It's a Problem:
- `service fee` is **calculated using price**, making it **inappropriate** for training.
- Using this feature leads to **data leakage**, **inflated performance**, and **unreliable models** in real-world applications.

### 📌 Final Decision:
> 🚫 **This project is halted at model evaluation stage** due to confirmed leakage.  
> ✅ All steps until this point are still **valid, insightful, and reusable** for similar datasets.

---

## 🔬 Deep Exploratory Data Analysis (EDA)

We performed detailed EDA to understand the dataset:

- **Distributions:** Visualized histograms and boxplots of `price`, `minimum nights`, `reviews`, etc.
- **Categorical Analysis:** Used countplots and boxplots on `room type`, `cancellation policy`, `neighbourhood group`, etc.
- **Scatter Plots:** Examined `price` vs key numerical features.
- **Correlation Heatmap:** Helped identify feature relationships.

---

## 🧹 Preprocessing

Performed comprehensive data preparation:

- **Outlier Removal** using IQR on `minimum nights`, `reviews per month`, etc.
- **Label Encoding** on categorical features.
- **Feature Scaling** using StandardScaler on numeric columns.
- **Datetime Handling:** Parsed `last review`, computed `days_since_last_review`.

---

## 🤖 Modeling (Linear Regression)

- Trained a **linear regression model** using `train_test_split`.
- Initially achieved **R² = 0.99**, which raised red flags.
- Identified and removed `service fee` (leaky feature).
- Post-removal R² dropped to near zero → confirming leakage.

---

## 📚 Learning & Future Precaution

### What We Learned:
- **Always inspect correlations** between features and the target early.
- Watch for **business-derived features** that indirectly encode the target.
- **Don’t trust very high performance scores blindly** — validate them logically.

### How to Avoid This Next Time:
- Run `.corr()` on features vs target before modeling.
- Ask: "Could this feature be derived from or influenced by the target?"
- Use **domain knowledge + statistical checks** to catch such issues early.

---

## 📦 Final Note

> ❗This model should **not** be deployed.  
> 🧠 However, the **EDA, preprocessing pipeline, and insights remain extremely valuable** and can be reused on clean datasets without leakage.

