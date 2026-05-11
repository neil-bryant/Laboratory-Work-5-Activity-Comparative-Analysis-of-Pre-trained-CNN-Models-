Google Drive:
https://drive.google.com/drive/folders/1YayFfeVTXGSpMxTL2guComR6eYvTnwfJ?usp=sharing

Goggle Collab:
https://colab.research.google.com/drive/1l337kLVaxvefZZpu3u90tqfwtREZRzFX?usp=sharing

Comparative Analysis of Pre-trained CNN Models for Custom Image Classification

Pre-trained Models Used
MobileNetV2 — Fastest, best for mobile deployment
EfficientNetB0 — Best overall accuracy
InceptionV3 — Stable, strong baseline

Dataset
20 Mushroom Species — 250 images per class
Total Images: 5,000
Split: 80% Training / 20% Validation
Image Size: 224×224 pixels

Performance Comparison Table

| Model          | Train Acc | Train Loss | Val Acc    | Val Loss   | Precision  | Recall     | F1-Score   | AUC        |
| -------------- | --------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- | ---------- |
| MobileNetV2    | 98.82%    | 0.0837   | *99.59%  | 0.0282 |  99.66% | 99.66% |  99.65%| 0.9999  |
| EfficientNetB0 | 99.13%   |0.0911    | 100.00%     |  0.0094    | 100.00%    | 100.00%    | 100.00%   | 1.0000   |
| InceptionV3    |83.91%     | 0.7569    | 83.71%     |0.3643     |  88.49%   |   84.24%   | 83.03%    |  0.9891   |

| Model                | Val Accuracy | Val Loss | Precision | Recall | F1-Score | AUC    | Notes                   |
| -------------------- | ------------ | -------- | --------- | ------ | -------- | ------ | ----------------------- |
| Teachable Machine    | 24.40%       | 6.2387   | 20.80%    | 24.19% | 22.00%   | 0.6338 | Label order mismatch    |
| LW3 — Custom CNN     | 93.20%       | 0.2215   | 94.91%    | 93.18% | 92.89%   | 0.9644 | Baseline improved model |
| LW4 — Enhanced CNN   | 96.70%       | 0.0644   | 97.80%    | 96.85% | 96.68%   | 0.9963 | Best custom CNN         |
| LW5 — InceptionV3    | 94.50%       | 0.1500   | 94.87%    | 94.74% | 94.64%   | 0.9961 | Pre-trained (ImageNet)  |
| LW5 — EfficientNetB0 | 97.30%       | 0.0663   | 98.29%    | 97.71% | 97.49%   | 0.9977 | Pre-trained (ImageNet)  |
| LW5 — MobileNetV2    | 97.70%       | 0.0596   | 98.47%    | 98.05% | 97.88%   | 0.9989 | Best overall            |



GUIDE QUESTIONS (FINAL REFLECTION)

A. Model Performance

A. Model Performance

1. Which pre-trained model achieved the highest accuracy? Why?
EfficientNetB0 achieved the highest validation accuracy at 100.00%. After correcting the preprocessing step using its proper preprocess_input function, the model successfully utilized its pre-trained ImageNet weights, resulting in excellent classification performance.

2. Which model had the lowest performance? What could be the reason?
InceptionV3 had the lowest performance with 83.71% validation accuracy. Early Stopping restored the model weights from Epoch 1, suggesting that validation performance did not improve and the model may have overfit early or used non-optimal hyperparameters for the dataset.

3. How did loss values compare across models?
 EfficientNetB0 achieved the lowest validation loss (0.0094), showing excellent performance and matching its 100% accuracy. MobileNetV2 followed with a low validation loss of 0.0282 and high accuracy of 99.59%. Meanwhile, InceptionV3 had the highest validation loss (0.3643), which corresponded to its lower accuracy of 83.71%, indicating weaker optimization performance.

B. Evaluation Metrics
4. Why is accuracy not enough to evaluate a model?
Accuracy can be misleading in imbalanced datasets because a model may achieve high accuracy by predicting only the majority class while failing to identify minority classes correctly. It also treats all errors equally, even when some mistakes are more critical than others. Metrics like Precision, Recall, and F1-score provide a better understanding of model performance by evaluating specific types of classification errors.

5. Which model had the best F1-score? What does it indicate?
EfficientNetB0 achieved the best F1-score at 100.00%, indicating a perfect balance between Precision and Recall. This means the model correctly identified all class instances without producing false positives or false negatives.

6. How did Precision and Recall differ across models?
EfficientNetB0 achieved perfect Precision and Recall scores of 100.00%, showing excellent classification with almost no errors. MobileNetV2 also performed very well with 99.66% for both metrics, indicating only a few minor misclassifications. In contrast, InceptionV3 had lower Precision (88.49%) and Recall (84.24%), meaning it produced more false positives and false negatives, leading to weaker overall performance.

C. Confusion Matrix Analysis

7. Which classes were frequently misclassified?
 For the InceptionV3 model, the most frequently misclassified classes were Cattleya (Recall: 21%), Epindendrum (Recall: 42%), and Miltoniopsis (Recall: 37%), meaning many actual samples were incorrectly predicted as other classes. Orsum (Precision: 54%), Stanhopea (Precision: 58%, Recall: 78%), and Masdevallia (Precision: 66%) also showed frequent confusion due to higher false positive predictions.

8. What patterns did you observe in the confusion matrix?
   The InceptionV3 confusion matrix showed strong pairwise misclassifications, such as Cattleya being confused with Stanhopea, Epindendrum with Pleurothallis, and Miltoniopsis with Phragmipedium. Some classes had low recall, meaning many actual samples were missed, while others had low precision due to false positives. These patterns suggest difficulty distinguishing visually similar orchid classes, likely worsened by Early Stopping, which ended training after only one epoch.

D. ROC and AUC

9. Which model had the highest AUC score?   
The EfficientNetB0 model had the highest AUC score of 1.0000.
10. What does AUC tell us about model performance?
AUC measures how well a model separates classes. In multi-class problems, it’s averaged across all classes (one-vs-rest). A value of 1.0 means perfect classification, while 0.5 means random guessing.

E. Explainability (Grad-CAM)
11. What did Grad-CAM reveal about model decision-making?
Grad-CAM shows which parts of an image influence a model’s prediction by producing a heatmap of important regions. For MobileNetV2 and InceptionV3, it highlighted the key areas used for classification in the test image. However, for EfficientNetB0, Grad-CAM failed due to a missing layer error, so its decision-making process could not be visualized.

12. Did the model focus on relevant image regions?
The exact image regions cannot be confirmed without visually inspecting the Grad-CAM heatmaps. However, we can infer from prediction confidence: MobileNetV2 predicted “Marriot” with 43.48% confidence, suggesting it likely focused on relevant orchid features if the prediction is correct. In contrast, InceptionV3 predicted “Calanthe” with only 7.36% confidence, indicating weak focus on meaningful features and overall uncertainty in its decision.

13. Which model produced the most meaningful heatmaps?
Without visual heatmaps, only inference is possible. EfficientNetB0 failed Grad-CAM due to a layer error. Between the others, MobileNetV2 (43.48% confidence) likely focused on more relevant features than InceptionV3 (7.36%), which showed weak and uncertain attention.

F. Model Comparison & Improvement
14. Which model would you recommend for deployment? Why?
EfficientNetB0 is the best choice for deployment because it achieved 100% validation accuracy, the lowest validation loss (0.0094), perfect AUC (1.0000), and perfect Precision, Recall, and F1-score. This means it made no classification errors on the validation set. Although MobileNetV2 also performed strongly (99.59% accuracy), EfficientNetB0 was consistently superior across all metrics, making it the most reliable model for this dataset.

15. How can you further improve your best-performing model?
Even with perfect results, improvements are still possible. Using stronger data augmentation, collecting a larger and more diverse dataset, and applying ensemble methods can improve robustness. Fine-tuning EfficientNetB0, tuning hyperparameters, and using cross-validation would also help confirm and strengthen its real-world performance.

G. Real-World Application
16. How can your model be applied in real-world scenarios?
The orchid classification system, especially the best model EfficientNetB0, has practical uses such as helping users identify orchids through photos, supporting growers in managing nursery plants, and assisting botanists in biodiversity monitoring and conservation work. It can also be extended for early pest or disease detection and used as an educational tool for learning orchid species.

17. What are the risks of deploying an inaccurate model?
 An inaccurate orchid classification model can cause misidentification, leading to improper plant care and even plant loss for hobbyists. In agriculture, it may result in poor crop management and economic losses. In conservation, it can misdirect efforts and resources away from truly endangered species. Overall, it reduces user trust and limits adoption of the system.

18. How can this system be integrated into a mobile/web app?
To integrate the orchid classification model into an app, the trained EfficientNetB0 can be converted to a mobile format like TensorFlow Lite for on-device inference or deployed via a cloud API for web/mobile use. The application should include proper image preprocessing, a user-friendly interface for capturing/uploading images, and display predictions with confidence scores. Optional features like user feedback and periodic model updates can further improve accuracy and performance over time.
