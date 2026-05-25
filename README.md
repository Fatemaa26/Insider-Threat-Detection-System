# Insider-Threat-Detection-System
An intelligent supervised machine learning pipeline to detect malicious insider activities using an Ensemble Stacking Classifier.

## 🔄 How to Adapt This Code for a Different Dataset
To easily reuse this pipeline on another tabular dataset, you only need to modify a few column name strings in the notebook:

1. **Target Label:** In the Data Splitting cell, change `'is_malicious'` to your dataset's specific prediction target column name (e.g., `'Attack'` or `'Fraud'`).
2. **Missing Data Handling:** If your dataset doesn't need artificial missing rows injected, completely skip/delete Cell 5, or update the `columns` list with your new dataset's feature names.
3. **Feature Selection:** In the column-dropping cell, replace the strings in `cols_to_drop` (`'total_files_burned'`, etc.) with the redundant features identified by your new dataset's correlation heatmap.

## 💾 Data Source
The dataset used in this project is the public **Insider Threat Detection Dataset** available on Kaggle. 
* To run this notebook, download the raw data from Kaggle and place it in your local project directory.

> ⚠️ **Important Note on Outliers:** > This pipeline deliberately omits an outlier-removal step because it is optimized for **Cybersecurity Anomaly Detection**, where extreme behavioral spikes (e.g., massive off-hour data transfers) represent actual malicious threats rather than data errors. Deleting outliers would erase the threat signatures. 
> 
> * If you are adapting this code for **Security, Fraud, or Intrusion Detection**, leave the outlier handling as is (the `StandardScaler` and `StackingClassifier` naturally handle them safely).
> * If you are adapting this code for **Standard Regression/Classification tasks** (e.g., predicting house prices), you should implement an outlier-removal step (such as IQR trimming or Isolation Forest) prior to the scaling step.
