# LSTM-Based-Sequence-Modeling-for-Healthcare-Professional-Engagement

# HCP Journey Sequence Prediction using LSTM (Encoder–Decoder)

This project builds an LSTM-based encoder–decoder model to predict the next best engagement touchpoint for Healthcare Professionals (HCPs).  
In omnichannel pharma engagement, timing and sequencing of touchpoints (Email, Call, Visit, etc.) significantly influence engagement outcomes.  
This model helps automate that decision-making by learning historical interaction behavior and generating the next likely touchpoint.

## 🚀 Project Overview

Healthcare Professionals interact across multiple channels, and the *order* of engagements matters.  
This project uses deep learning to understand those sequences and predict what should happen next.

### 1. Data Preparation
- Generated detailed HCP engagement histories (touchpoint type + timestamp).
- Calculated time differences between consecutive touchpoints.
- Label-encoded touchpoint types.
- Min-max scaled time differences.
- Grouped and padded sequences for LSTM processing.

### 2. Feature Engineering
- Touchpoint types → integer tokens + embedding layer.
- Time difference → numerical sequence (reshaped for LSTM input).
- Both sequences concatenated → input to encoder LSTM.

### 3. Model Architecture

The solution uses an encoder–decoder architecture:

- **Encoder LSTM**  
  Converts the sequence into a context vector (hidden state + cell state).

- **Decoder LSTM**  
  Predicts two outputs:
  - Next touchpoint type (classification with softmax)
  - Next time interval (regression)

A zero-loss output is added to pass internal states without affecting training.

### 4. Training
- Losses:
  - Touchpoint: `sparse_categorical_crossentropy`
  - Time: `mse`
  - State output: zero loss
- Optimizer: Adam
- Early stopping applied
- 80/20 train-test split

### 5. Prediction Function
A multi-step forecasting loop:
- Pads current sequence
- Predicts next touchpoint + time
- Appends back into sequence
- Repeats for `n` steps
- Time predictions inverse-transformed with MinMaxScaler

## 📂 Suggested Project Structure

## 🔧 Technologies Used
- Python  
- TensorFlow / Keras  
- NumPy, Pandas  
- Scikit-learn  
- LSTM Encoder–Decoder architecture  

## 🧪 Example Output

- Predicted touchpoints:  
  `Email → Visit → Call → Email → Visit`

- Predicted time gaps (days):  
  `[2.4, 5.1, 3.0, 6.2, 4.8]`

## 💡 Business Impact

This model empowers commercial pharma teams to:

- Personalize HCP touchpoint journeys
- Optimize omnichannel sequencing
- Improve engagement relevance
- Strengthen recommendation and conversion rates

## 📈 Future Enhancements
- Add additional HCP-level features (specialty, behavior clusters)
- Include attention mechanism for better sequence learning
- Deploy via FastAPI + Docker
- Hyperparameter tuning with Optuna

