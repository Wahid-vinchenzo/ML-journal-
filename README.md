

# 📊 **COMPREHENSIVE EVALUATION METRICS GUIDE**
## For ML/DL Researchers & Engineers

---

## **1️⃣ CLASSIFICATION METRICS**

### **Binary Classification**
✅ **Accuracy** = (TP+TN)/(TP+TN+FP+FN)  
✅ **Precision** = TP/(TP+FP)  
✅ **Recall/Sensitivity/TPR** = TP/(TP+FN)  
✅ **Specificity/TNR** = TN/(TN+FP)  
✅ **F1-Score** = 2×(Precision×Recall)/(Precision+Recall)  
✅ **Fβ-Score** (F2, F0.5 for weighted precision/recall)  
✅ **Log Loss/Binary Cross-Entropy**  
✅ **AUC-ROC** (Area Under ROC Curve)  
✅ **AUC-PR** (Area Under Precision-Recall Curve) *Critical for imbalanced data*  
✅ **MCC** (Matthews Correlation Coefficient) *Best for imbalanced*  
✅ **Cohen's Kappa** *Accounts for random chance*  
✅ **Balanced Accuracy** = (Sensitivity+Specificity)/2  
✅ **Youden's J Index** = Sensitivity + Specificity - 1  
✅ **False Positive Rate (FPR)** = FP/(FP+TN)  
✅ **False Negative Rate (FNR)** = FN/(FN+TP)  
✅ **False Discovery Rate (FDR)** = FP/(TP+FP)  
✅ **Negative Predictive Value (NPV)** = TN/(TN+FN)  

---

### **Multi-Class Classification**
✅ **Macro-Averaged Metrics** (equal weight to each class)  
✅ **Micro-Averaged Metrics** (equal weight to each instance)  
✅ **Weighted-Averaged Metrics** (weight by class support)  
✅ **Confusion Matrix** (n×n)  
✅ **Per-Class Precision/Recall/F1**  
✅ **Top-K Accuracy** (Top-3, Top-5)  
✅ **Hamming Loss**  
✅ **Jaccard Index/Similarity**  
✅ **Multiclass Log Loss**  
✅ **One-vs-Rest (OvR) AUC**  
✅ **One-vs-One (OvO) AUC**  

---

## **2️⃣ REGRESSION METRICS**

✅ **MAE** (Mean Absolute Error)  
✅ **MSE** (Mean Squared Error)  
✅ **RMSE** (Root Mean Squared Error)  
✅ **RMSLE** (Root Mean Squared Log Error) *For skewed targets*  
✅ **R² Score** (Coefficient of Determination)  
✅ **Adjusted R²** (Penalizes adding features)  
✅ **MAPE** (Mean Absolute Percentage Error)  
✅ **SMAPE** (Symmetric MAPE)  
✅ **MPE** (Mean Percentage Error)  
✅ **MedAE** (Median Absolute Error) *Robust to outliers*  
✅ **Max Error** (Worst case)  
✅ **Explained Variance Score**  
✅ **Poisson Deviance** *For count data*  
✅ **Gamma Deviance** *For positive continuous*  
✅ **Tweedie Deviance** *For compound Poisson*  
✅ **Concordance Correlation Coefficient (CCC)**  
✅ **Pearson Correlation Coefficient**  
✅ **Spearman Rank Correlation**  

---

## **3️⃣ RANKING METRICS**

✅ **AUC-ROC**  
✅ **AUC-PR**  
✅ **NDCG** (Normalized Discounted Cumulative Gain)  
✅ **DCG** (Discounted Cumulative Gain)  
✅ **MRR** (Mean Reciprocal Rank)  
✅ **MAP** (Mean Average Precision)  
✅ **Hit Rate@K**  
✅ **Precision@K**  
✅ **Recall@K**  
✅ **F1@K**  
✅ **NDCG@K**  
✅ **Normalized DCG**  
✅ **Kendall's Tau** *Rank correlation*  
✅ **Spearman's Rho**  
✅ **Expected Reciprocal Rank (ERR)**  
✅ **Gini Coefficient** = 2×AUC - 1  

---

## **4️⃣ OBJECT DETECTION METRICS**

✅ **IoU** (Intersection over Union)  
✅ **mAP** (mean Average Precision)  
✅ **mAP@0.5** (IoU threshold 0.5)  
✅ **mAP@0.5:0.95** (COCO standard)  
✅ **mAP@0.75** (Strict)  
✅ **AP per class**  
✅ **Precision-Recall Curve**  
✅ **F1-Score at IoU threshold**  
✅ **AR** (Average Recall)  
✅ **AR@1, AR@10, AR@100** (Max detections)  
✅ **AR_small, AR_medium, AR_large** (By object size)  
✅ **False Positives Per Image (FPPI)**  
✅ **Miss Rate**  
✅ **Jaccard Index**  

---

## **5️⃣ SEGMENTATION METRICS**

### **Semantic Segmentation**
✅ **Pixel Accuracy**  
✅ **Mean Pixel Accuracy**  
✅ **mIoU** (mean Intersection over Union)  
✅ **Frequency Weighted IoU**  
✅ **Dice Coefficient/F1-Score** = 2×|A∩B|/(|A|+|B|)  
✅ **Jaccard Index/IoU** = |A∩B|/|A∪B|  
✅ **Precision/Recall per class**  
✅ **Boundary F1 (BF1)** *Boundary accuracy*  
✅ **Hausdorff Distance** *Max boundary distance*  
✅ **Average Surface Distance (ASD)**  
✅ **Volumetric Overlap Error (VOE)**  
✅ **Relative Volume Difference (RVD)**  

### **Instance Segmentation**
✅ **mAP@IoU thresholds** (COCO style)  
✅ **PQ** (PQ, SQ, RQ) *Panoptic Quality*  
✅ **AP for boundaries**  

---

## **6️⃣ CLUSTERING METRICS**

### **Supervised (with labels)**
✅ **Adjusted Rand Index (ARI)**  
✅ **Normalized Mutual Information (NMI)**  
✅ **Fowlkes-Mallows Index**  
✅ **Homogeneity Score**  
✅ **Completeness Score**  
✅ **V-Measure**  
✅ **Adjusted Mutual Information (AMI)**  

### **Unsupervised (no labels)**
✅ **Silhouette Coefficient** [-1, 1]  
✅ **Calinski-Harabasz Index** (Higher is better)  
✅ **Davies-Bouldin Index** (Lower is better)  
✅ **Dunn Index**  
✅ **Inertia/Within-Cluster Sum of Squares**  
✅ **Elbow Method**  
✅ **Gap Statistic**  
✅ **Bayesian Information Criterion (BIC)**  
✅ **Akaike Information Criterion (AIC)**  

---

## **7️⃣ NLP & TEXT GENERATION METRICS**

### **Machine Translation**
✅ **BLEU** (Bilingual Evaluation Understudy)  
✅ **BLEU-1, BLEU-2, BLEU-3, BLEU-4**  
✅ **METEOR** (Metric for Evaluation of Translation)  
✅ **TER** (Translation Edit Rate)  
✅ **WMT Metrics**  
✅ **chrF** (character n-gram F-score)  

### **Text Summarization**
✅ **ROUGE-N** (Recall-Oriented Understudy)  
✅ **ROUGE-1, ROUGE-2, ROUGE-L**  
✅ **ROUGE-W** (Weighted)  
✅ **ROUGE-S** (Skip-bigram)  
✅ **BERTScore**  
✅ **MoverScore**  

### **Question Answering**
✅ **Exact Match (EM)**  
✅ **F1-Score** (token-level overlap)  
✅ **BLEU**  
✅ **ROUGE-L**  
✅ **SQuAD Metrics**  
✅ **MRR** (Mean Reciprocal Rank)  

### **Text Classification**
✅ **All classification metrics** (Section 1)  
✅ **Perplexity** *For language models*  

### **Language Modeling**
✅ **Perplexity** (Lower is better)  
✅ **Cross-Entropy Loss**  
✅ **Bits per Character (BPC)**  

### **Dialogue Systems**
✅ **BLEU/ROUGE**  
✅ **Embedding-based metrics** (Embedding Average, Vector Extrema)  
✅ **Distinct-n** (Diversity)  
✅ **Coherence Score**  
✅ **Engagement metrics**  

### **Semantic Similarity**
✅ **Cosine Similarity**  
✅ **Pearson/Spearman Correlation**  
✅ **STS Benchmark Metrics**  

---

## **8️⃣ RECOMMENDATION SYSTEM METRICS**

### **Rating Prediction**
✅ **RMSE**  
✅ **MAE**  
✅ **R²**  

### **Ranking/Top-K Recommendation**
✅ **Precision@K**  
✅ **Recall@K**  
✅ **F1@K**  
✅ **NDCG@K**  
✅ **MAP@K**  
✅ **MRR**  
✅ **Hit Rate@K**  
✅ **Coverage** (Catalog coverage)  
✅ **Diversity** (Intra-list diversity)  
✅ **Novelty**  
✅ **Serendipity**  
✅ **AUC**  
✅ **Mean Reciprocal Rank (MRR)**  

### **Beyond Accuracy**
✅ **Calibration**  
✅ **Fairness metrics**  
✅ **Cold-start performance**  

---

## **9️⃣ TIME SERIES FORECASTING METRICS**

✅ **MAE**  
✅ **MSE/RMSE**  
✅ **MAPE**  
✅ **SMAPE**  
✅ **MASE** (Mean Absolute Scaled Error) *Best for comparison*  
✅ **RMSSE** (Root Mean Squared Scaled Error)  
✅ **Quantile Loss** *For probabilistic forecasting*  
✅ **Pinball Loss**  
✅ **Coverage Probability**  
✅ **Interval Score**  
✅ **CRPS** (Continuous Ranked Probability Score)  
✅ **Theil's U Statistic**  
✅ **Directional Accuracy**  
✅ **Turning Point Accuracy**  

---

## **🔟 GAN & GENERATIVE MODEL METRICS**

✅ **Inception Score (IS)** *Higher is better*  
✅ **Fréchet Inception Distance (FID)** *Lower is better*  
✅ **Kernel Inception Distance (KID)**  
✅ **Precision & Recall for GANs**  
✅ **Mode Coverage**  
✅ **MS-SSIM** (Multi-Scale SSIM) *Diversity*  
✅ **LPIPS** (Learned Perceptual Image Patch Similarity)  
✅ **Perceptual Path Length (PPL)**  
✅ **Detection Score**  
✅ **1-NN Classifier Accuracy**  

---

## **1️⃣1️⃣ FAIRNESS & BIAS METRICS**

### **Group Fairness**
✅ **Demographic Parity**  
✅ **Equalized Odds**  
✅ **Equal Opportunity**  
✅ **Predictive Parity**  
✅ **Calibration by Group**  
✅ **Disparate Impact** = P(Ŷ=1|A=0)/P(Ŷ=1|A=1)  
✅ **Statistical Parity Difference**  

### **Individual Fairness**
✅ **Individual Fairness**  
✅ **Counterfactual Fairness**  

### **Bias Metrics**
✅ **True Positive Rate Difference**  
✅ **False Positive Rate Difference**  
✅ **True Negative Rate Difference**  
✅ **False Negative Rate Difference**  
✅ **Precision Difference**  
✅ **FPR Ratio**  
✅ **FNR Ratio**  
✅ **Theil Index**  
✅ **Generalized Entropy Index**  

---

## **1️⃣2️⃣ CALIBRATION METRICS**

✅ **Brier Score** = Mean squared difference between predicted prob and actual  
✅ **Expected Calibration Error (ECE)**  
✅ **Maximum Calibration Error (MCE)**  
✅ **Adaptive Calibration Error (ACE)**  
✅ **Test Calibration Error (TCE)**  
✅ **Reliability Diagrams**  
✅ **Calibration Curve**  
✅ **Log Loss**  
✅ **Sharpness**  

---

## **1️⃣3️⃣ UNCERTAINTY QUANTIFICATION**

✅ **Predictive Variance**  
✅ **Entropy**  
✅ **Mutual Information**  
✅ **Expected Calibration Error**  
✅ **Coverage Probability**  
✅ **Prediction Interval Width**  
✅ **Sharpness**  
✅ **NLL** (Negative Log Likelihood)  
✅ **CRPS**  

---

## **1️⃣4️⃣ MODEL EFFICIENCY & DEPLOYMENT METRICS**

### **Computational**
✅ **FLOPs** (Floating Point Operations)  
✅ **MACs** (Multiply-Accumulate Operations)  
✅ **Inference Time/Latency**  
✅ **Throughput** (samples/sec)  
✅ **Training Time**  
✅ **Time to Convergence**  

### **Memory**
✅ **Model Size** (MB/GB)  
✅ **Number of Parameters**  
✅ **Peak Memory Usage**  
✅ **GPU Memory Footprint**  
✅ **RAM Usage**  

### **Energy**
✅ **Energy Consumption** (Joules)  
✅ **Carbon Footprint**  
✅ **Power Draw** (Watts)  

### **Compression**
✅ **Compression Ratio**  
✅ **Pruning Ratio**  
✅ **Quantization Bits**  

---

## **1️⃣5️⃣ ROBUSTNESS & RELIABILITY METRICS**

✅ **Adversarial Robustness**  
✅ **Accuracy under Noise**  
✅ **Accuracy under Distribution Shift**  
✅ **Out-of-Distribution Detection**  
✅ **AUROC for OOD**  
✅ **FPR@95TPR**  
✅ **Stability Score**  
✅ **Vulnerability Score**  
✅ **Certified Robustness**  

---

## **1️⃣6️⃣ ANOMALY DETECTION METRICS**

✅ **Precision@K**  
✅ **Recall@K**  
✅ **F1-Score@K**  
✅ **AUC-ROC**  
✅ **AUC-PR**  
✅ **Average Precision (AP)**  
✅ **Rank at K**  
✅ **NDCG**  
✅ **False Positive Rate at given Recall**  

---

## **1️⃣7️ SURVIVAL ANALYSIS METRICS**

✅ **Concordance Index (C-index)**  
✅ **Integrated Brier Score (IBS)**  
✅ **Time-Dependent AUC**  
✅ **Log-Rank Test p-value**  
✅ **Hazard Ratio**  

---

## **1️⃣8️ MULTI-TASK LEARNING METRICS**

✅ **Task-wise Performance**  
✅ **Average Performance across tasks**  
✅ **Task Affinity**  
✅ **Transfer Gain**  
✅ **Negative Transfer**  
✅ **Task Gradient Angle**  

---

## **1️⃣9️⃣ META-LEARNING & FEW-SHOT METRICS**

✅ **Accuracy on Novel Classes**  
✅ **Base to Novel Generalization Gap**  
✅ **Shot-wise Performance** (1-shot, 5-shot, etc.)  
✅ **Cross-Domain Performance**  
✅ **Adaptation Speed**  

---

## **2️⃣0️ REINFORCEMENT LEARNING METRICS**

✅ **Cumulative Reward**  
✅ **Average Return**  
✅ **Discounted Return**  
✅ **Sample Efficiency**  
✅ **Time to Convergence**  
✅ **Success Rate**  
✅ **Regret**  
✅ **Policy Divergence**  
✅ **Exploration Metrics**  
✅ **Value Function Error**  

---

## **🎯 CRITICAL METRICS BY USE CASE**

### **Medical Diagnosis**
- **Sensitivity/Recall** (Don't miss positive cases)
- **Specificity**
- **AUC-PR** (Imbalanced data)
- **F1-Score**
- **Calibration**

### **Fraud Detection**
- **Precision** (Minimize false alarms)
- **Recall**
- **AUC-PR**
- **F2-Score** (Weight recall more)
- **Cost-sensitive metrics**

### **Search/Ranking**
- **NDCG@K**
- **MAP**
- **MRR**
- **Precision@K**

### **Autonomous Vehicles**
- **mAP@0.5:0.95**
- **IoU**
- **False Negative Rate** (Safety critical)
- **Latency** (Real-time)

### **Customer Churn**
- **Recall** (Find all churning customers)
- **Precision**
- **AUC-ROC**
- **Lift Chart**
- **Gain Chart**

---

## **📚 MUST-KNOW STATISTICAL TESTS**

✅ **t-test** (Compare two models)  
✅ **ANOVA** (Compare multiple models)  
✅ **McNemar's Test** (Paired classification)  
✅ **Wilcoxon Signed-Rank Test**  
✅ **Mann-Whitney U Test**  
✅ **Chi-Square Test**  
✅ **Fisher's Exact Test**  
✅ **Bootstrap Confidence Intervals**  
✅ **Permutation Test**  

---

## **✅ ESSENTIAL CHECKLIST FOR RESEARCH PAPERS**

1. **Report multiple metrics** (Never just accuracy)
2. **Include confidence intervals**
3. **Statistical significance testing**
4. **Ablation studies**
5. **Cross-validation results**
6. **Standard deviation/variance**
7. **Comparison with baselines**
8. **Runtime/memory metrics**
9. **Failure case analysis**
10. **Limitations discussion**

---

## **🔥 TOP 20 MUST-KNOW METRICS (Priority)**

1. **Accuracy** (Baseline)
2. **Precision/Recall/F1** (Classification)
3. **AUC-ROC** (Ranking ability)
4. **AUC-PR** (Imbalanced data)
5. **Log Loss** (Probability calibration)
6. **MAE/RMSE** (Regression)
7. **R² Score** (Regression fit)
8. **mAP** (Detection/Segmentation)
9. **IoU** (Overlap)
10. **BLEU/ROUGE** (NLP)
11. **NDCG** (Ranking)
12. **Silhouette Score** (Clustering)
13. **Perplexity** (Language models)
14. **FID** (Generative models)
15. **Brier Score** (Calibration)
16. **ECE** (Calibration error)
17. **MASE** (Time series)
18. **C-index** (Survival)
19. **Inference Time** (Deployment)
20. **Model Size** (Deployment)

---
