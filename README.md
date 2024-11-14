# Summary

This notebook is an implementation of the paper titled "HeteroFL: Computation and Communication Efficient Federated Learning for Heterogeneous Clients" (https://arxiv.org/abs/2010.01264)


The paper presents a novel framework for Federated Learning (FL) that addresses the challenges posed by heterogeneous clients with varying computational and communication capabilities. Below is a detailed explanation of the methodology employed in this research.
## Methodology Overview

### Problem Definition

The authors identify the limitations of traditional FL methods, which typically assume that all local models share the same architecture as the global model. This assumption restricts the complexity of the global model to accommodate the least capable client, leading to inefficiencies in both computation and communication.

### HeteroFL Framework

The proposed HeteroFL framework allows for heterogeneous local models, meaning that clients can have different model architectures and complexities while still contributing to a unified global model. The key components of this framework include:

#### A. Model Heterogeneity

Adaptive Subnetwork Allocation: Clients are assigned subnetworks based on their computational capabilities. This allows each client to train a model that suits its resources while contributing to a common global model.

Model Complexity Levels: The framework defines multiple levels of computation complexity, enabling clients to operate at different levels based on their capabilities. This flexibility helps optimize performance across diverse devices.

#### B. Global Model Aggregation

Weighted Model Averaging: The server aggregates model parameters from clients based on their assigned complexity levels. This process ensures that smaller models can still benefit from updates made by larger models while maintaining stability in global aggregation.

Dynamic Parameter Selection: The method allows for the selection of subsets of global model parameters for local training, which helps in reducing communication overhead and enhancing efficiency.

### Training Process

The training process in HeteroFL involves several key steps:

Client Selection: A subset of clients is selected randomly for each communication round.

Model Distribution: The server distributes the current global model parameters to selected clients.

Local Training: Each client trains its local model using its private data for several epochs, adjusting its parameters based on local computations.

Parameter Uploading: After local training, clients send their updated parameters back to the server.

Global Aggregation: The server aggregates these updates into a new global model using weighted averaging based on the complexity levels of each client.

### Static Batch Normalization (sBN)

To address privacy concerns associated with Batch Normalization (BN), which requires sharing running statistics, the authors introduce Static Batch Normalization (sBN). In this approach:
Clients do not track running statistics during training but normalize their batch data locally.
After training, the server queries clients to update global BN statistics cumulatively, ensuring privacy while stabilizing optimization.

### Scaler Module
To manage discrepancies in scale between different local models:
A Scaler module is introduced that adjusts outputs from local models during training. This module ensures that representations are appropriately scaled before being passed through normalization and activation layers.
This adjustment allows for seamless integration of various local models into a single global inference model without compromising performance.

### Empirical Evaluation
The methodology is validated through extensive experiments across multiple datasets and model architectures, demonstrating that HeteroFL:

Effectively handles heterogeneous client capabilities.

Reduces communication costs while maintaining high accuracy.

Performs robustly against non-IID data distributions.






### My Model

![image](https://github.com/user-attachments/assets/37b1f54d-f320-4452-a232-431c9386812d)





Conclusion
The HeteroFL framework represents a significant advancement in Federated Learning by allowing for heterogeneous local models that can adaptively contribute to a single global inference model. This approach enhances both computation and communication efficiency while addressing the challenges posed by diverse client capabilities in real-world applications.
