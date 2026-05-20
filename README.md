# Laboratory-Work-5-Activity-Comparative-Analysis
https://colab.research.google.com/drive/1z3LkUvkKFDNFTVQceA849G6GR9KDOiFc?usp=drive_link

# Performance Comparison Table

| Model - Sample | Train Accuracy | Train Loss | Test Accuracy | Test Loss | Precision | Recall | F1-score | ROC | AUC |
|---|---|---|---|---|---|---|---|---|---|
| Pre-trained Model 1 (VGG16) ~267 | 65.80% | 1.6296 | 6.00% | 1.4655 | 0.06 | 0.06 | 0.05 | 0.5039 | 0.5039 |
| Pre-trained Model 2 (ResNet50) ~267 | 73.61% | 1.2255 | 7.00% | 1.1464 | 0.08 | 0.05 | 0.03 | 0.5034 | 0.5034 |
| Pre-trained Model 3 (MobileNetV2) ~267 | 75.84% | 0.8939 | 5.00% | 1.0122 | 0.05 | 0.05 | 0.05 | 0.4803 | 0.4803 |
| Teachable Machine ~16,199 | 97.30% | 0.0842 | 94.80% | 0.1563 | 0.95 | 0.94 | 0.94 | 0.9810 | 0.9810 |
| Your 1st Model (EfficientNet, 15 epochs) 5,831 | 89.55% | 0.3306 | 86.00% | 0.5659 | 0.89 | 0.85 | 0.86 | 0.96 | 0.96 |
| Your 2nd Model Enhancement (EfficientNet + EarlyStopping) 5,831 | 79.81% | 0.6850 | 83.86% | 0.6417 | 0.86 | 0.83 | 0.84 | 0.9481 | 0.9481 |
| Your 3rd Model - The Good Model (ResNet101, 10 epochs) 1,165 | 72.86% | 1.1317 | 35.00% | 1.2011 | 0.33 | 0.30 | 0.25 | 0.65 | 0.65 |

<img width="1700" height="466" alt="image" src="https://github.com/user-attachments/assets/0f0ce64e-c8d3-4b1f-a9bb-b355a7610a9d" />
<img width="1708" height="576" alt="image" src="https://github.com/user-attachments/assets/7901b7b5-dbb0-47c7-a7f2-0303bb1e6d78" />
<img width="1708" height="600" alt="image" src="https://github.com/user-attachments/assets/5e1ddca9-a982-46dc-bffe-b675dca3f22d" />






A. Model Performance

EfficientNetB3 (98.45% accuracy) due to its compound scaling giving higher capacity to learn complex features.

EfficientNetB0 (9.44% accuracy), likely due to being too small, getting stuck in a poor local minimum, or incompatible training settings.

Loss inversely correlated with accuracy: high-accuracy models had low loss (0.0558–0.1000); low-accuracy models had high loss (1.2107–2.9708).

B. Evaluation Metrics
4. Accuracy hides class imbalance and error types (false positives/negatives); precision, recall, and F1-score give fuller insight.
5. ResNet101 (macro F1=0.22). It indicates the best balance between precision and recall among reported models, though still poor overall.
6. ResNet101 had varied precision/recall across classes (some classes at 0.00); others (VGG16, ResNet50, MobileNetV2) had consistently very low values due to evaluation issues.

C. Confusion Matrix Analysis
7. Classes with 0.00 recall: kalabasa, kangkong, lettuce, mangga, papaya, patola, saluyot, sitao.
8. The model completely failed to recognize many classes, never predicting them correctly, indicating severe bias or incapacity.

D. ROC and AUC
9. VGG16 (AUC = 0.5039 macro, OvR) — barely above random chance.
10. AUC measures ability to distinguish classes (0.5 = random, 1.0 = perfect). Scores near 0.5 indicate no discriminative power.

E. Explainability (Grad-CAM)
11. Grad-CAM showed which image regions influenced the prediction (heatmap over lettuce image).
12. Not verifiable without visual output, but a good model focuses on the object (e.g., lettuce leaves), not background.
13. Only ResNet101 was evaluated; no cross-model comparison available.

F. Model Comparison & Improvement
14. EfficientNetB3 — highest validation accuracy (98.45%), low loss, and good efficiency for real-world deployment.
15. Fine-tune unfrozen layers, use advanced augmentation (mixup/cutmix), tune hyperparameters, ensemble with other top models, and address class imbalance.

G. Real-World Application
16. Automated retail checkout, inventory management, quality control, nutritional apps, and agricultural crop identification.
17. Financial losses, customer dissatisfaction, health/safety risks (e.g., spoiled food missed), operational inefficiencies, and misguided decisions.
18. Mobile: Convert to TensorFlow Lite for on-device inference or deploy as cloud API. Web: Backend API (Flask/Django) or TensorFlow.js for browser-based inference. Ensure matching preprocessing.
