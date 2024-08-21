# HSBC-Hackathon-Fraudulent-Transaction-Detection

## **Problem Statment** - Develop an AI model capable of detecting fraudulent transactions in real-time. Use historical transaction data to train the model to identify anomalies and flag suspicious activities.

# Model Documentation - Weighted Classification using Two XGBoost Models

This documentation provides an overview of the weighted classification approach using two XGBoost models. The models are trained with different hyperparameters, and their predictions are combined using a weighted average.

## Model Parameters

### Model 1 Parameters:
- **colsample_bytree**: `0.8`
- **learning_rate**: `0.01`
- **max_depth**: `9`
- **n_estimators**: `100`
- **subsample**: `0.8`

### Model 2 Parameters:
- **colsample_bytree**: `1.0`
- **learning_rate**: `0.2`
- **max_depth**: `6`
- **n_estimators**: `100`
- **subsample**: `1.0`

## Weightage for Model Predictions

The predictions from the two models are combined using a weighted average, with the following weights:

- **Model 1 Weight**: `0.6`
- **Model 2 Weight**: `0.4`

## Prediction Process

1. **Training**: Both models are trained separately using their respective parameters on the same dataset.

2. **Prediction**:
   - Each model generates probabilities for the positive class (e.g., fraud) on the test dataset.
   - The probabilities are combined using a weighted average:
   
   **Combined Probability** = (0.6 × Model 1 Probability) + (0.4 × Model 2 Probability)


3. **Thresholding**:
   - The combined probabilities are then thresholded at `0.5` to make the final binary classification:
     \[
     \text{Final Prediction} = 
     \begin{cases} 
     1 & \text{if Combined Probability} \geq 0.5 \\
     0 & \text{otherwise}
     \end{cases}
     \]

## Evaluation Metrics

The performance of the combined model can be evaluated using various metrics such as:

- **Precision**: The proportion of positive identifications that are actually correct.
- **Recall**: The proportion of actual positives that are correctly identified.
- **F1-Score**: The harmonic mean of precision and recall.
- **ROC AUC Score**: The Area Under the Receiver Operating Characteristic Curve, indicating the model's ability to distinguish between the classes.

## Conclusion

This approach allows leveraging the strengths of two models with different configurations by combining their predictions in a weighted manner. The choice of weights (0.6 for Model 1 and 0.4 for Model 2) reflects the relative importance or performance of each model in the final decision-making process.
