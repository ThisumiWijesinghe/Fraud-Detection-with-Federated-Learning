# Federated Fraud Detection using FedAvg and FedBN

## 📌 Project Overview

This project implements a **Federated Learning–based fraud detection system** using the **PaySim dataset**. The goal is to simulate a real-world banking scenario where **12 banks (clients)** collaboratively train a fraud detection model **without sharing raw data**.

We use **Deep Neural Networks (DNNs)** and compare two federated learning strategies:

* **FedAvg (Federated Averaging)**
* **FedBN (Federated Batch Normalization – optional extension)**

The dataset is split across clients in a **Non-IID manner using Dirichlet distribution**, which reflects realistic data heterogeneity among banks.

---

## 🏦 Problem Setting

* Each bank has its **own transaction data**
* Fraud patterns are **different for each bank**
* Data privacy is preserved (no raw data sharing)
* A central **server coordinates model aggregation**

---

## 📊 Dataset

* **Name:** PaySim – Simulated Mobile Money Transactions
* **Source:** Kaggle (`ealaxi/paysim1`)
* **Size:** ~6.3 million transactions
* **Target Variable:** `isFraud`

### Selected Features

* `step`
* `type` (encoded)
* `amount`
* `oldbalanceOrg`
* `newbalanceOrig`
* `oldbalanceDest`
* `newbalanceDest`

---

## 🔀 Data Distribution (Non-IID)

* Number of clients: **12 (banks)**
* Data split method: **Dirichlet distribution**
* Alpha (α): Controls degree of non-IID (smaller α → more skewed)
* Fraud samples are **unevenly distributed** across banks

This setup closely matches **real-world banking environments**.

---

## 🧠 Model Architecture (DNN)

Each client trains the same Deep Neural Network locally:

* Input layer
* Dense layer (ReLU)
* Dense layer (ReLU)
* Output layer (Sigmoid)

Loss Function:

* Binary Cross Entropy

Optimizer:

* Adam

---

## 🔁 Federated Learning Workflow (FedAvg)

1. The **server initializes an empty global model**
2. The server sends the global model to all 12 clients
3. Each client:

   * Trains the model using its **local data**
   * Uses **1 local epoch**
4. Clients send updated model weights back to the server
5. The server **averages the weights (FedAvg)**
6. The updated global model is redistributed
7. Steps 3–6 are repeated for **5 global rounds**

---

## 📈 Evaluation Strategy

* Metric used: **Accuracy**
* Evaluation is performed:

  * **Client-wise (per bank)**
  * After **each global round**
* Average accuracy across all clients is also reported

---

## 🧪 Experimental Setup

* Number of clients: 12
* Global rounds: 5
* Local epochs: 1
* Batch size: 1024
* Learning rate: 0.001

---

## ✅ Key Outcomes

* Demonstrates **privacy-preserving fraud detection**
* Shows impact of **Non-IID data** on federated models
* Provides a strong baseline using **FedAvg**
* Can be extended to **FedBN for better personalization**

---

## 🚀 Future Work

* Implement **FedBN** and compare with FedAvg
* Add fraud-focused metrics (Recall, Precision)
* Visualize performance across global rounds
* Test with different Dirichlet α values

---

## 🛠️ Technologies Used

* Python
* TensorFlow / Keras
* NumPy, Pandas
* Scikit-learn
* KaggleHub

---

## 📌 Note

This project is designed for **academic and research purposes**, focusing on federated learning concepts applied to financial fraud detection.


