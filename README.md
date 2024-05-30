## Drug Discovery: A Machine Learning and Deep Learning Approach using SMILES Strings

This Jupyter Notebook demonstrates the use of Machine Learning and Deep Learning for drug discovery of a specific protein. We establish a pipeline that includes constructing a Random Forest (RF) regression model to predict the pIC50 values for the target’s chemical compounds, employing LSTMs to generate novel Simplified Molecular-Input Line Entry System (SMILES) strings, and utilizing the trained RF model to predict the pIC50 values for the generated strings.

Inspired by Chanin Nantasenamat's [Computational Drug Discovery](https://github.com/dataprofessor/code/blob/master/python/CDD_ML_Part_1_Acetylcholinesterase_Bioactivity_Data_Concised.ipynb)

## Methods and Dataset
* Dataset
  * Bioactivity data from the ChEMBL database for Human Acetylcholinesterase (hAChE)
  * 9,091 data points and 46 associated properties
  * Preprocessing data:
    * remove duplicates and missing values
    * normalized IC50 values with negative log base 10
    * calculate fingerprint descriptor using molecule ID and SMILES strings
* Methods
  * Training Random Forest model
    * Apply nested cross-validation to find optimal parameters (5-fold outer loop and 3-fold inner loop)
    * Summary of nested cross-validation

        | k-fold    | Best parameters | Best scores |
        | -------- | ------- | ------- |
        | k=1  | {'max_depth': 100, 'n_estimators': 1000} | 0.58   |
        | k=2  | {'max_depth': 90, 'n_estimators': 1000}  | 0.55    |
        | k=3  | {'max_depth': 100, 'n_estimators': 1000} | 0.46    |
        | k=4  | {'max_depth': 100, 'n_estimators': 1000} | 0.52    |
        | k=5  | {'max_depth': 100, 'n_estimators': 1200} | 0.52    |
  * Training [SMILES generator](https://github.com/alexarnimueller/SMILES_generator) with 1,725 SMILES strings representing active molecules

## Results
* Mean Absolute Error for Random Forest: **0.75**
![test_pred_v1](https://github.com/TienNguyen93/drug-discovery/assets/43976085/fb8575ac-3b33-493a-9e7c-784cd2385926)

* SMILES generator: cannot generate novel SMILES string due to minimum amount of training data
