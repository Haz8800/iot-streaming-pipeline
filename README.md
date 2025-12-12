# IoT Streaming Pipeline – ICS 474 Big Data Project

This repository contains my full end-to-end big data pipeline for ICS 474 (Big Data Analytics).  
The pipeline simulates IoT sensors, streams the data, processes it using Spark Structured Streaming, stores the results, visualizes insights, and applies machine learning anomaly detection.

Everything was implemented inside Google Colab using a Kafka-like file buffer because Colab cannot run Kafka brokers or background services.

---

## 📌 Project Overview

This end-to-end pipeline includes:

- **Simulated IoT Data Producer**  
- **Kafka-like Buffering Layer** (file-based event stream)  
- **Spark Structured Streaming**  
- **Time-windowed Aggregation with Watermarking**  
- **Storage using Parquet Format**  
- **Interactive Visualization (Plotly)**  
- **ML Anomaly Detection using IsolationForest**  

This satisfies all required components for ICS 474 and includes the optional ML bonus.

---

## 📌 Architecture Diagram

IoT Producer → Input Folder (Simulated Kafka Buffer) → Spark Structured Streaming

↓ ↓

JSON Message Files Window Aggregation (10s)

↓ ↓

Storage Layer (Parquet) ← ML (IsolationForest)

↓

Visualization (Plotly Dashboards)


---

## 📌 Why Kafka Was Simulated

Google Colab does **not** allow:

- background services  
- open ports  
- Zookeeper or Kafka brokers  
- long-running daemons  

So the **input folder acts as a Kafka-like message buffer**.  
Spark Structured Streaming treats new JSON files in the folder as incoming streaming events.

This satisfies the course requirement of:

> “Kafka or a similar messaging platform.”

---


---

## 📌 How to Run the Pipeline (Google Colab)

1. Open the notebook:  
   `notebooks/ICS474Project.ipynb`

2. Run all cells in order:
   - Install dependencies  
   - Initialize Spark  
   - Start the IoT producer  
   - Launch Spark Structured Streaming  
   - Wait for processing  
   - Load Parquet results  
   - Visualize dashboards  
   - Run ML anomaly detection  

3. View the generated:
   - Time-series subplots  
   - Boxplots  
   - Anomaly-highlighted visualizations  
   - Anomaly-only scatter plots  

4. All outputs are automatically saved inside:
/content/iot_stream_pipeline/artifacts/


---

## 📌 Sample Visualizations

### 📊 Temperature Trends per Device (Subplots)
![Temperature Subplots](artifacts/charts/Temp%20trend%20per%20device%20%28subplots%29.png)


### 📈 Temperature Distribution (Boxplot)
*Saved in artifacts/charts/*

### 🔥 Anomalies Detected (IsolationForest)
*Saved in artifacts/charts/*

---

## 📌 ML Component (Bonus)

Algorithm:  
**IsolationForest**

Features used:  
- `avg_temperature`  
- `avg_humidity`  

The model labels each window as:
- **0 → Normal**
- **1 → Anomaly**

These anomalies are visualized clearly in the notebook.

---

## 📌 Credits

Developed as part of:

**ICS 474 – Big Data Analytics**  
King Fahd University of Petroleum and Minerals  
Fall 2025



