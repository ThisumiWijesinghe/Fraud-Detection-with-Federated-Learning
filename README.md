# Privacy-Preserving Fraud Detection using Federated Learning

##Project Overview
This project presents a **Privacy-Preserving Fraud Detection System** built using **Deep Neural Networks (DDNs)** and  **Federated Learning (FL)**. The goal is to enable multiple financial institutions (clients) to collaboratively train a highly accurate fraud detection model without ever sharing sensitive, raw customer transaction data.

To simulate real-world financial networks, the system was evaluated on two distinct datasets:
1. **PaySim:** Synthetic mobile money transactions.
2. **Credit Card Fraud Dataset:** Real-World anoymized credit card data.

To improve computational efficiency and feasibility in a constrained environment, the PaySim dataset was reduced from approximately 6 million records to 1 million records, while ensuring that all fraud cases were preserved. This maintains the integrity of fraud detection while reducing training time.

## Architecture & Data Preparation
### 1. Data Partitioning (The Challenge)
In reality, no two banks share the exact same transaction behavior (Non-IID). To emulate this **Statistical Heterogeneity**, the training data was split among **12 clients** using a **Dirichlet Distribution **(alpha = 0.5$)**. 

However, to ensure fair evaluation, the *test data* was kept stictly independent and identically distributed (IID).
Additionally, random seed initialization was applied across Numpy, TensorFlow, and python to ensure reproducibility and consistent experimental results across multiple runs.

### 2. Local Deep Neural Network (DNN) Design
Each client trains a local DNN model characterized by the following parameters:
* **Training Specs:** 5 Epochs per global round | Batch size:
* PaySim: 1024
* Credit Card Dataset: 512
* **Network Layers:**
  - Input Layer (Feature Scaled)
  - Dense Layer (64 neurons, ReLU)
  - **Batch Normalization Layer**
  - Dense Layer (32 neurons. ReLU)
  - Output Layer (1 neuron, Sigmoid for Binary Classification)
 
    Batch Normalization layers were specifically included to stablize training and were later leveraged in the FedBN approach to handle Non-IID data effectively.

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
fedBN preserves client-specific Batch Normalization statistics locally while averaging only the non-BN layers.

This approach allows each client model to adapt to its own data distribution while still benefiting from shared global knowledge, making it highly effective under Non-IID conditions.

## Key Findings & Results
After rigorous evaluation on the IID test sets, the results conclusively demonstrated:
- Collaborative Advantage: Both federated approaches (FedAvg and FedBN) consistently outperformed isolated local training.
- Handling Heterogeneity: FedBN provided a distinct advantage in scenarios with highly non-IID training data, proving its effectiveness in maintaining stability and accuracy when data distributions vary wildly between banks.
- Privacy Assurance: The workflow guarantees data privacy by transmitting only model gradients (weights) instead of personally identifiable information (PII).

Additional evaluation metrics such as Precision, Recall, F1-score, and Loss were incorporated tobetter assess model performance on highly imbalanced fraud datasets, where accuracy alone can be misleading.

System Implementation Enhancements

To improve performance and scalability, GPU acceleration (TPU v2 / T4 GPU via Google Colab Pro) was utilized specifically for the PaySim dataset due to its large size. The Credit Card dataset was efficiently processed using CPU resources.

Memory optimization techniques such as float 32 data types and garbage collection (gc.collect()) were applied to handle large-scale training without crashes.

Training results, including accuracy, loss, precision, recall, and F1-score, were exported into csv files for both datasets to support visualization and analysis.

## Keywords
`Federated Learning` `Fraud Detection` `FedBN` `Deep Neural Networks` `Privacy preserving Machine Learning` `Non-IID` `Dirichlet Distribution` `PaySim` `Financial Technology (FinTech)`

## References

[1] B. McMahan, E. Moore, D. Ramage, S. Hampson and B. A. y Arcas, “Communication-Efficient Learning of Deep Networks from Decentralized Data” in Proceedings of the 20th International Conference on Artificial Intelligence and Statistics (AISTATS), 2017.

[2] T. Li, A. S. Sahu, M. Zaheer, M. Sanjabi, A. Talwalkar and V. Smith, “Federated Optimization in Heterogeneous Networks,” in Proceedings of Machine Learning and Systems  (MLSys), 2020.

[3] X. Li, M. Huang, Y. Yang, S. Wang and Z.Zhang, “On the Convergence of FedAvg on Non-IID Data,” International Conference on Learning Representations (ICLR), 2020.

[4] S. Ioffe and C. Szegedy, “Batch Normalization: Accelerating Deep Neural Network Training by Reducing Internal Covariate Shift,” in Proceedings of the International Conference on Machine Learning (ICML), 2015.

[5] X. Li, Y. Jiang, M.Zhang, X. Kamp and Q. Dou, “FedBN: Federated Learning on Non-IID Features via Local Batch Normalization,” in International Conference on Learning Representations (ICLR), 2021.

[6] I. Goodfellow, Y. Bengio and A. Courville, Deep Learning, Cambridge, MA, USA: MIT Press, 2016.

[7] C. C. Aggarwal, Neural Networks and Deep Learning: A Textbook, Cham, Switzerland: Springer, 2018.

[8] D. P. Kingma and J. Ba, “Adam: A Method for Stochastic Optimization," International Conference on Learning Representations (ICLR), 2015.

[9] A. Paszke et al., “PyTorch: An Imperative Style, High-Performance Deep Learning Library,” in Advances in Neural Information Processing Systems (NeurlPS), 2019.

[10] M. Abadi et al., “TensorFlow: Large-Scale  Machine Learning on Heterogeneous Systems,” 2016.

[11] F. Chollet, Deep Learning with Python, 2nd ed., Shelter Island, NY, USA: Manning Publications, 2021.

[12] E.A. Lopez-Rojas, A. Elmir and S. Axelsson, “PaySim: A financial mobile money simulator for fraud detection,” 2016.

[13] Kaggle,”Credit Card Fraud Detection Dataset,”2016.

[14] A. Ng, “Machine Learning Yearning,” deeplearning.ai, 2018.

[15] N. Kairouz et al., “Advances and Open Problems in Federated Learning,” Foundations and Trends in Machine Learning, vol.14, no. 1-2, pp. 1-210, 2021.

[16] A. Géron, Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow, 3rd ed., Sebastopol, CA, USA: O’Reilly Media, 2022.



