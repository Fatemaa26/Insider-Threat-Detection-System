# Intelligent Insider Threat Detection System

A supervised machine learning classification pipeline designed to analyze corporate employee activity metrics, map behavior patterns, and predict potential insider security risks.

## 🔍 Pipeline Architecture & Strategy
1. **Data Imputation & Preprocessing:** Artificially introduced and handled missing data to demonstrate clean data-recovery pipelines.
2. **Feature Encoding:** Converted categorical profile metrics into numeric formats.
3. **Feature Selection:** Dropped highly redundant/highly correlated columns using a customized block filter to focus on distinct, high-quality feature sets (evaluated via Mutual Information and ANOVA F-scores).
4. **Data Scaling:** Leveraged `StandardScaler` to safeguard linear/distance-based models against mathematical distortion from extreme behavioral spikes without deleting critical threat signatures.
5. **Ensemble Stacking:** Combined tree-based models immune to outlier distortion (**XGBoost**, **Random Forest**) with distance-based structures (**KNN**) feeding into a **Logistic Regression** meta-learner.

## 📊 Performance Metrics

### Final Ensemble Model
* **Final Stacking Classifier AUC-ROC Score:** `0.9858` *(Our absolute top-performing architecture)*

### 📈 Baseline Individual Classifiers Evaluated
To construct the highest quality meta-learner, multiple standard classifications were evaluated independently on the dataset:

* **K-Nearest Neighbors (KNN):**
  * Training Accuracy: `0.9809`
  * Test Accuracy: `0.9723` *(Demonstrates exceptional generalization with zero overfitting)*
* **XGBoost Classifier:** Test Accuracy: `0.9577`
* **Random Forest Classifier:** Test Accuracy: `0.9546`
* **Decision Tree Classifier:** Test Accuracy: `0.9255`
* **Support Vector Machines (SVM):** Test Accuracy: `0.8931`
* **Logistic Regression:** Test Accuracy: `0.8752`

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
> * If you are adapting this code for **Security, Fraud, or Intrusion Detection**, leave the outlier handling as it is (the `StandardScaler` and `StackingClassifier` naturally handle them safely).
> * If you are adapting this code for **Standard Regression/Classification tasks** (e.g., predicting house prices), you should implement an outlier-removal step (such as IQR trimming or Isolation Forest) prior to the scaling step.

## 👥 Project Team
* **Developers:** Jana Mohamed, Ganna Mohamed, and Abd Al-Hamid.
* **Supervisors:** Dr. Heba Zaki and Dr. Yasmeen Abdelmohsen.
