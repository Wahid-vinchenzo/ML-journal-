# 📘 Master Guide: Tier 1 Evaluation Metrics
*A complete, math-to-code bridge for every essential metric you listed. Read sequentially, work through the examples, then run the code.*

---

## 🔑 FOUNDATION: The Confusion Matrix
Every classification metric is built from four numbers. Understand these deeply before moving forward.

### 📖 Definition
A 2×2 table comparing actual labels vs. predicted labels for binary classification:
| | Predicted Positive (1) | Predicted Negative (0) |
|---|---|---|
| **Actual Positive (1)** | TP (True Positive) | FN (False Negative) |
| **Actual Negative (0)** | FP (False Positive) | TN (True Negative) |

### 🧠 Intuition
- **TP**: Model correctly spotted the positive case.
- **TN**: Model correctly ignored the negative case.
- **FP**: Model cried wolf (false alarm).
- **FN**: Model missed a real positive (missed detection).

### 🔢 Worked Example
Actual: `[1,1,1,1,1, 0,0,0,0,0]` (5 pos, 5 neg)  
Predicted: `[1,1,1,0,1, 1,0,0,0,0]`
- TP = 3, FN = 2
- FP = 1, TN = 4
- Total = 10

### 💻 Python ↔ Math Mapping
```python
import numpy as np
y_true = np.array([1,1,1,1,1, 0,0,0,0,0])
y_pred = np.array([1,1,1,0,1, 1,0,0,0,0])

tp = np.sum((y_true==1) & (y_pred==1))
tn = np.sum((y_true==0) & (y_pred==0))
fp = np.sum((y_true==0) & (y_pred==1))
fn = np.sum((y_true==1) & (y_pred==0))
print(f"TP={tp}, FN={fn}, FP={fp}, TN={tn}")
```
*Connection*: Boolean masking directly implements the set intersections that define TP/TN/FP/FN.

---

## 📊 CLASSIFICATION METRICS

### 1️⃣ Accuracy
**Definition**: Proportion of correct predictions out of total.  
**Formula**:  
$$ \text{Accuracy} = \frac{TP + TN}{TP + TN + FP + FN} $$

**🧠 Intuition**: Simple "hit rate". Works well only when classes are balanced. Fails catastrophically on imbalanced data (e.g., 99% negative → always predict 0 → 99% accuracy but useless).

**🔢 Worked Example** (from confusion matrix above):  
$$ \text{Acc} = \frac{3+4}{10} = 0.70 $$

**📈 Good/Bad Values**:
- `> 0.85`: Strong (balanced data)
- `0.70–0.85`: Acceptable baseline
- `< 0.70`: Weak or imbalanced trap
- ⚠️ *Always check class balance first.*

**💻 Code**
```python
from sklearn.metrics import accuracy_score
print(accuracy_score(y_true, y_pred))  # 0.7
```

---

### 2️⃣ Precision, Recall & F1-Score
**Definitions**:
- **Precision**: Of all predicted positives, how many are truly positive?  
  $$ P = \frac{TP}{TP + FP} $$
- **Recall (Sensitivity/TPR)**: Of all actual positives, how many did we catch?  
  $$ R = \frac{TP}{TP + FN} $$
- **F1-Score**: Harmonic mean of P & R. Balances both.  
  $$ F1 = 2 \cdot \frac{P \cdot R}{P + R} $$

**🧠 Intuition**:
- High **Precision** → Few false alarms (good for spam, fraud where FP is costly).
- High **Recall** → Few misses (good for cancer screening where FN is deadly).
- **F1** penalizes extreme imbalance between P & R. We use *harmonic* mean because arithmetic mean would reward a metric of 1.0 paired with 0.0 (giving 0.5), while harmonic gives 0.

**🔢 Derivation of Harmonic Mean Property**  
Given $P, R \in [0,1]$, the harmonic mean is:
$$ H = \frac{2}{\frac{1}{P} + \frac{1}{R}} = 2\frac{PR}{P+R} $$
If $P=1, R=0 \Rightarrow H=0$. The model catches nothing → score 0. Arithmetic would give $0.5$, falsely rewarding it.

**🔢 Worked Example**  
$TP=3, FP=1, FN=2$  
$P = 3/(3+1) = 0.75$  
$R = 3/(3+2) = 0.60$  
$F1 = 2 \cdot \frac{0.75 \cdot 0.60}{0.75+0.60} = \frac{0.90}{1.35} \approx 0.667$

**📈 Good/Bad Values**:
- `> 0.85`: Excellent
- `0.70–0.85`: Good
- `< 0.70`: Weak (needs threshold tuning or better features)
- *Context matters*: Medical → prioritize Recall (`>0.90`). Email spam → prioritize Precision (`>0.90`).

**💻 Code**
```python
from sklearn.metrics import precision_score, recall_score, f1_score
print("Precision:", precision_score(y_true, y_pred))  # 0.75
print("Recall:   ", recall_score(y_true, y_pred))      # 0.60
print("F1:       ", f1_score(y_true, y_pred))          # 0.666...
```

---

### 3️⃣ AUC-ROC (Area Under Receiver Operating Characteristic Curve)
**Definition**: Probability that a randomly chosen positive instance ranks higher than a randomly chosen negative instance. Threshold-invariant.

**🧠 Intuition**: Measures *ranking quality*, not hard predictions. ROC plots TPR (y-axis) vs FPR (x-axis) while sweeping decision threshold from 1.0 → 0.0. AUC = 0.5 → random guessing. AUC = 1.0 → perfect separation.

**🔢 Math Formulation**  
- $TPR(threshold) = \frac{TP}{TP+FN}$
- $FPR(threshold) = \frac{FP}{FP+TN} = 1 - \text{Specificity}$
- $AUC = \int_{0}^{1} TPR(FPR) \, d(FPR)$  
In practice, computed via trapezoidal rule over sorted probability thresholds.

**Probabilistic Interpretation Derivation**:  
Let $S_+$ be scores for positives, $S_-$ for negatives.  
$$ AUC = P(S_+ > S_-) + 0.5 \cdot P(S_+ = S_-) $$
This comes from integrating the joint distribution over the unit square where $s_+ > s_-$.

**🔢 Worked Example (Manual)**  
True labels: `[1,0,1,0]`  
Predicted probs: `[0.8, 0.4, 0.6, 0.3]`  
Sort by prob desc:  
| Prob | Label | TPR | FPR |
|------|-------|-----|-----|
| 0.8  | 1     | 0.5 | 0.0 |
| 0.6  | 1     | 1.0 | 0.0 |
| 0.4  | 0     | 1.0 | 0.5 |
| 0.3  | 0     | 1.0 | 1.0 |

Trapezoidal areas:  
$(0.5-0.0)\cdot(0.5+1.0)/2 = 0.375$  
$(0.0-0.0)\cdot(1.0+1.0)/2 = 0$  
$(0.5-0.0)\cdot(1.0+1.0)/2 = 0.5$  
Total AUC ≈ `0.875`

**📈 Good/Bad Values**:
- `> 0.90`: Excellent
- `0.80–0.90`: Good
- `0.70–0.80`: Fair
- `0.50–0.70`: Poor
- `0.50`: Random
- ⚠️ On highly imbalanced data, AUC-ROC can look artificially optimistic. Use AUC-PR (Tier 2).

**💻 Code**
```python
from sklearn.metrics import roc_curve, roc_auc_score
y_true = np.array([1,0,1,0])
y_prob = np.array([0.8,0.4,0.6,0.3])

fpr, tpr, thresholds = roc_curve(y_true, y_prob)
print("AUC-ROC:", roc_auc_score(y_true, y_prob))  # 0.875
```

---

### 4️⃣ Log Loss (Cross-Entropy Loss)
**Definition**: Measures the quality of predicted probabilities. Heavily penalizes confident wrong predictions.

**🧠 Intuition**: If model says `p=0.99` for a negative case, log loss explodes. Forces models to output calibrated probabilities, not just hard classes.

**🔢 Math & Derivation from MLE**  
Assume Bernoulli trials. Likelihood for one sample:  
$$ L_i = p_i^{y_i} (1-p_i)^{1-y_i} $$
For $N$ samples:  
$$ L = \prod_{i=1}^N p_i^{y_i} (1-p_i)^{1-y_i} $$
Take log (monotonic, preserves max):  
$$ \ln L = \sum_{i=1}^N \left[ y_i \ln p_i + (1-y_i) \ln(1-p_i) \right] $$
Maximizing $\ln L$ ≡ minimizing negative log-likelihood. Divide by $N$ for scale-invariance:  
$$ \text{LogLoss} = -\frac{1}{N} \sum_{i=1}^N \left[ y_i \ln(p_i) + (1-y_i) \ln(1-p_i) \right] $$

**🔢 Worked Example**  
$y = [1,0,1]$, $p = [0.9, 0.2, 0.7]$  
Term1: $-1 \cdot \ln(0.9) = 0.105$  
Term2: $-(1-0) \cdot \ln(1-0.2) = -\ln(0.8) = 0.223$  
Term3: $-1 \cdot \ln(0.7) = 0.357$  
Sum = `0.685`, Avg = `0.228`

**📈 Good/Bad Values**:
- `< 0.30`: Well-calibrated, confident
- `0.30–0.60`: Acceptable
- `> 0.60`: Poor calibration or noisy data
- *Lower is always better*. 0 = perfect.

**💻 Code**
```python
from sklearn.metrics import log_loss
print("Log Loss:", log_loss([1,0,1], [0.9,0.2,0.7]))  # 0.228...
```

---

## 📉 REGRESSION METRICS

### 5️⃣ MAE (Mean Absolute Error)
**Definition**: Average absolute difference between actual and predicted.  
$$ MAE = \frac{1}{N} \sum_{i=1}^N |y_i - \hat{y}_i| $$

**🧠 Intuition**: "On average, how far off are we?" Robust to outliers. Easy to interpret in original units.

**🔢 Worked Example**  
$y = [10, 20, 30]$, $\hat{y} = [12, 18, 35]$  
Errors: `|2|, |2|, |5|` → MAE = `(2+2+5)/3 = 3.0`

**📈 Good/Bad**: Context-dependent. Compare to baseline (predict mean). `< 10%` of target range is often good.

**💻 Code**
```python
from sklearn.metrics import mean_absolute_error
print("MAE:", mean_absolute_error(y, y_hat))
```

---

### 6️⃣ RMSE (Root Mean Squared Error)
**Definition**: Square root of average squared errors.  
$$ RMSE = \sqrt{ \frac{1}{N} \sum_{i=1}^N (y_i - \hat{y}_i)^2 } $$

**🧠 Intuition**: Penalizes large errors quadratically. Use when big mistakes are costly (e.g., financial forecasting, engineering tolerances).

**🔢 Derivation from Variance**  
MSE = Variance of residuals + Bias². RMSE ≈ standard deviation of errors when model is unbiased.

**🔢 Worked Example**  
Same data: errors `2, 2, 5`  
Squared: `4, 4, 25` → Mean = `11` → RMSE = `√11 ≈ 3.32`  
Note: RMSE > MAE always (unless all errors equal).

**📈 Good/Bad**: Lower is better. Compare to MAE: if RMSE >> MAE, outliers dominate errors.

**💻 Code**
```python
from sklearn.metrics import mean_squared_error
rmse = mean_squared_error(y, y_hat, squared=False)  # sklearn >= 0.24
print("RMSE:", rmse)
```

---

### 7️⃣ R² Score (Coefficient of Determination)
**Definition**: Proportion of variance in $y$ explained by the model.  
$$ R^2 = 1 - \frac{SS_{res}}{SS_{tot}} = 1 - \frac{\sum (y_i - \hat{y}_i)^2}{\sum (y_i - \bar{y})^2} $$

**🧠 Intuition**: 
- $R^2 = 1$: Perfect fit
- $R^2 = 0$: Model predicts mean $\bar{y}$ for all inputs
- $R^2 < 0$: Model worse than predicting the mean

**🔢 Derivation (Variance Decomposition)**  
Total variation = Explained + Residual:  
$SS_{tot} = \sum(y_i-\bar{y})^2$  
$SS_{res} = \sum(y_i-\hat{y}_i)^2$  
$SS_{reg} = \sum(\hat{y}_i-\bar{y})^2$  
Under OLS: $SS_{tot} = SS_{reg} + SS_{res}$  
$\Rightarrow R^2 = SS_{reg}/SS_{tot} = 1 - SS_{res}/SS_{tot}$

**🔢 Worked Example**  
$y = [10, 20, 30]$, $\bar{y}=20$  
$SS_{tot} = (10-20)^2+(20-20)^2+(30-20)^2 = 200$  
$SS_{res} = (10-12)^2+(20-18)^2+(30-35)^2 = 4+4+25=33$  
$R^2 = 1 - 33/200 = 0.835$

**📈 Good/Bad**:
- `> 0.75`: Strong
- `0.50–0.75`: Moderate
- `< 0.50`: Weak
- `< 0`: Broken or mismatched features/target

**💻 Code**
```python
from sklearn.metrics import r2_score
print("R²:", r2_score(y, y_hat))
```

---

## ⚖️ HOW TO COMPARE MODELS & CHOOSE METRICS

### 🔍 Step-by-Step Comparison Framework
1. **Define Business Objective**: What costs more? False positives or false negatives? Large errors or small consistent errors?
2. **Select Primary Metric**: Align with objective (e.g., Recall for medical, RMSE for finance, AUC-PR for imbalanced tabular).
3. **Use Cross-Validation**: Never compare on a single train/test split. Use 5-fold CV → get mean ± std.
4. **Check Confidence Intervals**: Bootstrap or CV std tells you if difference is statistically meaningful.
5. **Secondary Metrics**: Ensure primary improvement doesn't break calibration (Log Loss) or ranking (AUC-ROC).
6. **Threshold Tuning**: For classification, optimize threshold on validation set using F1 or business cost matrix.

### 📊 Quick Decision Table
| Goal | Best Primary Metric | Backup |
|------|-------------------|--------|
| Balanced classification | Accuracy / F1 | AUC-ROC |
| Imbalanced classification | AUC-PR / MCC | F1, Log Loss |
| Costly false alarms | Precision | AUC-ROC |
| Costly misses | Recall | F1 |
| Probabilistic decisions | Log Loss / Brier Score | AUC-ROC |
| Regression (outlier-sensitive) | RMSE | R² |
| Regression (robust) | MAE | R² |
| Explained variance focus | R² | Adjusted R² (Tier 2) |

### 🧪 Statistical Comparison (Practical)
```python
from scipy import stats
# Compare two models' CV scores
model1_scores = [0.82, 0.79, 0.85, 0.80, 0.83]
model2_scores = [0.81, 0.80, 0.82, 0.83, 0.84]
t_stat, p_val = stats.ttest_rel(model1_scores, model2_scores)
print(f"p-value: {p_val:.3f}")  # p < 0.05 → significant difference
```

---

## 💻 COMPLETE PYTHON TEMPLATE (Tier 1)
```python
import numpy as np
from sklearn.metrics import (accuracy_score, precision_score, recall_score, f1_score,
                             confusion_matrix, roc_curve, roc_auc_score, log_loss,
                             mean_absolute_error, mean_squared_error, r2_score)

# === CLASSIFICATION ===
y_cls_true = np.array([1,1,1,1,1, 0,0,0,0,0])
y_cls_pred = np.array([1,1,1,0,1, 1,0,0,0,0])
y_cls_prob = np.array([0.9,0.85,0.8,0.4,0.75, 0.6,0.2,0.1,0.15,0.25])

print("=== CLASSIFICATION ===")
print("Confusion Matrix:\n", confusion_matrix(y_cls_true, y_cls_pred))
print("Accuracy:          ", accuracy_score(y_cls_true, y_cls_pred))
print("Precision:         ", precision_score(y_cls_true, y_cls_pred))
print("Recall:            ", recall_score(y_cls_true, y_cls_pred))
print("F1:                ", f1_score(y_cls_true, y_cls_pred))
print("AUC-ROC:           ", roc_auc_score(y_cls_true, y_cls_prob))
print("Log Loss:          ", log_loss(y_cls_true, y_cls_prob))

# === REGRESSION ===
y_reg_true = np.array([10.0, 20.0, 30.0, 40.0, 50.0])
y_reg_pred = np.array([12.0, 18.5, 33.0, 38.0, 49.0])

print("\n=== REGRESSION ===")
print("MAE:  ", mean_absolute_error(y_reg_true, y_reg_pred))
print("RMSE: ", mean_squared_error(y_reg_true, y_reg_pred, squared=False))
print("R²:   ", r2_score(y_reg_true, y_reg_pred))
```

**🔗 Math ↔ Code Mapping Summary**:
- `confusion_matrix` → set intersections for TP/TN/FP/FN
- `accuracy_score` → $(TP+TN)/N$
- `precision_score` → $TP/(TP+FP)$
- `recall_score` → $TP/(TP+FN)$
- `f1_score` → $2PR/(P+R)$
- `roc_auc_score` → trapezoidal integration of TPR vs FPR curve
- `log_loss` → $-\frac{1}{N}\sum [y\log p + (1-y)\log(1-p)]$
- `mean_absolute_error` → $\frac{1}{N}\sum |y-\hat{y}|$
- `mean_squared_error` → $\sqrt{\frac{1}{N}\sum (y-\hat{y})^2}$
- `r2_score` → $1 - SS_{res}/SS_{tot}$

---

## 🎓 HOW TO USE THIS GUIDE
1. **Day 1-2**: Build confusion matrix manually. Compute P, R, F1, Accuracy on paper. Run code. Verify match.
2. **Day 3-4**: Generate probabilities. Sweep thresholds. Plot ROC manually (3 points). Compare with `roc_curve`. Compute Log Loss for 3 samples.
3. **Day 5**: Compute MAE, RMSE, R² on a small dataset. Observe how outlier changes RMSE vs MAE.
4. **Day 6-7**: Cross-validate two models. Compare metrics. Use `ttest_rel` to check significance. Decide winner based on business goal.

---

