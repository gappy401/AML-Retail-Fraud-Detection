# Financial Transaction Anomaly Detection Engine
### **Snowflake MLOps Pipeline with Snowpark & Isolation Forest**



## Project Overview
This repository implements a production-ready MLOps system within the **Snowflake Data Cloud**. By utilizing **Snowpark Python**, the entire ML lifecycle—from feature engineering to real-time inference—is executed natively inside Snowflake, ensuring enterprise-grade security and zero-copy data architecture.

### **Business Impact**
* **Detection Rate:** Increased identification of suspicious activities by **33%**.
* **Precision:** Reduced False Positive Rates by **20%** via refined threshold tuning ($score < -0.06$).
* **Efficiency:** Automated risk-triage workflows, cutting investigation lead time by **40%**.

---

## Technical Architecture
The pipeline follows a serverless architecture, eliminating the latency and security risks associated with moving data to external compute environments.

* **Ingestion:** Automated streaming from **AWS S3** via **Snowpipe**.
* **Feature Engineering:** Scale-out processing of transaction velocity and behavioral aggregates using **Snowpark DataFrames**.
* **Modeling:** **Isolation Forest** (Scikit-learn) trained and serialized to a Snowflake Stage.
* **Deployment:** Model operationalized as a permanent **Python UDF** for real-time, in-warehouse scoring.
* **Orchestration:** **Snowflake Tasks** trigger incremental hourly scoring and risk tiering (High/Med/Low).
* **Analytics:** Dynamic SQL views powering a [Live Tableau Dashboard](https://public.tableau.com/app/profile/nandita.ghildyal4373/viz/Fraud-Detection_17621216990630/Dashboard1).

---

## Repository Structure

| Folder | Description |
| :--- | :--- |
| `Setup/` | SQL DDL for environment configuration (Stages, Snowpipe, RBAC). |
| `Modeling/` | Snowpark Python scripts for feature engineering and model training. |
| `Automation/` | Implementation of the Python UDF and scheduled Snowflake Tasks. |
| `View/` | SQL logic for the final reporting layer and risk-level tiering. |

---

## Tech Stack
* **Language:** Python (Snowpark), SQL
* **Cloud:** Snowflake, AWS (S3)
* **ML Libraries:** Scikit-learn (Isolation Forest), Joblib
* **Visualization:** Tableau

---

### **How to Deploy**
1.  Execute `Setup/` scripts to initialize the Snowflake environment.
2.  Run `Modeling/` to train the model and upload the `.joblib` file to the Snowflake stage.
3.  Deploy the scoring logic via `Automation/` to create the **Python UDF**.
4.  Activate the **Snowflake Task** to begin hourly automated inference.
