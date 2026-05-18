# 4_ACTIVITY_1
— Improving CNN Performance Using Regularization, Fine-Tuning, and  Advanced Evaluation

## 🔗 Links
# Google Colab Link: https://colab.research.google.com/drive/1TVqiCLlhnGw0mZFCeKo15R2HYWbh3lC4?usp=drive_link
# Google Drive Link: https://drive.google.com/drive/folders/1JEXebpRXK43gujSRPkj9BaSxLtUv93pb?usp=drive_link
# Github Repo Link: https://colab.research.google.com/drive/1TVqiCLlhnGw0mZFCeKo15R2HYWbh3lC4



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
| **Training Accuracy** | [XX]% | [XX]% | 90% – 97% |
| **Validation Accuracy** | [XX]% | [XX]% | 85% – 93% |
| **Training Loss** | [X.XX] | [X.XX] | 0.1 – 0.3 |
| **Validation Loss** | [X.XX] | [X.XX] | 0.2 – 0.5 |
| **Overall AUC Score** | [0.XX] | [0.00] | > 0.90 |
| **F1-Score (Avg)** | [0.XX] | [0.00] | > 0.85 |

### **Visual Evidence of Improvement**
| Training History | Confusion Matrix |
| :---: | :---: |
| ![Accuracy/Loss Plot](path/to/plot.png) | ![Confusion Matrix](path/to/cm.png) |
| *Stable convergence vs. Baseline* | *Visualizing misclassified species* |



##  PART 2: Explainable AI (Grad-CAM)
Using **Gradient-weighted Class Activation Mapping**, we visualized the decision-making process of the CNN to ensure the model focuses on botanical features rather than background noise.

* **Result:** The improved model successfully localized the **[e.g., leaf venation/flower structure]**, proving that the features learned are relevant to plant biology.
![Grad-CAM Overlay](path/to/gradcam.png)



## 🛠️ Model Enhancements Implemented
1. **Regularization:** Added **Batch Normalization** for stability and **Dropout (0.5)** to prevent overfitting.
2. **Architecture:** Expanded to a 128-filter deep CNN with **He Normalization**.
3. **Optimization:** Reduced Learning Rate to **0.0001** and implemented **Early Stopping** to restore the best weights.
4. **Augmentation:** Added **RandomContrast** and **RandomRotation** to increase dataset variability.



## 📝 Guide Questions: Student Reflection

### **A. Model Evaluation Analysis**
1. **Weakest-performing classes:** Based on the confusion matrix, [Class X] and [Class Y] were the weakest due to similar leaf patterns.
2. **Metric Variance:** Precision was high for distinct species like [Species], while Recall suffered in species with high color variability.
3. **Low Recall Meaning:** It indicates the model is frequently failing to identify the class (False Negatives), often confusing it with a visually similar "neighbor" class.
4. **AUC vs. Accuracy:** AUC reflects the model’s ability to separate classes regardless of the classification threshold, making it more reliable than accuracy for imbalanced datasets.
---
### **B. Model Improvement**
5. **Data Augmentation Effect:** It stabilized the validation accuracy by preventing the model from "memorizing" specific pixel locations.
6. **Batch Normalization Importance:** It normalized the inputs to each layer, which accelerated training and allowed for a higher learning rate without instability.
7. **Dropout Role:** It forced the network to learn redundant representations, ensuring that the model doesn't rely on a single "cheat" feature to identify a plant.
8. **Early Stopping:** It prevented the model from entering the "Overfitting Zone" by terminating training once the validation loss stopped improving for 3 consecutive epochs.
---
### **C. Performance Comparison**
9. **Observed Improvements:** The validation accuracy increased by [XX]% and the loss curves showed significantly less "jitter" compared to Lab 3.
10. **Most Impactful Enhancement:** [Batch Normalization/Early Stopping] was most effective because it [e.g., smoothed the optimization landscape].
11. **Generalization Gap:** The gap decreased to [X]%. This indicates the model is now generalizing rather than memorizing.
---
### **D. Explainability (Grad-CAM)**
12. **Grad-CAM Insights:** It allowed us to debug the model. We verified it was looking at the leaf texture rather than the background soil.
13. **Model Focus:** The improved model showed more localized and "confident" heatmaps on the actual plant organs compared to the baseline.
14. **Importance of XAI:** Explainability is vital in real-world applications (like agriculture) to ensure users can trust the AI’s diagnosis before applying treatments to crops.
