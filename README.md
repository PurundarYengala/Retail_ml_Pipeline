# Retail_ml_Pipeline
End-to-end machine learning pipeline using Amazon SageMaker for predicting retail sales. Includes data preprocessing, model training with XGBoost, deployment as a real-time endpoint, testing via notebooks, and future integration with Prometheus-Grafana for monitoring.
////
# 🧠 Retail Sales Prediction ML Pipeline

This repository contains an end-to-end machine learning pipeline for predicting retail sales using Amazon SageMaker and AWS services. It includes data processing, model training with hyperparameter tuning, deployment as a real-time endpoint, and testing via notebook instances. The model is based on XGBoost and optimized using Bayesian techniques.

---

## 📦 Project Structure

retail-ml-pipeline/
├── config/
│ └── hyperparams.json # All hyperparameters used in XGBoost training
├── notebooks/
│ └── test_endpoint.ipynb # Inference notebook used for testing the model
├── models/
│ └── endpoint_info.txt # Metadata about the deployed endpoint
├── scripts/
│ └── deploy.md # Deployment steps followed using AWS Console
│ └── monitor.md # Steps to set up monitoring with CloudWatch / Prometheus
├── data/
│ └── s3_paths.txt # S3 locations of raw/processed/trained data
├── README.md # This file

markdown
Copy
Edit

---

## 🚀 Pipeline Overview

### 📁 1. Data Ingestion
- Data is stored in: `s3://retail.sales.lp/processed/`
- Format: CSV
- Three parts used: possibly train, validation, test
- `date` and `warehouse_sales` used as input features
- `retail_sales` is the target label

### 🧠 2. Model Training (XGBoost)
- Platform: Amazon SageMaker built-in algorithm
- Objective: `reg:squarederror`
- Evaluation metric: `rmse`
- Training job name: `retail-xgboost-training-copy-06-11`
- Training output: `s3://retail.sales.lp/output/.../model.tar.gz`
- Instance type: `ml.m4.xlarge`

### 🔍 3. Hyperparameter Tuning
- Bayesian Optimization used for tuning
- Key tuned parameters:
  - `max_depth`: 6
  - `eta`: 0.3
  - `lambda`: 1.0
  - `subsample`: 1.0
  - `num_round`: 50
- Full config available in [`config/hyperparams.json`](./config/hyperparams.json)

### ⚙️ 4. Model Deployment
- Deployed as a **real-time endpoint**
- Model name: `retail-xgboost-model-v1`
- Endpoint name: `retail-xgboost-endpoint`
- Instance type: `ml.t2.medium`
- Deployment done via AWS Console

### 🧪 5. Testing
- Notebook instance used to test predictions
- Test input format: `"warehouse_sales"` or `"year,month,warehouse_sales,..."`
- Notebook: [`notebooks/test_endpoint.ipynb`](./notebooks/test_endpoint.ipynb)

### 📈 6. Monitoring
- Enabled CloudWatch metrics for:
  - `Invocations`
  - `ModelLatency`
  - `4XX/5XX Errors`
- Plan to set up **Grafana dashboard** using Prometheus + CloudWatch exporter

---

## 📊 Sample Output

Example test input:

```python
payload = "8.0"
Returns prediction like:

makefile
Copy
Edit
Prediction: 12.67
🛠 Future Improvements
Enable automated re-training using SageMaker Pipelines

Integrate with Amazon Model Monitor for drift detection

Automate via Terraform/CDK

Full Grafana dashboard via Prometheus exporter

📬 Contact
Owner: Purundar Yengala Madhusudhan Rao
Email: purundar.yengalamadhusudhanrao@my.liu.edu
Location: Hillsboro, OR, USA

