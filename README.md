# 4_ACTIVITY_1
— Improving CNN Performance Using Regularization, Fine-Tuning, and  Advanced Evaluation

## 🔗 Links
# Google Colab Link: https://colab.research.google.com/drive/1TVqiCLlhnGw0mZFCeKo15R2HYWbh3lC4#scrollTo=QAit3_kKgb5R&uniqifier=1
# Google Drive Link: https://drive.google.com/drive/folders/1JEXebpRXK43gujSRPkj9BaSxLtUv93pb?usp=drive_link
# Github Repo Link: https://github.com/zhairamilan/4_ACTIVITY_1


**Learning Outcomes**

*By the end of this activity, students will be able to:*
1. Analyze weaknesses from evaluation metrics (Precision, Recall, F1, Confusion Matrix)
2. Apply techniques to improve model generalization
3. Modify CNN architecture for better performance
4. Compare baseline vs improved model results
5. Justify improvements using quantitative and visual evidence


##  PART 1 & 3: Advanced Evaluation & Comparative Results
This phase evaluates the transition from the Laboratory 3 baseline to the optimized Laboratory 4 architecture. We utilized Precision, Recall, F1-Score, and AUC to measure success beyond simple accuracy.

### **Performance Comparison Table**
| Metric | Baseline Model (Lab 3) | Improved Model (Lab 4) | Target Range |
| :--- | :---: | :---: | :---: |
| **Training Accuracy** | [N/A (not explicitly captured)	]% | [0.4301]% | 90% – 97% |
| **Validation Accuracy** | [0.6300]% | [0.5046]% | 85% – 93% |
| **Training Loss** | [X.XX] | [X.XX] | 0.1 – 0.3 |
| **Validation Loss** | [X.XX] | [X.XX] | 0.2 – 0.5 |
| **Overall AUC Score** | [0.9076	] | [0.8188] | > 0.90 |
| **F1-Score (Avg)** | [0.6145	] | [0.4989] | > 0.85 |


## 📝 Guide Questions: Student Reflection

### **A. Model Evaluation Analysis**
1. **Weakest-performing classes:** Based on the classification report for the Improved Model, the class '10_epipremnum_variegated' performed the weakest, showing 0.00 precision, recall, and F1-score. This indicates the model completely failed to correctly classify any instances of this class.
2. **Metric Variance:** The precision, recall, and F1-score varied significantly across classes for both models. For the improved model, some classes like '20_golden_melonii' had high precision (0.96) and '12_bipinnatifidum' had very high recall (0.90), leading to good F1-scores. However, many classes showed low scores, indicating the model struggled with specific categories. For example, '10_epipremnum_variegated' had 0.00 for all three metrics, and '3_brasil' had very low recall (0.12).
3. **Low Recall Meaning:**  A low recall indicates that the model is failing to identify a significant portion of the actual positive cases for that particular class. In other words, it means the model is producing a lot of false negatives for that class. For instance, if '3_brasil' has a recall of 0.12, it means the model only correctly identified 12% of all actual '3_brasil' instances, missing the other 88%.
4. **AUC vs. Accuracy:** Accuracy provides a general sense of how well the model classifies all instances correctly (total correct predictions / total predictions). It's straightforward but can be misleading in imbalanced datasets where a model might achieve high accuracy by simply predicting the majority class. AUC (Area Under the Receiver Operating Characteristic Curve) reflects the model's ability to distinguish between classes across all possible classification thresholds. A higher AUC (closer to 1) means the model is better at separating positive and negative classes. It's less sensitive to class imbalance than accuracy. For multi-class classification, as we have, the 'OvR' (One-vs-Rest) AUC score is an average measure of how well the model discriminates each class against all others. In our case, the AUC score (Baseline: 0.9076, Improved: 0.8188) is a more robust indicator of the model's overall discriminative power compared to accuracy (Baseline: 0.6300, Improved: 0.5046), especially as we have multiple classes.
---
### **B. Model Improvement**
5. **Data Augmentation Effect:** While data augmentation is generally expected to improve generalization and validation accuracy by providing more diverse training data, in our case, the validation accuracy actually decreased from 0.6300 (Baseline) to 0.5046 (Improved Model with augmentation and other changes). This suggests that either the augmentation parameters were too aggressive for this dataset, or other changes in the 'improved' model's architecture or training regimen negatively impacted its performance, overshadowing any potential benefits from augmentation.
6. **Batch Normalization Importance:** Stabilizes learning: It normalizes the inputs to layers, reducing the problem of 'internal covariate shift' where the distribution of layer inputs changes during training. This allows for higher learning rates and faster training. Regularizes the model: It adds a slight regularization effect, which can sometimes reduce the need for Dropout. Reduces sensitivity to initial weights: It makes the network less dependent on the initial parameter values. What role did Dropout play in improving your model? Dropout is a regularization technique that randomly sets a fraction of input units to 0 at each update during training. Its role is to prevent overfitting by forcing the network to learn more robust features that are not dependent on the presence of any single input. In our Improved Model, Dropout layers were added (0.4 and 0.5), intending to reduce the model's reliance on specific neurons and improve its generalization to unseen data.
7. **Dropout Role:** It forced the network to learn redundant representations, ensuring that the model doesn't rely on a single "cheat" feature to identify a plant.
8. **Early Stopping:** Early Stopping prevented overfitting by monitoring a performance metric on the validation set (in our case, val_loss). When the val_loss stopped improving for a specified number of epochs (patience=3), training was halted. This ensures that the model stops training before it starts to memorize the training data too much and loses its ability to generalize to new, unseen data, thus preventing the validation loss from increasing due to overfitting.
---
### **C. Performance Comparison**
9. **Observed Improvements:**  Contrary to expectations, no overall improvements were observed in the key validation metrics after modifying the model. The Improved Model showed a decrease across all compared metrics:

 Validation Accuracy: Decreased from 0.6300 to 0.5046. Avg Precision: Decreased from 0.6527 to 0.5523. Avg Recall: Decreased from 0.6117 to 0.5038. Avg F1-score: Decreased from 0.6145 to 0.4989. AUC Score: Decreased from 0.9076 to 0.8188. The only 'improvement' is that the training accuracy for the improved model is now captured (0.4301), which was not explicitly available for the baseline model.

10. **Most Impactful Enhancement:** Given the observed decrease in all validation metrics, it's difficult to pinpoint an enhancement that contributed the most to performance improvement. Instead, the combination of changes in the 'improved' model seems to have deteriorated performance. This could be due to factors like sub-optimal hyperparameters for the new architecture, potential issues with the data augmentation strategy, or a model architecture that is less suitable for the problem compared to the baseline.
 
11. **Generalization Gap:** We don't have the training accuracy for the baseline model to directly compare the gap. However, for the Improved Model, the training accuracy was 0.4301 and the validation accuracy was 0.5046. Curiously, the validation accuracy is higher than the training accuracy for the improved model. This can sometimes happen in early stages of training, or if the data augmentation is applied only to the training set and makes it significantly harder than the validation set, or if the early stopping was very aggressive. Typically, we'd expect training accuracy to be higher than validation accuracy (or very close if the model generalizes perfectly).
---
### **D. Explainability (Grad-CAM)**
12. **Grad-CAM Insights:**  Grad-CAM helped in understanding model predictions by visually highlighting the regions in the input image that were most important for the model's classification decision. By overlaying the heatmap onto the original image, we could see exactly where the CNN was looking when it made its prediction. This provides transparency into the model's reasoning, allowing us to verify if it's focusing on relevant features (e.g., the plant's leaves or stem) or irrelevant background noise.

    
13. **Model Focus:** We only generated Grad-CAM for the baseline model (original_eval_model), as the improved model's performance was worse. For the baseline model, the Grad-CAM overlay (from cell 1fkY60JkhhNH) showed that the model was indeed focusing on the central parts of the plant, specifically the leaves and stem, which are relevant regions for plant classification. Without Grad-CAM for the improved model, we cannot directly compare whether it focused on more relevant regions. However, given its lower performance, it's plausible it might have been focusing on less discriminative or even misleading features, or not focusing as strongly on the correct features.
    
14. **Importance of XAI:** Trust and Acceptance: Users are more likely to trust and adopt AI systems if they understand how decisions are made, especially in critical domains like healthcare or finance. Debugging and Improvement: Explainable AI (XAI) helps developers debug models by identifying biases, errors, or spurious correlations. If a model makes a wrong prediction, XAI can show why, enabling targeted improvements. Compliance and Regulation: In regulated industries, it's often legally required to explain AI decisions to stakeholders or regulatory bodies. Fairness and Ethics: XAI can reveal if a model is making decisions based on discriminatory features, helping to ensure fairness and ethical deployment. Domain Insight: By understanding what features an AI model prioritizes, domain experts can gain new insights into their field. This concludes the comprehensive review of the notebook's activities and your guide questions.
