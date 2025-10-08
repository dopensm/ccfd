# **Credit Card Fraud Detection**

1. **Introduction**

Credit card fraud is a major problem in today’s financial sector, leading to significant financial losses. Detecting fraudulent transactions quickly and accurately is crucial for banks and payment providers. This project implements a machine learning solution to predict credit card fraud using historical transaction data.

The model combines Random Forest and XGBoost in an ensemble approach for high accuracy and robustness, while addressing class imbalance using appropriate techniques.

2. **Objective**

* Build a predictive model to classify transactions as fraudulent or legitimate.  
* Optimize performance metrics such as F1-score, recall, ROC-AUC score, prioritising detection of fraud (minority class).  
* Deploy a trained model with thresholding for real-world inference.  
    
3. **Dataset**

* The dataset contains anonymized credit card transaction data.  
* Features: Transaction amount, time, and anonymized principal components  
* Target variables: Class (0 \= legitimate, 1 \= fraud).  
* Class distribution: Highly imbalance with very few fraudulent transactions (\~0.17%).

4. **Data Preprocessing**

* Checked for missing values (none found).  
* Scaled numerical features where required.  
* Split the dataset into **training** and **testing** sets.  
* Applied techniques to handle class imbalance:	  
  * Adjusted scale\_pos\_weight in XGBoost.  
  * Tuned Random Forest class weights.

5. **Model Selection**

Two models were selected based on performance and interpretability:

1. **Random Forest (RF)**  
   * Handles imbalance well with weighted classes.  
   * Provides feature importance insights.

2. **XGBoost (XGB)**  
   * Gradient boosting with regularization to reduce overfitting.  
   * Tuned scale\_pos\_weight to handle imbalanced data.

**Ensemble approach:** A soft-voting ensemble of RF and XGB was used for final predictions.

**6\. Model Training**

* Both RF and XGB were trained on the training dataset.  
* Hyperparameters were tuned for optimal performance:  
  * RF: n\_estimators, max\_depth, class\_weight  
  * XGB: scale\_pos\_weight, learning\_rate, max\_depth  
* The ensemble used **soft voting** to combine probability outputs.

**7\. Model Evaluation**

**Metrics used:**

* Accuracy  
* Precision  
* Recall  
* F1-score  
* ROC-AUC

**Results (on test set):**

| Model | Precision (Fraud) | Recall (Fraud) | F1-score (Fraud) | ROC-AUC |
| :---: | :---: | :---: | :---: | :---: |
| XGBoost | 0.89 | 0.84 | 0.86 | 0.964 |
| Ensemble | 0.63 | 0.85 | 0.72 | 0.983 |

* Confusion matrices show that the model correctly identifies most fraudulent transactions while keeping false positives low.  
* Threshold tuning improved F1-score for the minority class.

**8\. Deployment**

* Trained ensemble and threshold saved using **joblib**:  
* fraud\_ensemble\_model.pkl  
* fraud\_threshold.pkl  
* Model can be loaded in Python via predict.py for inference.  
* Dependencies are listed in requirements.txt.

**9\. Usage**

1. Clone the repository:

git clone https://github.com/dopensm/ccfd.git  
cd ccfd

2. Install dependencies:

pip install \-r requirements.txt

3. Run predictions:

python predict.py

**10\. Conclusion**

* A robust ensemble model for credit card fraud detection has been developed.  
* Performance metrics indicate high recall for fraudulent transactions, ensuring minimal missed fraud cases.  
* The project can be extended by integrating real-time transaction streaming for deployment in banking systems.

**11\. Future Work**

* Integrate additional features like transaction location and device fingerprinting.  
* Experiment with deep learning models for sequence-based transaction prediction.  
* Deploy a **web API** or **microservice** for real-time fraud detection.

