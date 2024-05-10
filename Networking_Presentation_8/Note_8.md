# Relation to Previous Papers

![[Pasted image 20240510091657.png|500x100]]

  

This paper cites our 6th presentation paper: "Energy-Efficient Radio Resource Allocation for Federated Edge Learning"

  
  

## Main Topics

The paper focuses on the challenges of implementing Federated Edge Learning (FEEL) in environments where communication bandwidth is limited and edge devices are diverse in capabilities and data distribution. It introduces a data-aware device scheduling algorithm that prioritizes devices based on data diversity to improve model training efficiency and accuracy.

  

## Main Contributions

1. **Diversity Indicator Design**: A novel indicator to evaluate data diversity among devices, influencing the selection of devices for model training in FEEL.

2. **Joint Device Selection and Bandwidth Allocation**: A problem formulation that integrates device selection with data diversity and resource allocation to optimize FEEL operations.

3. **Data-Aware Scheduling (DAS) Algorithm**: A scheduling algorithm that effectively manages device selection and bandwidth allocation based on the proposed diversity indicator.


4. **Performance Evaluation**: Extensive simulations show that the DAS algorithm can significantly enhance learning accuracy and reduce resource consumption compared to traditional approaches.

  
  
  
  

### Introduction Summary

  

- **Context**: The paper discusses Federated Edge Learning (FEEL), which enables collaborative machine learning across edge devices without centralizing data, thus addressing privacy and bandwidth issues in distributed networks.

  

- **Challenges**: FEEL faces challenges due to limited communication bandwidth and the diverse data distribution across devices, which affects the efficiency of the learning process.

  

- **Proposed Solution**: The authors propose a data-aware device scheduling algorithm that prioritizes devices for training based on the diversity of their data, aiming to enhance learning efficiency and accuracy.

  

- **Innovation**: Unlike traditional FEEL approaches that may overlook the significance of data characteristics, this paper focuses on integrating these characteristics into the scheduling process to improve outcomes.

  

- **Objectives**: The primary goal is to develop an algorithm that optimally selects devices for participation in the learning process, considering both their data properties and resource constraints, to minimize overall learning time and energy consumption while maximizing accuracy.

  

# III. DIVERSITY IN FEDERATED LEARNING

  
  

- Diversity on the construction of training batches to improve the efficiency of the learning process: **citation \[23\]**

### Citation \[23\] Abstract:

**<u>Determinantal Point Processes for Mini-Batch Diversification</u>**

We study a mini-batch diversification scheme for stochastic gradient descent (SGD). While classical SGD relies on uniformly sampling data points to form a mini-batch, we propose a non-uniform sampling scheme based on the Determinantal Point Process (DPP). The DPP relies on a similarity measure between data points and gives low probabilities to mini-batches that contain redundant data, and higher probabilities to mini-batches with more diverse data. This simultaneously balances the data and leads to stochastic gradients with lower variance. We term this approach Diversified Mini-Batch SGD (DM-SGD). We show that regular SGD and a biased version of stratified sampling emerge as special cases. Furthermore, DM-SGD generalizes stratified sampling to cases where no discrete features exist to bin the data into groups. We show experimentally that our method results in more interpretable and diverse features in unsupervised setups, and in better classification accuracies in supervised setups.

  

### Active Learning

  

#### Citation \[12\]

**Diversifying Convex Transductive Experimental Design for Active Learning**

Convex Transductive Experimental Design (CTED) is one of the most representative active learning methods. It utilizes a data reconstruction framework to select informative samples for manual annotation. However, we observe that CTED cannot well handle the diversity of selected samples and hence the set of selected samples may contain mutually similar samples that convey similar or overlapped information. This is definitely undesired. Given the limited budget for data labeling, it is desired to select informative samples with complementary information, i.e., similar samples are excluded. To this end, we propose Diversified CTED by seamlessly incorporating a novel and effective diversity regularizer into CTED, ensuring the selected samples are diverse. The involvement of the diversity regularizer makes the optimization problem hard to solve. We derive an effective algorithm to solve an equivalent problem which is easier to optimize. Extensive experimental results on several benchmark data sets demonstrate that Diversified CTED significantly improves CTED and consistently outperforms the state-of-the-art methods, verifying the effectiveness and advantages of incorporating the proposed diversity regularizer into CTED.

  
  

#### Citation \[13\]

**Diverse Expected Gradient Active Learning for Relative Attributes**

The use of relative attributes for semantic understanding of images and videos is a promising way to improve communication between humans and machines. However, it is extremely labor- and time-consuming to define multiple attributes for each instance in a large amount of data. One option is to incorporate active learning so that the informative samples can be actively discovered and then labeled. However, most existing active-learning methods select samples one at a time (serial mode), and may therefore lose efficiency when learning multiple attributes. In this paper, we propose a batch-mode active-learning method, called diverse expected gradient active learning. This method integrates an informativeness analysis and a diversity analysis to form a diverse batch of queries. Specifically, the informativeness analysis employs the expected pairwise gradient length as a measure of informativeness, while the diversity analysis forces a constraint on the proposed diverse gradient angle. Since simultaneous optimization of these two parts is intractable, we utilize a two-step procedure to obtain the diverse batch of queries. A heuristic method is also introduced to suppress imbalanced multi-class distributions. Empirical evaluations of three different databases demonstrate the effectiveness and efficiency of the proposed approach.

  
  
  
  

**What is a good measure of diversity for FEEL**

- Shanon Entropy

- Gini-Simpson index

We can use the above two to check if the dataset has diverse examples from multiple classes.

  

Consequently, the diversity (i.e., variations of the sequence data) should be evaluated using methods such as **approximate entropy (ApEn)** and **sample entropy (SampEn)** \[30\].

  

**Citation \[30\]**

[Entropy | Free Full-Text | Approximate Entropy and Sample Entropy: A Comprehensive Tutorial (mdpi.com)](https://www.mdpi.com/1099-4300/21/6/541)]

  

#### Gini-Simpson Index

![[Pasted image 20240510111044.png]]

##### Shannon Entropy

![[Pasted image 20240510111106.png]]

  
  

# System Model and Problem Formulation

  

![[Pasted image 20240510111123.png]]

  

### System Model and Problem Formulation Summary

  

- **System Model Overview**: The system consists of a multi-access edge computing (MEC) server and multiple edge devices participating in FEEL. Each device contains a local dataset used for training. The global model is trained by aggregating updates from these devices, which train models locally using their data.

  

- **Learning Model**:

- The model’s parameters are initialized by the MEC server, and the global model is updated by aggregating local updates from the devices.

- The objective is to minimize the prediction loss across all devices, represented by the equation:

$$

\min_{w \in \mathbb{R}^d} F(w) = \frac{1}{N} \sum_{k=1}^K F_k(w)

$$

where $w$ is the model parameter vector, $F_k(w)$ is the loss function computed by device $k$, and $N$ is the total number of data points.
![[Pasted image 20240510115628.png]]
  

- **Dataset Diversity Index Design**:

- To address dataset diversity, the authors propose incorporating a diversity index into the device selection process. The diversity index quantifies the value of data each device holds, focusing on metrics such as dataset size and variance.

- The diversity index $D_k$ for a device $k$ is defined as:

$$

D_k = \sum_i E_{i,k} \times W_{i,k}

$$

where $E_{i,k}$ is the normalized value of the metric $i$ for dataset $k$, and $W_{i,k}$ is the weight assigned to each metric.


### Overview of the Transmission Model

This model deals with the challenges and considerations around efficiently managing the bandwidth and communication resources to ensure effective data transmission during the training process. It’s crucial because the constraints of wireless networks, such as bandwidth limitations and variable channel conditions, can significantly impact the performance of FEEL.

### Key Components of the Transmission Model

1. **Bandwidth Allocation**:
   - Each device $k$ is allocated a portion of the total available bandwidth, denoted as $U_k$. This allocation determines how much network capacity each device can use to send its data.

2. **Channel Gain and Transmit Power**:
   - $h_k$ represents the channel gain between device $k$ and the base station, reflecting the quality of the transmission channel, which can affect the data rate.
   - $P_k$ denotes the transmit power of device $k$, which is a factor in how effectively data can be transmitted over the allocated bandwidth.

### Mathematical Formulation

- **Achievable Data Rate**:
  - The data rate $R_k$ that device $k$ can achieve over its allocated bandwidth $U_k$ is calculated using the Shannon-Hartley theorem, which is a fundamental equation in information theory that relates the capacity of a communication channel to its bandwidth, the transmit power, and the noise level:
    $$
    R_k = U_k \log_2(1 + \frac{P_k h_k}{U_k N_0})
    $$
    Here, $N_0$ is the noise power spectral density, a measure of the power of the background noise in the channel.

### Key Points Addressed in the Transmission Model

- **Efficient Use of Bandwidth**:
  - The model must optimize how bandwidth is allocated among devices to maximize the overall data throughput. This involves a trade-off between the number of devices transmitting simultaneously and the quality of each transmission.

- **Handling Communication Constraints**:
  - In FEEL, not all devices may be able to communicate simultaneously due to bandwidth limitations. The transmission model helps determine which devices should transmit their updates based on the current network conditions and their data's relevance (as influenced by factors like data diversity and the age of data).

- **Optimization Goals**:
  - The ultimate goal is to minimize the time and energy required for data transmission while ensuring that enough data is transmitted for effective model training. This involves balancing the transmit power, bandwidth allocation, and the scheduling of device transmissions to optimize the use of limited network resources.

### Conclusion of the Transmission Model Section

This section of the paper crucially addresses how the FEEL system manages the physical limitations and variabilities of wireless communications to ensure efficient and effective training of machine learning models. By mathematically modeling the transmission capabilities and constraints, the FEEL system can better optimize device participation and data flow, leading to improved learning outcomes and more efficient use of network resources.
