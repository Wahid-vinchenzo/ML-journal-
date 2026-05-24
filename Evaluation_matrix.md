## 🚨 **TIER 1: ABSOLUTE ESSENTIALS**
*এগুলো ছাড়া কোনো মডেল ইভালুয়েট করা অসম্ভব।*

### **Classification-এর জন্য:**
1. ✅ **Accuracy** (বেসলাইন)
2. ✅ **Precision, Recall, F1-Score** (Imbalanced data-র জন্য life-saving)
3. ✅ **Confusion Matrix** (ভুলগুলো কোথায় হচ্ছে তা বোঝার জন্য)
4. ✅ **AUC-ROC** (মডেলের ranking ability বোঝার জন্য)
5. ✅ **Log Loss** (Probability calibration বোঝার জন্য)

### **Regression-এর জন্য:**
6. ✅ **MAE** (Mean Absolute Error) - সহজ ব্যাখ্যা
7. ✅ **RMSE** (Root Mean Squared Error) - বড় ভুলগুলো ধরার জন্য
8. ✅ **R² Score** (Model fit কতটুকু ভালো)

---

## ⚠️ **TIER 2: HIGH PRIORITY (১ সপ্তাহের মধ্যে শিখতে হবে)**
*আপনার ৩টি ডেটা টাইপের জন্য স্পেসিফিক:*

### **Tabular Data-এর জন্য:**
- ✅ **AUC-PR** (Precision-Recall AUC) - *Imbalanced tabular data-র জন্য AUC-ROC-এর চেয়েও ভালো*
- ✅ **MCC** (Matthews Correlation Coefficient) - *Imbalanced ডেটাতে সবচেয়ে নির্ভরযোগ্য*
- ✅ **Calibration Curve / Brier Score** - *Probability prediction সঠিক কিনা*

### **NLP Classification-এর জন্য:**
- ✅ **F1-Score (Macro/Weighted)** - *Multi-class NLP-র জন্য*
- ✅ **Exact Match** (যদি text generation হয়)
- ✅ **BLEU/ROUGE** (যদি summarization/translation হয়)

### **Image Classification-এর জন্য:**
- ✅ **Top-1 Accuracy & Top-5 Accuracy**
- ✅ **Per-class Precision/Recall** (কোন class-এ মডেল fail করছে)
- ✅ **IoU** (যদি object detection/segmentation করেন)

### **Regression-এর জন্য (Advanced):**
- ✅ **MAPE** (Percentage error বোঝার জন্য business-এ খুব দরকারি)
- ✅ **Adjusted R²** (Multiple features থাকলে)
- ✅ **Residual Analysis** (Plot দেখে ভুল বোঝা)

---

## 📊 **TIER 3: MEDIUM PRIORITY (১ মাসের মধ্যে)**
*Research paper-এ ভালো দেখাতে এবং production-এ:*

1. **Cohen's Kappa** (Inter-rater agreement)
2. **Balanced Accuracy** (Imbalanced data)
3. **Specificity** (Medical/Fraud detection-এ দরকার)
4. **NDCG / MAP** (যদি ranking-related কাজ করেন)
5. **Silhouette Score** (যদি clustering করেন)
6. **Perplexity** (যদি Language Model নিয়ে কাজ করেন)

---

## 🎯 **আপনার জন্য Quick Decision Matrix:**

| ডেটা টাইপ | Classification | Regression |
|------------|---------------|------------|
| **Tabular** | Accuracy, F1, AUC-ROC, **AUC-PR**, MCC | MAE, RMSE, R², MAPE |
| **NLP** | F1 (Macro), Precision, Recall, BLEU/ROUGE | MAE, RMSE (যদি score predict করেন) |
| **Image** | Accuracy, Top-5 Acc, Per-class F1, IoU | MAE, RMSE (যদি age/price predict করেন) |

---

## ✅ **আজ থেকে শুরু করার Plan:**

### **Day 1-3:**
- Accuracy, Precision, Recall, F1-Score (formula + interpretation)
- Confusion Matrix পড়া শেখা

### **Day 4-7:**
- AUC-ROC vs AUC-PR (কখন কোনটা use করবেন)
- Log Loss

### **Week 2:**
- MAE, RMSE, R² (Regression)
- MAPE

### **Week 3:**
- MCC, Balanced Accuracy (Imbalanced data)
- Multi-class metrics (Macro vs Micro vs Weighted)

---

## 💡 **Pro Tips:**

1. **Tabular Data:** Imbalanced হলে **AUC-PR** এবং **MCC** ছাড়া কিছু trust করবেন না।
2. **NLP:** শুধু Accuracy দেখবেন না, **F1-Score (Macro)** দেখুন।
3. **Image:** **Top-5 Accuracy** দেখা জরুরি যদি classes অনেকগুলো হয়।
4. **Regression:** **RMSE** এবং **MAE** দুটোই দেখুন (RMSE বড় error ধরে, MAE গড় error)।
5. **Production-এ:** অবশ্যই **Calibration** (Brier Score) check করবেন probability prediction-এর জন্য।

---

**সারকথা:** প্রথমে **Tier 1**-এর ৮টি মেট্রিক্স পুরোপুরি আয়ত্ত করুন। তারপর আপনার ডেটা টাইপ অনুযায়ী **Tier 2** শিখুন। বাকিগুলো যখন দরকার পড়বে তখন শিখলেই হবে।
