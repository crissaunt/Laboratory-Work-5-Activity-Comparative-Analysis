# Laboratory-Work-5-Activity-Comparative-Analysis

https://colab.research.google.com/drive/1bZ-1yKoyz_IN3swwv2zky1sexGOaP-z_?usp=sharing

<img width="446" height="394" alt="image" src="https://github.com/user-attachments/assets/2b74c1b1-14dc-424d-b094-7fe085e2df50" />
<img width="201" height="214" alt="image" src="https://github.com/user-attachments/assets/95c2cde1-8f3d-4d78-856d-93adb8222570" />
<img width="225" height="214" alt="image" src="https://github.com/user-attachments/assets/19d331e7-f781-46fe-a82b-7d48dc3754b9" />





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
