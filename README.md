# Customer-Retention-Prediction-Using-Artificial-Neural-Networks

## Introduction
This project focuses on predicting customer retention using Artificial Neural Networks (ANNs). The study analyzes the impact of neural network depth, activation functions, and gradient descent optimization techniques on model performance and learning behavior.

The target variable is:

- **Retention**
  - `1` → Customer retained
  - `0` → Customer not retained

---

## Dataset Description

The dataset contains customer-related numerical and categorical features including:

- Age
- MonthlyIncome
- YearsWithCompany
- UsageHours
- CustomerSatisfaction
- LoyaltyScore
- LastActivityDays
- ContactType
- NumProducts
- NumComplaints

The objective is to predict whether a customer will remain retained based on these attributes.

---

## Data Preprocessing

### Missing Value Handling
The dataset was inspected for missing values, and no missing values were found.

### Feature Selection
The following numerical features were selected for scaling:

- Age
- MonthlyIncome
- YearsWithCompany
- UsageHours
- CustomerSatisfaction
- LoyaltyScore
- LastActivityDays

Discrete and binary features such as:

- ContactType
- NumProducts
- NumComplaints

were excluded from scaling to preserve their original representation.

### Outlier Analysis
Box plot analysis was performed to inspect outliers. Although some extreme values were observed, none were significant enough to justify removal.

### Feature Scaling
Standardization was applied using **StandardScaler** to transform numerical features to:

- Zero mean
- Unit variance

### Train-Test Split
The dataset was divided into:

- **80% Training**
- **20% Testing**

using stratified sampling based on the retention label.

---

## Artificial Neural Network Models

### Deep Neural Network with Sigmoid Activation

A deep neural network with **10 layers** was trained to study the effect of network depth and sigmoid activation.

### Configuration
- Activation Function: Sigmoid
- Optimizer: SGD
- Learning Rate: 0.01
- Loss Function: Binary Cross Entropy
- Epochs: 50

### Training Outcome
The model showed minimal improvement during training:

| Metric | Training | Validation |
|---|---|---|
| Final Loss | 0.645 | 0.645 |
| Final Accuracy | 65.3% | 65.4% |

This indicated learning difficulties caused by vanishing gradients.

---

# Part 1: Vanishing Gradients

## Training Observations
The deep neural network experienced:

- Nearly constant training accuracy (~65%)
- Minimal reduction in loss
- Flat training and validation loss curves

These observations indicated ineffective learning.

## Vanishing Gradient Problem
Vanishing gradients occurred because gradients became extremely small while propagating backward through deep sigmoid layers. As a result:

- Early layers received negligible updates
- Learning stagnated
- Model convergence failed

## Impact on Performance
The vanishing gradient issue severely reduced predictive performance and prevented the network from learning effectively.

## Remedies for Vanishing Gradients
Several techniques can reduce vanishing gradients:

- Replacing Sigmoid with ReLU
- Proper weight initialization
- Batch normalization
- Reducing network depth
- Using advanced optimizers such as Adam

## Implemented Solution
The sigmoid activation function was replaced with **ReLU** in hidden layers.

This resulted in:

- Faster convergence
- Better gradient propagation
- Improved learning performance

---

# Part 2: Gradient Descent Variants

## Experimental Setup

Three neural networks with identical architectures were trained using different gradient descent strategies.

### Common Settings
- Hidden Activation: ReLU
- Output Activation: Sigmoid
- Learning Rate: 0.001
- Loss Function: Binary Cross Entropy
- Epochs: 50

### Gradient Descent Variants
1. Stochastic Gradient Descent (SGD)
2. Batch Gradient Descent (BGD)
3. Mini-Batch Gradient Descent (MBGD)

---

## Training Time Comparison

| Optimizer | Training Time |
|---|---|
| SGD | High |
| Batch GD | Low |
| Mini-Batch GD | Medium |

### Observations
- SGD required many updates and showed noisy convergence
- Batch GD converged slowly but smoothly
- Mini-Batch GD balanced efficiency and stability

---

## Final Performance Comparison

| Optimizer | Final Loss | Final Accuracy | Convergence |
|---|---|---|---|
| SGD | ≈ 0.638 | ≈ 65.4% | Noisy |
| Batch GD | ≈ 0.681 | ≈ 57.9% | Slow & Smooth |
| Mini-Batch GD | ≈ 0.644 | ≈ 65.4% | Fast & Stable |

## Recommended Optimization Method
Mini-Batch Gradient Descent provided the best balance between:

- Training speed
- Stability
- Convergence behavior
- Predictive performance

---

# Part 3: Activation Functions

## Experimental Setup

Four activation functions were compared using neural networks with:

- 3 hidden layers
- 32 neurons per layer

### Common Settings
- Optimizer: Adam
- Learning Rate: 0.001
- Batch Size: 32
- Loss Function: Binary Cross Entropy
- Epochs: 50
- Validation Split: 20%

### Activation Functions Evaluated
1. Sigmoid
2. Tanh
3. ReLU
4. Leaky ReLU

---

## Training Behavior Analysis

### Sigmoid and Tanh
- Slower convergence
- Stable learning
- Better generalization

### ReLU and Leaky ReLU
- Faster convergence
- Lower training loss
- Signs of overfitting

---

## Final Performance Comparison

| Activation | Train Loss | Val Loss | Train Accuracy | Val Accuracy |
|---|---|---|---|---|
| Sigmoid | 0.6429 | 0.6458 | 65.34% | 65.44% |
| Tanh | 0.6252 | 0.6615 | 65.88% | 63.51% |
| ReLU | 0.6113 | 0.6749 | 66.92% | 63.90% |
| Leaky ReLU | 0.6130 | 0.6787 | 66.80% | 62.36% |

---

## Best Performing Activation Function

Although ReLU achieved better training accuracy, Sigmoid demonstrated:

- Better validation accuracy
- Stable learning behavior
- Lower overfitting

This indicates that faster convergence does not always guarantee better generalization.

---

## Technologies Used

- Python
- TensorFlow
- Keras
- NumPy
- Pandas
- Matplotlib
- Scikit-learn

---

## Conclusion

This project analyzed the performance of Artificial Neural Networks for customer retention prediction. The experiments highlighted important deep learning concepts including vanishing gradients, optimization strategies, and activation function behavior.

The results demonstrated that:

- ReLU effectively mitigates vanishing gradients
- Mini-Batch Gradient Descent provides balanced optimization performance
- Sigmoid activation achieved the best generalization performance for this dataset

The study emphasizes the importance of selecting suitable architectures, activation functions, and optimization methods to achieve stable and effective neural network learning.
