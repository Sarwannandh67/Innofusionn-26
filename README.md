# Network Traffic Threat Analysis & Risk-Based Attack Classification

## Executive Summary

This project implements a structured cybersecurity analytics pipeline to analyze network traffic telemetry, detect malicious behavior, and prioritize threats using a risk-based approach.
The solution combines exploratory data analysis, interpretable machine learning, and temporal behavior analysis to mirror how modern Security Operations Centers (SOC) investigate and triage network threats.

Rather than relying on deep packet inspection, the analysis focuses on **behavioral indicators** such as packet characteristics, anomaly scores, protocol usage, and time-based activity—aligning with scalable, real-world security monitoring practices.

---

## Problem Statement

Enterprise networks generate massive volumes of traffic logs, making manual inspection infeasible.
Security teams require automated mechanisms to:

* Identify suspicious traffic patterns
* Classify attack behavior accurately
* Prioritize alerts based on operational risk

This project evaluates whether **structured network telemetry alone** can support effective attack classification and actionable security insights.

---

## Dataset Overview

Each row in the dataset represents a discrete network event enriched with packet metadata, anomaly indicators, severity labels, and contextual attributes.

### Key Analytical Features

* Source Port / Destination Port
* Protocol
* Packet Length
* Packet Type
* Traffic Type
* Anomaly Scores
* Severity Level
* Network Segment
* Hour (derived from timestamp)

### Excluded Fields

Unstructured and high-cardinality fields such as raw IP addresses, payload data, firewall logs, and IDS/IPS text logs were excluded to avoid noise, overfitting, and reduced interpretability.

---

## Data Preparation & Feature Engineering

The preprocessing pipeline included:

* Timestamp transformation into an **hour-based temporal feature**
* Removal of unstructured log-heavy columns
* Encoding of categorical variables into numerical form
* Filtering of incomplete records
* Selection of features suitable for tabular machine learning models

This ensured a clean, interpretable, and ML-ready dataset.

---

## Exploratory Data Analysis (EDA)

### Attack Type Distribution

Understanding class balance and attack prevalence.

```md
![Attack Type Distribution](images/attack_type_distribution.png)
```

**Observation:**
Attack categories are unevenly distributed, highlighting the importance of precision and recall during evaluation.

---

### Anomaly Score Behavior Across Attacks

```md
![Anomaly Score vs Attack Type](images/anomaly_score_attack_type.png)
```

**Observation:**
Higher anomaly scores consistently align with malicious traffic, validating anomaly metrics as strong early indicators.

---

### Protocol Usage by Attack Type

```md
![Protocol vs Attack Type](images/protocol_attack_pattern.png)
```

**Observation:**
Certain protocols show stronger association with specific attack behaviors, suggesting protocol-aware monitoring is valuable.

---

## Machine Learning Approach

### Model Selection

A **Random Forest Classifier** was used due to its suitability for structured cybersecurity data:

* Handles mixed numerical and categorical features
* Robust to noise
* Provides transparent feature importance

### Training Strategy

* Dataset split into training and test subsets
* Model trained on engineered behavioral features
* Performance evaluated using standard classification metrics

---

## Model Performance

### Classification Metrics

```md
![Classification Report](images/classification_report.png)
```

The model achieved balanced performance across attack classes, demonstrating reliable detection capability using structured telemetry alone.

---

### Feature Importance Analysis

```md
![Feature Importance](images/feature_importance.png)
```

**Top Influential Features Identified:**

* Packet Length
* Anomaly Scores
* Source Port
* Destination Port
* Hour

These features represent behavioral deviations commonly associated with malicious activity.

---

## Risk Scoring & Threat Prioritization

To simulate real SOC workflows, a **risk scoring mechanism** was implemented by combining:

* Anomaly Scores
* Packet Length
* Port behavior

Traffic was categorized into **Low**, **Medium**, and **High** risk tiers.

```md
![Risk Level Distribution](images/risk_level_distribution.png)
```

This enables prioritization of alerts rather than treating all detections equally.

---

## Temporal Attack Analysis (SOC-Style Timeline)

```md
![Attack Timeline by Hour](images/attack_timeline.png)
```

**Insights:**

* Distinct attack bursts occur during specific hours
* Patterns suggest automated or scripted attack behavior
* Time-aware monitoring improves detection effectiveness

---

## Key Security Insights

* Anomaly Scores are the strongest predictors of malicious activity
* Packet Length and port behavior reveal abnormal data flows
* Time-based patterns expose coordinated or automated attacks
* Severity levels align closely with computed risk scores

---

## Security Recommendations

Based on the findings:

* Deploy anomaly-threshold-based alerting mechanisms
* Prioritize incident response using computed risk levels
* Monitor abnormal packet sizes and repeated port activity
* Increase vigilance during peak attack hours
* Apply protocol-aware defensive controls

---

## Limitations

* Payload and deep packet inspection were not performed
* No real-time streaming or live deployment implemented
* IP reputation and behavioral profiling were excluded

---

## Future Enhancements

* Integrate real-time traffic ingestion and alerting
* Apply anomaly detection models (e.g., Isolation Forest)
* Perform NLP-based analysis on payload and firewall logs
* Deploy interactive dashboards for SOC analysts

---

## Conclusion

This project demonstrates that structured network telemetry, when analyzed systematically, can provide strong attack detection capability and meaningful operational insights.
By combining interpretable machine learning, risk-based prioritization, and temporal analysis, the solution reflects practical cybersecurity monitoring strategies used in modern enterprise environments.

---

### 📌 Note on Visuals

All figures referenced above correspond to plots generated in the accompanying Google Colab notebook and should be exported and placed in the `/images` directory before final submission.

