# 🏦 Fraud Detection with Federated Learning

## 📌 Project Overview
This project aims to build a **fraud detection system** for banking transactions using **Machine Learning (ML)** and **Federated Learning (FL)**.

- **Problem:** Online banking fraud is increasing. Traditional ML requires collecting sensitive customer data in one place, which risks privacy breaches.  
- **Solution:** Use **Federated Learning** so multiple banks can collaboratively train a model **without sharing raw data**. This preserves privacy while improving fraud detection.

---

## 🎯 Project Goals
- Detect fraudulent transactions accurately.  
- Compare **centralized ML models** with **federated learning models**.  
- Demonstrate **privacy-preserving AI** in financial fraud detection.

---

## 📊 Dataset
- **Name:** [PaySim Dataset](https://www.kaggle.com/datasets/ntnu-testimon/paysim1)  
- **Size:** ~6 million transactions  
- **Features:**  
  - `type` – transaction type (CASH-IN, TRANSFER, etc.)  
  - `amount` – transaction value  
  - `oldbalanceOrg` – original balance before transaction  
  - `newbalanceOrig` – balance after transaction  
  - `isFraud` – fraud label (1 = Fraud, 0 = Legitimate)  

---

## ⚙️ Methodology
1. **Data Preprocessing:** Clean dataset and handle class imbalance (fraud cases are rare).  
2. **Baseline Models:** Train centralized ML models (Random Forest, XGBoost, Neural Networks) for comparison.  
3. **Federated Learning Setup:** Simulate multiple banks as separate clients and train using **FedAvg**.  
4. **Training & Evaluation:** Compare centralized vs federated models using:  
   - Precision, Recall, F1-score  
   - Per-client performance metrics  
5. **Enhancements:** Implement **secure aggregation** for privacy and optionally **Explainable AI (XAI)** using SHAP or LIME to interpret flagged transactions.

---

## 📈 Expected Outcomes
- A robust fraud detection model with strong accuracy and recall.  
- Demonstrate the advantages of **federated learning** over centralized training for privacy and scalability.  
- Provide explainable results to help banks understand flagged transactions.

---

## 🔑 Keywords
`Machine Learning`, `Federated Learning`, `Fraud Detection`, `Banking Security`, `Privacy-Preserving AI`, `PaySim Dataset`

---

## 📚 References / Literature
1. McMahan et al., “Communication-Efficient Learning of Deep Networks from Decentralized Data” (FedAvg).  
2. Lopez et al., “PaySim: Mobile Money Payment Simulator” (2016).  
3. Zheng et al., “Federated Meta-Learning for Fraudulent Credit Card Detection” (IJCAI 2020).  
4. Bonawitz et al., “Practical Secure Aggregation for Federated Learning” (2016/2017).  

