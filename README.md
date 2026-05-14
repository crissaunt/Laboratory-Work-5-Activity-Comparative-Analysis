# Laboratory-Work-5-Activity-Comparative-Analysis

https://colab.research.google.com/drive/1bZ-1yKoyz_IN3swwv2zky1sexGOaP-z_?usp=sharing

<img width="446" height="394" alt="image" src="https://github.com/user-attachments/assets/2b74c1b1-14dc-424d-b094-7fe085e2df50" />
<img width="201" height="214" alt="image" src="https://github.com/user-attachments/assets/95c2cde1-8f3d-4d78-856d-93adb8222570" />
<img width="225" height="214" alt="image" src="https://github.com/user-attachments/assets/19d331e7-f781-46fe-a82b-7d48dc3754b9" />





A. Model Performance

Which pre-trained model achieved the highest accuracy? Why?

Based on the training logs (Epoch 10 validation accuracy), EfficientNetB3 achieved the highest accuracy of 0.9845.
EfficientNet models are renowned for their high performance through a compound scaling method that systematically scales network depth, width, and resolution. EfficientNetB3, being a larger variant, likely benefited from greater capacity to learn complex features, leading to superior generalization.
Which model had the lowest performance? What could be the reason?

Based on the training logs, EfficientNetB0 had the lowest accuracy of 0.0944 and the highest loss of 2.9708.
This extremely low performance (barely above random chance for 20 classes) suggests a significant issue during its training. Possible reasons include: the model getting stuck in a poor local minimum, the base model being too small (B0 is the smallest EfficientNet variant) to learn effectively when its layers are frozen, or an incompatibility with the specific dataset and training parameters (e.g., learning rate) when only the top layers are trained.
How did loss values compare across models?

Loss values generally showed an inverse correlation with accuracy. Models with higher validation accuracy (e.g., EfficientNetB3, ResNet50, Xception, InceptionV3, MobileNetV2) consistently exhibited significantly lower validation loss values (ranging from 0.0558 to 0.1000). This indicates they were more confident and correct in their predictions.
Conversely, models with very low accuracy (e.g., EfficientNetB0, DenseNet121, NASNetMobile, ResNet101) had much higher validation losses (ranging from 1.2107 to 2.9708), reflecting their inability to make accurate classifications and their high predictive uncertainty.
B. Evaluation Metrics

Why is accuracy not enough to evaluate a model?

Accuracy can be misleading, especially with imbalanced datasets. A model might achieve high accuracy by simply predicting the majority class, while failing to correctly identify minority classes. It doesn't provide insight into the types of errors (false positives vs. false negatives), which can be critical depending on the application. Metrics like precision, recall, F1-score, and AUC offer a more comprehensive understanding of a model's performance across all classes.
Which model had the best F1-score? What does it indicate?

Among the models for which classification_report output was provided (ResNet101, VGG16, ResNet50, MobileNetV2), ResNet101 had the highest F1-score (macro average 0.22, weighted average 0.24).
The F1-score is the harmonic mean of precision and recall, providing a single metric that balances both. A higher F1-score indicates a better balance between correctly identifying positive instances (recall) and avoiding false positives (precision). The reported F1-scores are still quite low, suggesting overall poor performance in balancing precision and recall across all classes for these models.
Note: There was a significant discrepancy between training validation accuracies (high) and reported classification report accuracies/F1-scores (low) for VGG16, ResNet50, and MobileNetV2, suggesting a potential issue with how those evaluation metrics were computed in the notebook (e.g., val_ds iteration issues). ResNet101's report matched its training performance.
How did Precision and Recall differ across models?

For ResNet101, the precision and recall values varied widely across classes. Some classes showed decent precision but very low recall (e.g., 'eggplant' precision 0.89, recall 0.12), meaning it was often correct when it predicted that class but missed many instances of it. Other classes had higher recall but low precision (e.g., 'chili' recall 0.86, precision 0.20), meaning it identified many actual instances but also mislabeled many non-instances. Notably, several classes had 0.00 precision and recall ('kalabasa', 'kangkong', 'lettuce', 'mangga', 'papaya', 'patola', 'saluyot', 'sitao'), indicating a complete failure to classify these.
For VGG16, ResNet50, and MobileNetV2 (as evaluated in the uqUMw1I-jy_h cell), both precision and recall were consistently very low (mostly below 0.15) across almost all classes, indicating these models struggled in both identifying positive instances correctly and finding all positive instances when evaluated this way.
C. Confusion Matrix Analysis

Which classes were frequently misclassified?

Based on the classification_report for ResNet101, classes with a recall of 0.00 were most frequently misclassified: 'kalabasa', 'kangkong', 'lettuce', 'mangga', 'papaya', 'patola', 'saluyot', and 'sitao'. This means the model never correctly identified any images belonging to these classes. Classes with very low recall like 'carrots', 'eggplant', 'onion', and 'tomato' were also highly misclassified.
What patterns did you observe in the confusion matrix?

Since the confusion matrix plot itself was not displayed in the output, specific patterns of which classes were confused with which cannot be observed directly. However, based on the classification_report for ResNet101, a clear pattern is the complete failure to recognize numerous classes (0.00 recall for many). This indicates that the model either consistently predicted these specific classes as other categories or simply never predicted them at all. The uneven precision and recall values across other classes also suggest that some classes are more difficult to distinguish, or the model has developed a bias towards predicting certain classes over others.
D. ROC and AUC

Which model had the highest AUC score?

AUC scores were reported for VGG16, ResNet50, and MobileNetV2. Among these, VGG16 had the highest AUC score of 0.5039 (macro, OvR).
Note: These AUC scores are very close to 0.5, which typically signifies a model performing no better than random chance. This again highlights the potential evaluation discrepancy mentioned earlier for these specific models.
What does AUC tell us about model performance?

AUC (Area Under the Receiver Operating Characteristic curve) quantifies a model's ability to distinguish between classes. It represents the probability that the model will rank a randomly chosen positive instance higher than a randomly chosen negative instance. A higher AUC (closer to 1.0) indicates better overall discriminative performance across various classification thresholds. An AUC of 0.5 suggests the model's performance is equivalent to random guessing. In a multi-class setting (like here), a macro-averaged AUC typically averages the AUC for each class in a one-vs-rest manner.
E. Explainability (Grad-CAM)

What did Grad-CAM reveal about model decision-making?

Grad-CAM was applied to the ResNet101 model for an image of 'lettuce'. The technique generates a heatmap that highlights the regions in the input image that were most influential in the model's prediction. Generally, Grad-CAM aims to show whether the model is focusing on relevant visual features of the object (e.g., the leaves of the lettuce) or irrelevant background details.
Did the model focus on relevant image regions?

Without the visual output of the Grad-CAM heatmap and its overlay on the image, a definitive answer is not possible. However, if the heatmap showed concentrated activation over the 'lettuce' in the image, it would indicate that the model focused on the correct, relevant regions for its classification decision. If the heatmap was diffuse or centered on unrelated parts of the image, it would suggest the model was not using appropriate visual cues.
Which model produced the most meaningful heatmaps?

Grad-CAM was only demonstrated for the ResNet101 model in the provided output. Therefore, we cannot compare the quality or meaningfulness of heatmaps across different models based on the available information.
F. Model Comparison & Improvement

Which model would you recommend for deployment? Why?

Based on the training validation accuracies, EfficientNetB3 (accuracy 0.9845, loss 0.0558) would be recommended for deployment. Its superior performance during training suggests it learned the features most effectively and generalized best to unseen validation data. EfficientNet models are also known for striking a good balance between accuracy and computational efficiency, making them practical for real-world deployment.
How can you further improve your best-performing model?

To further improve EfficientNetB3:
Fine-tuning: Gradually unfreeze more layers of the pre-trained EfficientNetB3 base model and continue training with a very low learning rate, allowing the model to adapt more specifically to the dataset.
Advanced Data Augmentation: Implement more sophisticated augmentation techniques (e.g., mixup, cutmix, autoaugment) to enhance data diversity.
Hyperparameter Optimization: Conduct a more thorough search for optimal learning rates, batch sizes, optimizers (e.g., AdamW), and regularization techniques (e.g., more aggressive dropout).
Ensemble Methods: Combine EfficientNetB3 with other high-performing models (e.g., ResNet50, InceptionV3) through ensemble techniques (like averaging predictions) to potentially achieve even higher robustness and accuracy.
Address Class Imbalance: If there are still class imbalance issues, implement techniques like weighted loss, oversampling, or undersampling.
G. Real-World Application

How can your model be applied in real-world scenarios?

Assuming the model accurately classifies fruits and vegetables, it could be used for:
Automated Retail Systems: Speed up checkout processes by automatically identifying produce at grocery stores.
Inventory Management: Monitor and track produce stock levels in supermarkets or warehouses.
Quality Control: Detect and sort out damaged, spoiled, or unripe produce in supply chains.
Nutritional Apps: Help users identify food items from images to provide nutritional information or recipe suggestions.
Agricultural Intelligence: Assist farmers in identifying crop types, growth stages, or potential diseases.
What are the risks of deploying an inaccurate model?

Deploying an inaccurate model can lead to significant risks:
Financial Losses: Misclassifications in retail could lead to incorrect pricing and revenue loss.
Customer Dissatisfaction: Erroneous identifications in consumer apps can frustrate users and erode trust.
Health and Safety: In food quality control, missing spoiled items could pose health risks to consumers.
Operational Inefficiencies: Requiring constant human oversight or manual correction negates the benefits of automation.
Misguided Decisions: In agriculture, incorrect disease identification could lead to crop failures.
How can this system be integrated into a mobile/web app?

Mobile App Integration:
On-device Inference: Convert the model to a mobile-optimized format like TensorFlow Lite (.tflite). This allows the model to run directly on the device, providing fast, offline inference capabilities.
Cloud-based Inference: Deploy the model to a cloud service (e.g., Google Cloud AI Platform, AWS SageMaker) as a REST API. The mobile app captures an image, sends it to the cloud for prediction, and displays the result (requires internet connectivity).
Web App Integration:
Backend API: Deploy the model on a server-side framework (e.g., Flask, Django) as a RESTful API. The web application sends image data to this API, which performs inference and returns the results to the client-side.
Browser-based Inference: Convert the model to TensorFlow.js format to run inference directly within the user's web browser, offering immediate feedback and reducing server load for simpler models.
In both cases, preprocessing steps (resizing, normalization) for the input images must match what the model expects, and the app would need functionalities for image capture/upload and displaying predictions
