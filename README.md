# Real_Time_Streaming_Data_Pipeline_on_GCP
This project focuses on implementing a real-time streaming data ingestion pipeline into BigQuery using GCP native services and Python. The primary objective is to demonstrate real-time streaming ingestion, transformation using Python UDFs, and analytical storage into BigQuery. The data used for streaming is mock IRCTC booking data.

---

## Architecture

The architecture involves data publishing to a Pub/Sub topic, real-time data processing using Dataflow with a Python UDF for transformation, and ingestion into a target BigQuery table for downstream analytical consumption.

![Data Architecture](/Data_Architecture.jpg)

---

## Tech Stack Used
- **Google Cloud Pub/Sub** → Real-time data ingestion and event streaming
- **Google Dataflow (Apache Beam)** → Stream processing and transformation engine  
- **Google BigQuery** → Scalable data warehouse for storing and analyzing processed data 
- **Google Cloud Storage** → Stores UDF scripts and any intermediate files  
- **Python** → Used for generating mock streaming data and implementing UDFs for custom transformation logic during stream processing.
- **SQL** → Data transformation & querying in BigQuery  

---

## Setup Instructions

### 1. Clone the Repository
```bash
git clone https://github.com/Ishant0091/Real_Time_Streaming_Data_Pipeline_on_GCP.git
cd Real_Time_Streaming_Data_Pipeline_on_GCP
```

### 2. Create Pub/Sub Topic
Create Pub-Sub topic named as `irctc_data` with default subscriber.

### 3. Set GCP Environment Variables in the Script
Update the following environment variables in the `irctc_mock_data_to_pubsub.py` script before running it:

```python
PROJECT_ID = "your-gcp-project-id"
TOPIC_ID = "pub/sub-topic-name"  # e.g., "irctc_data"
```

### 4. Setup for Publishing Events to GCP Pub/Sub (Local system)

#### 🔹 Python Package Installation
Install the required Pub/Sub client library:
```bash
pip3 install google-cloud-pubsub
```

#### 🔹 Install Google Cloud SDK
Ensure the Google Cloud SDK is installed to access gcloud CLI commands.

#### 🔹 Authenticate GCP Account in Terminal
Run the following command to authenticate:
```bash
gcloud auth application-default login
```
This will open a browser window — select the GCP account email you wish to use.

#### 🔹 Assign IAM Roles
In IAM & Admin:

Assign the following roles to your GCP user/email:
- Pub/Sub Publisher
- Pub/Sub Subscriber
  
This ensures you have the required permissions to publish and consume messages.

### 5. BigQuery Initial Setup

#### ✅ Enable Required APIs

When using **BigQuery** for the first time in a project, you will be prompted to enable the necessary APIs.  
👉 Make sure to enable all required APIs when prompted to ensure BigQuery and related services function properly.

#### 🔹 Create BigQuery Dataset
Create a dataset named `irctc_dwh` in your GCP project. This will serve as the **data warehouse** where your transformed streaming data will be stored.

#### 🔹 Assign Required IAM Roles

Grant the following roles to the **Service Account** associated with your application or Dataflow job. These roles are necessary for interacting with GCP services:

- `BigQuery Admin`
- `Dataflow Admin`
- `Pub/Sub Admin`


### 6. Upload Python UDF Script to GCS
You can upload your UDF script (`transform_udf.py`) to a **Google Cloud Storage** bucket using the **Google Cloud Console**.

#### 📁 Upload Location:
Place the file inside the following folder path in your bucket:  
`gs://your-bucket-name/pubsub-to-bigquery/`

Make sure the bucket path (your-bucket-name) exists and is accessible.

### 7. Create a Dataflow Job (Streaming)
Use the **Google Cloud Console** to create a streaming Dataflow job using the built-in template:  
**"Pub/Sub to BigQuery with Python UDFs"**

#### 📌 Configuration Details:

- **Source Parameters -> Input Pub/Sub Topic**: "pub/sub-topic-name"  # e.g., "irctc_data"` (your Pub/Sub topic)
- **Target -> BigQuery Output Table**: "<gcp-project-name>.<dateset-name>.<table-name>"  `irctc_stream_tb` (your BigQuery table)
- **Cloud Storage path to python UDF source**: GCS path to your uploaded Python UDF script 

   Example:  
  `gs://your-bucket-name/pubsub-to-bigquery/transform_udf.py`

*This template reads real-time data from Pub/Sub, applies transformation using the Python UDF, and writes the results into BigQuery.*

## 8. Run the Publisher
```bash
python irctc_mock_data_to_pubsub.py
```

This script will:

* Generate mock booking activity data
* Encode as JSON
* Publish to `irctc-data` topic on Pub/Sub

---

## Learnings

- Implemented a real-time streaming data pipeline using **Google Pub/Sub**, **Dataflow**, and **BigQuery**
- Gained hands-on experience with **Python UDFs** for applying custom transformations on streaming data
- Learned how to manage **GCP IAM roles** and service account permissions for secure resource access
- Worked with **Google Cloud Storage (GCS)** to store and reference transformation scripts
- Developed end-to-end skills in building **scalable, serverless, streaming pipelines** on GCP

---

### 🔗 Connect With Me

- [LinkedIn](https://www.linkedin.com/in/ishant-kumar-534989233)

 Tags
#GoogleCloud #Dataflow #PubSub #BigQuery #GCS #Python #ApacheBeam #RealTimeStreaming #DataEngineering #CloudPipeline #GCP #UDF #CloudAutomation #Serverless


