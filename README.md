# Privacy-Preserving Fraud Detection using Federated Learning

##Project Overview
This project presents a **Privacy-Preserving Fraud Detection System** built using **Deep Neural Networks (DDNs)** and  **Federated Learning (FL)**. The goal is to enable multiple financial institutions (clients) to collaboratively train a highly accurate fraud detection model without ever sharing sensitive, raw customer transaction data.

To simulate real-world financial networks, the system was evaluated on two distinct datasets:
1. **PaySim:** Synthetic mobile money transactions.
2. **Credit Card Fraud Dataset:** Real-World anoymized credit card data.

## Architecture & Data Preparation
### 1. Data Partitioning (The Challenge)
In reality, no two banks share the exact same transaction behavior (Non-IID). To emulate this **Statistical Heterogeneity**, the training data was split among **12 clients** using a **Dirichlet Distribution ($\alpha = 0.5$)**. However, to ensure fair evaluation, the *test data* was kept stictly independent and identically distributed (IID).

### 2. Local Deep Neural Network (DNN) Design
Each client trains a local DNN model characterized by the following parameters:
* **Training Specs:** 5 Epochs per global round | Batch size: 1024
* **Network Layers:**
  - Input Layer (Feature Scaled)
  - Dense Layer (64 neurons, ReLU)
  - **Batch Normalization Layer**
  - Dense Layer (32 neurons. ReLU)
  - Output Layer (1 neuron, Sigmoid for Binary Classification)

  ## Federated Training Strategies Evaluated
  We explored and benchmarked three distict training strategies:

  ### 1. Local Training (No FL Baseline)
  Clients trained their local NNs independently on their isolated Non-IID datasets without any collaboration. This served as our performance baseline.

  ### 2. Federated Averaging (FedAvg)
  Clients trained locally and periodically sent their model weights to a central server. The server aggregate these weights based on the sample size of each client.

  **Mathematical Formulation of FedAvg:**
  $$w^{(t+1)} = \sum_{k=1}^{K} \frac{n_k}{n} w_k^{(t)}$$
*(where $w^{(t+1)}$ is the updated global weights, $w_k^{(t)}$ are the local weights of client $k$ at round $t$, $n_k$ is the client sample size, and $n$ is the total sample size across all clients).*

### 3. Federated Batch Normalization (FedBN) [Proposed]
Designed explicitly for highly Non-IID distributions, FedBN preserves the client-specific **Batch Normakization (BN) statistics** locally while averaging only the non-BN weights (Dense layers) across the network. This allows the model to "Personalize" its learning to the local bank's unique data distribution while still benefiting from global knowledge.

## Key Findings & Results
After rigorous evaluation on the IID test sets, the results conclusively demonstrated:
- Collaborative Advantage: Both federated approaches (FedAvg and FedBN) consistently outperformed isolated local training.
- Handling Heterogeneity: FedBN provided a distinct advantage in scenarios with highly non-IID training data, proving its effectiveness in maintaining stability and accuracy when data distributions vary wildly between banks.
- Privacy Assurance: The workflow guarantees data privacy by transmitting only model gradients (weights) instead of personally identifiable information (PII).

## Keywords
`Federated Learning` `Fraud Detection` `FedBN` `Deep Neural Networks` `Privacy preserving Machine Learning` `Non-IID` `Dirichlet Distribution` `PaySim` `Financial Technology (FinTech`

## References
[1] B.McMahan, E.Moore, D.Ramage, S.Hampson and B.A.yArcas, “Comunication-Efficient Learning of Deep Networks from Decentralized Data,” in Proceedings of the 20th International Conference on Artificial Intelligence and Statistics (AISTATS), 2017.

[2] T. Li, A. S. Sahu, M. Zaheer, M. Sanjabi, A. Talwalkar and V. Smith, “Federated Optimization in Heterogeneous Networks,” in Proceedings of Machine Learning and Systems  (MLSys), 2020.

[3] X. Li, M. Huang, Y. Yang, S. Wang and Z.Zhang, “On the Convergence of FedAvg on Non-IID Data,” International Conference on Learning Representations (ICLR), 2020.

[4] S. Ioffe and C. Szegedy, “Batch Normalization: Accelerating Deep Neural Network Training by Reducing Internal Covariate Shift,” in Proceedings of the International Conference on Machine Learning (ICML), 2015.

[5] X. Li, Y. Jiang, M.Zhang, X. Kamp and Q. Dou, “FedBN: Federated Learning on Non-IID Features via Local Batch Normalization,” in International Conference on Learning Representations (ICLR), 2021.

[6] I. Goodfellow. Y. Bengio and A. Courville, Deep Learning, Cambridge, MA, USA: MIT Press, 2016.

[7] C. C. Aggrawal, Neural Networks and Deep Learning: A Textbook, Cham, Switzerland: Springer, 2018.

[8] D. P. Kingma and J. Ba, “Adam: A Method for Stochastic Optimization," International Conference on Learning Representations (ICLR), 2015.
