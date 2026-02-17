# 🔐 Network Traffic Threat Analysis & Risk-Based Attack Classification

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python)
![License](https://img.shields.io/badge/License-MIT-green)
![Build](https://img.shields.io/badge/Build-Passing-brightgreen)
![Issues](https://img.shields.io/github/issues/Sarwannandh67/Innofusionn-26)
![Stars](https://img.shields.io/github/stars/Sarwannandh67/Innofusionn-26?style=social)

---
<p align="center">
  <a href="https://github.com/Sarwannandh67/Innofusionn-26/blob/main/Network_Security_Analysis_Hackathon.ipynb">
    <img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/>
  </a>
</p>

---

## 📘 Executive Overview
This project presents a cybersecurity analytics workflow designed to analyze structured network telemetry, classify malicious behaviour, and prioritize threats using interpretable machine learning.  
The approach focuses on behavioural indicators — packet characteristics, anomaly scoring, protocol usage, and temporal activity — mirroring modern Security Operations Center (SOC) investigation practices.

## Domain
*Cyber Security*
---

## 🎯 Problem Context
Enterprise networks generate large volumes of telemetry that cannot be manually inspected.  
This analysis demonstrates how structured traffic data alone can:

- Detect abnormal behaviour patterns  
- Classify attack categories (DDoS, Intrusion, Malware)  
- Support risk-based threat prioritization  

---

## 📂 Dataset Scope
Each record represents a network event enriched with packet metadata, anomaly indicators, severity labels, and contextual logging attributes.

### Key Features
- Source Port / Destination Port  
- Protocol  
- Packet Length  
- Traffic Type  
- Anomaly Scores  
- Severity Level  
- Network Segment  
- Hour (derived from timestamp)  

Unstructured fields (payload data, raw IP addresses, firewall logs, IDS/IPS text entries) were excluded to maintain interpretability and prevent overfitting.

---

## 🧹 Data Preparation Strategy
- Converted timestamps into an **Hour** feature for temporal analysis  
- Removed high-cardinality log fields  
- Encoded categorical variables numerically  
- Filtered incomplete records  
- Retained only structured telemetry suitable for tabular ML models  

---

## 📊 Exploratory Data Analysis

### Attack Type Distribution
![Attack Type Distribution](images/Attack%20Type%20Distribution.png)

**Insight:** Attack categories are relatively balanced, enabling stable model learning.

---

### Protocol Usage by Attack Type
![Protocol Usage by Attack Type](images/Protocol%20Usage%20by%20Attack%20Type.png)

**Insight:** Protocol behaviour varies across attack classes, suggesting protocol-aware monitoring strategies.

---

### Anomaly Score Distribution Across Attack Types
![Anomaly Score Distribution](images/Anomaly%20Score%20Distribution%20Across%20Attack%20Types.png)

**Insight:** Higher anomaly score ranges consistently align with malicious traffic, validating anomaly scoring as a strong behavioural indicator.

---

## 🕒 Temporal Behaviour Analysis

### Overall Network Activity Timeline
![Overall Network Activity Timeline](images/Overall%20Network%20Activity%20Timeline.png)

**Observation:** Network activity fluctuates throughout the day, influencing baseline behaviour patterns.

---

### Attack Activity Timeline by Hour
![Attack Activity Timeline](images/Attack%20Activity%20Timeline%20by%20Hour.png)

**Observation:** Distinct spikes indicate potential automated or scripted attack behaviour.

---

### Detailed Attack Activity by Hour
![Attack Activity by Hour](images/Attack%20Activity%20by%20Hour.png)

**Observation:** Different attack types peak at different time windows, reinforcing the importance of time-aware monitoring.

---

## 🤖 Machine Learning Approach

### Model Selection
A **Random Forest Classifier** was chosen due to:
- Strong performance on structured cybersecurity data  
- Robustness to noisy features  
- Built-in explainability via feature importance  

### Training Workflow
- Dataset split into training and testing subsets  
- Model trained on behavioural telemetry  
- Performance evaluated using precision, recall, and F1-score metrics  

---

## 📈 Model Explainability

### Top Security Indicators (Feature Importance)
![Top Security Indicators](images/Top%20Security%20Indicators.png)

**Key Findings:**
- Packet Length and Anomaly Scores dominate predictive power  
- Source and Destination Ports contribute strongly to classification  
- Temporal feature (**Hour**) captures burst-based activity patterns  

---

## ⚠️ Risk-Based Threat Prioritization

### Risk Score Distribution by Severity
![Risk Score Distribution](images/Risk%20Score%20Distribution%20by%20Severity.png)

**Insight:** Higher severity levels align with elevated risk scores, supporting automated prioritization.

---

### Risk Levels Across Attack Types
![Risk Levels Across Attack Types](images/Risk%20Levels%20Across%20Attack%20Types.png)

**Insight:** Low-risk traffic dominates overall volume, while medium-risk clusters align with malicious patterns.

---

## 🔍 Key Security Insights
- Behavioural telemetry alone provides strong attack classification capability  
- Anomaly Scores combined with packet characteristics form reliable detection signals  
- Hour-based analysis reveals coordinated attack bursts  
- Risk scoring enables practical prioritization similar to enterprise SOC tooling  

---

## 🛡️ Strategic Security Recommendations
- Implement anomaly-threshold alerting pipelines  
- Prioritize response actions using computed risk levels  
- Monitor abnormal packet lengths and repeated port usage  
- Increase defensive monitoring during peak attack hours  
- Apply protocol-aware filtering rules to reduce exposure  

---

## ⚙️ Limitations
- Payload-level inspection was intentionally excluded  
- Dataset reflects offline analysis rather than real-time deployment  
- IP-level behavioural profiling was not used to avoid overfitting  

---

## 🚀 Future Enhancements
- Integrate streaming telemetry for real-time detection  
- Apply anomaly detection models such as Isolation Forest  
- Perform NLP-based analysis on firewall and payload logs  
- Deploy interactive SOC dashboards for continuous monitoring  

---

## ✅ Conclusion
This project demonstrates that structured network telemetry, when analyzed using interpretable machine learning and temporal behavioural analytics, can generate actionable cybersecurity intelligence.  
The integration of feature importance, risk scoring, and timeline analysis reflects modern enterprise threat detection workflows.
