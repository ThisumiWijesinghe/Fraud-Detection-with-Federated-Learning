 🏦 Fraud Detection with Federated Learning


📌 Project Overview

This project aims to build a fraud detection system for banking transactions using Machine Learning (ML) and Federated Learning (FL).

Problem: Online banking fraud is increasing worldwide. Traditional ML requires collecting sensitive customer data in one place, which risks privacy breaches.

Solution: Use Federated Learning so multiple banks can collaboratively train a model without sharing raw data. This preserves privacy while improving fraud detection.

💡 Example: Imagine 10 banks. Each trains its fraud model locally. Then, instead of sharing data, they only send their trained models to a server. The server performs federated averaging (FedAvg) to create one global model and sends it back. This way, fraud patterns seen in one bank can be learned by all banks — helping detect frauds that would otherwise be missed.

🎯 Project Goals

Detect fraudulent transactions accurately.

Compare centralized ML models with federated learning models.

Demonstrate privacy-preserving AI in financial fraud detection.

Enable knowledge sharing between banks without exposing sensitive data.

📊 Dataset

Name: PaySim Dataset

Size: ~6 million transactions

Features:

type – transaction type (CASH-IN, TRANSFER, etc.)

amount – transaction value

oldbalanceOrg – original balance before transaction

newbalanceOrig – balance after transaction

isFraud – fraud label (1 = Fraud, 0 = Legitimate)


❓ Why PaySim Dataset?

We selected PaySim because:

It contains millions of transactions, suitable for ML and FL training.

The dataset is well-structured and clean, so we can finish within our 3-week timeline.

It simulates real-world mobile banking fraud patterns.

Other datasets (e.g., IEEE-CIS) are very complex and require long preprocessing, not practical for our timeframe.

Using PaySim with Federated Learning is less common, so our approach will still be unique and impactful.


⚙️ Methodology

Data Preprocessing: Clean dataset and handle class imbalance (fraud cases are rare).

Baseline Models: Train centralized ML models (Random Forest, XGBoost, Neural Networks) for comparison.

Federated Learning Setup: Simulate multiple banks as separate clients and train using FedAvg.

Training & Evaluation: Compare centralized vs federated models using:

Precision, Recall, F1-score

Per-client performance metrics


Enhancements:

Implement secure aggregation for privacy.

Add Explainable AI (XAI) (SHAP or LIME) to interpret flagged transactions.


📈 Expected Outcomes

A robust fraud detection model with strong accuracy and recall.

Demonstrate the advantages of federated learning over centralized training for privacy and scalability.

Help banks detect fraud cases that may only appear in other institutions.

Provide explainable results to help banks understand flagged transactions.


🔑 Keywords

Machine Learning, Federated Learning, Fraud Detection, Banking Security, Privacy-Preserving AI, PaySim Dataset


📚 References / Literature

McMahan et al., “Communication-Efficient Learning of Deep Networks from Decentralized Data” (FedAvg).

Lopez et al., “PaySim: Mobile Money Payment Simulator” (2016).

Zheng et al., “Federated Meta-Learning for Fraudulent Credit Card Detection” (IJCAI 2020).

Bonawitz et al., “Practical Secure Aggregation for Federated Learning” (2016/2017).

