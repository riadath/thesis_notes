
**Key Points of the Abstract:**

1. **Introduction of HSFL:** The paper introduces the HSFL framework, which allows users (UAVs) in wireless networks to choose between SL and FL based on their characteristics. This choice is aimed at improving energy efficiency and leveraging the benefits of both learning methods.

2. **User Scheduling and Training Method Selection Problem:** Given the unreliable nature of wireless channels and the finite energy resources of UAVs, the paper formulates a problem to optimally schedule users and select the most suitable training method (SL or FL) for each user. This optimization problem is structured as a Multiple-Choice Knapsack Problem (MCKP).

3. **Energy-Efficient User Scheduling Algorithm:** To solve the formulated problem, the paper proposes an energy-efficient user scheduling algorithm. This algorithm aims to select a subset of users for participation in each learning round and decide whether they should use SL or FL, optimizing for energy efficiency.

4. **Simulation Results:** The paper demonstrates through simulations that the proposed HSFL framework, coupled with the user scheduling algorithm, significantly reduces energy consumption while maintaining comparable test accuracy against existing distributed learning algorithms. Additionally, the algorithm effectively chooses between SL and FL methods based on different data distributions among the users, highlighting its adaptability to varied network conditions.


# I. Introduction
The introduction section of the paper discusses the emerging role of wireless Unmanned Aerial Vehicles (UAV) networks in the context of the upcoming sixth-generation (6G) networks. These networks are envisioned to support a variety of applications, such as video streaming and disaster surveillance, by leveraging machine learning (ML) algorithms. The key challenge addressed is the efficient training of ML models in such networks, especially considering the limitations posed by large dataset transmissions, which lead to high communication overhead and energy consumption, as well as potential privacy concerns.

The paper highlights the advantages of distributed learning algorithms, like Federated Learning (FL) and Split Learning (SL), which allow for ML model training across multiple devices without the need to share raw data, thereby reducing communication overhead and preserving privacy. However, these methods alone may not be sufficient due to the heterogeneous nature of network users, which vary in computational capabilities and data distributions.

To tackle these challenges, the paper proposes a novel Hybrid Split and Federated Learning (HSFL) framework. This framework allows users to choose between SL and FL based on their specific characteristics, aiming to enhance energy efficiency and take advantage of the strengths of both learning methods in wireless UAV networks. The introduction also sets the stage for discussing the energy-efficient user scheduling problem formulated as a Multiple-Choice Knapsack Problem (MCKP), which the paper seeks to solve through a proposed algorithm. This algorithm aims to optimize user selection and training method assignment, considering the unreliable wireless channels and the limited energy resources of the users.

In essence, the introduction section outlines the motivation for integrating ML algorithms in UAV networks, the challenges of conventional centralized and distributed learning approaches, and the innovative solution proposed by the paper through the HSFL framework. It lays the groundwork for the detailed exploration of the HSFL framework, the user scheduling and training method selection problem, and the energy-efficient algorithm that follows in the subsequent sections.


# II. System Model
Section II of the paper, titled "System Model," lays the foundational framework for the proposed Hybrid Split and Federated Learning (HSFL) in wireless Unmanned Aerial Vehicles (UAV) networks. This section is crucial for understanding the operational environment, the assumptions made, and the components involved in the HSFL framework. The key elements of the system model are detailed below:

### A. Learning Model

The section starts by positioning UAVs as flying users within a wireless network, contributing to various applications through the collection and processing of data (e.g., images, and videos) using machine learning algorithms. It introduces the concept of distributed learning, highlighting the shift from conventional centralized learning methods to those that share model parameters (Federated Learning - FL, and Split Learning - SL) instead of raw datasets, addressing privacy concerns and reducing communication overhead.

The paper then proposes the HSFL framework that integrates the benefits of both FL and SL. This hybrid approach allows users to select either Split Training (ST) or Federated Training (FT) based on user characteristics like computation capabilities and data distributions. This flexibility is aimed at enhancing energy efficiency and adaptability in diverse network scenarios.

### B. Computation Model

This subsection breaks down the computation processes involved in HSFL, differentiating between the computation efforts required by SL and FL. It details the computation capacities of UAVs, the energy consumption models for both SL and FL and how computation time and energy are calculated based on these models. The distinction between SL and FL computation models emphasizes the paper's goal of optimizing energy efficiency by leveraging the strengths of both methods.

### C. Transmission Model

The transmission model outlines how data (model parameters or learning updates) is communicated between UAVs and the base station (BS). This includes the description of uplink and downlink transmission rates, the communication overhead for both SL and FL methods, and how these factors contribute to the overall latency and energy consumption of the system. The model considers the limitations of system bandwidth and the impact of wireless channel conditions on the efficiency of data transmission.

### D. Diversity Index

A diversity index is introduced to capture the heterogeneous characteristics of users within the network. This index is a composite measure that includes factors like data distribution diversity, computation capacity, and dataset size. The diversity index is crucial for the user selection process in the HSFL framework, as it influences the decision on whether a user should employ SL or FL for training, aiming to maximize the efficiency and effectiveness of the distributed learning process.

### Summary of Section II

Overall, Section II meticulously constructs a comprehensive system model that underpins the HSFL framework. It systematically addresses the components of learning, computation, and transmission models while introducing a novel measure of user diversity. This system model serves as the backbone for the subsequent formulation of the energy-efficient user scheduling problem and the development of an algorithm to solve this problem, paving the way for the practical implementation of HSFL in wireless UAV networks.



# Equation (2)
Equation (2) states:

$$
\tau^{tr}_{iF} = \frac{e_i C_i F D_i}{f_i}, \quad \forall i \in K_F
$$

This equation calculates the computation time $\tau^{tr}_{iF}$ for user $i$ when using the Federated Training (FT) method. Here is what each symbol in the equation represents:

- $\tau^{tr}_{iF}$: Computation time for the user $i$ during federated training.
- $e_i$: Energy consumed by the user $i$ per CPU cycle.
- $C_i$: Number of CPU cycles required by the user $i$ to process one sample of data.
- $F$: A constant representing the number of local iterations of training that a user performs with its dataset.
- $D_i$: The size of the local dataset of the user $i$.
- $f_i$: Computational capability of the user $i$, in terms of CPU frequency.
- $K_F$: The set of users that are scheduled to perform Federated Training.

This equation integrates several aspects of the user's device capabilities and the task's requirements. It essentially says that the computation time for the user $i$ is directly proportional to the energy per CPU cycle, the number of CPU cycles to process one data sample, the number of iterations, and the size of the dataset. It is inversely proportional to the computational capability of the user. The equation applies to all users $i$ that are a part of the set $K_F$, which are those selected for Federated Training.



In the "B. Computation Model" section, the energy consumption $E_{iF}$ for user $i$ during federated training (FT) is given by:

$$
E_{iF} = k \cdot e_i \cdot C_{iF} \cdot D_i \cdot f_i^2
$$

Here's what each term in the equation represents:

- $E_{iF}$: Energy consumption for user $i$ during federated training.
- $k$: Effective switched capacitance, which depends on the chip architecture of the user's device. This is a constant factor that encapsulates the energy efficiency of the hardware.
- $e_i$: Number of local training iterations performed by the user $i$.
- $C_{iF}$: Number of CPU cycles required to process one sample of data by the user $i$.
- $D_i$: Size of the local dataset for the user $i$.
- $f_i$: Computation capacity of the user $i$, which is the CPU frequency.

To understand the equation better, let's break it down:

- $C_{iF} \cdot D_i$: This product gives the total number of CPU cycles required to process the entire dataset $D_i$ during one local training iteration.
- $e_i \cdot (C_{iF} \cdot D_i)$: When you multiply by the number of iterations $e_i$, you get the total number of CPU cycles required for all local training iterations.
- $f_i^2$: This term represents the quadratic relationship between CPU frequency and energy consumption. As frequency increases, energy consumption rises quadratically. This is consistent with the power consumption characteristics of CMOS technology, where dynamic power consumption is proportional to the square of the frequency.

Putting it all together, the equation $E_{iF} = k \cdot e_i \cdot C_{iF} \cdot D_i \cdot f_i^2$ calculates the total energy consumed by the user $i$ to complete all its local training iterations. It incorporates the frequency of operations, the workload in terms of CPU cycles and dataset size, and the number of iterations, all scaled by the effective switched capacitance of the device's CPU. This comprehensive view allows the researchers to estimate and optimize the energy consumption for users engaged in federated learning within the UAV network.



# Diversity Index
The section on the Diversity Index provides a method for quantifying the diversity of users within a wireless network, specifically considering their unique characteristics. This diversity index is crucial for optimizing network operations and ensuring efficient utilization of resources.

Here’s a breakdown of the Diversity Index as described in the section:

- **Diversity of Users**: Acknowledges that users have varied data distributions, computational capabilities, and resources. The diversity comes from these heterogeneous characteristics of the users in the network.

- **Diversity Index Definition**: The index is a weighted sum of four parameters for each user: 
  1. **Local Dataset Diversity**: This is quantified using Shannon entropy, a measure of uncertainty or unpredictability in the dataset's information content. High entropy implies more diversity within the user's data.
  2. **User Diversity**: Represented by the "age-of-update," which could relate to how current or stale the user's data or model is.
  3. **Computation Capacity**: Refers to the user's ability to process data, likely measured by the speed or power of the user's computational resources.
  4. **Local Dataset Size**: The amount of data the user has, which can influence the user's ability to contribute to the learning process.

- **Weighted Sum Calculation**: Each user's diversity measure is calculated using the normalized value of these four parameters, denoted by $v_{i,n}$, where $i$ represents the user and $n$ represents the parameter.

- **Diversity Index Equation**: The diversity index for a user $i$, denoted as $I_i$, is computed as follows:

$$
I_i = \sum_n v_{i,n} \gamma_{i,n}
$$

Here, $\gamma_{i,n}$ is an adjustable weight for the $n$th metric of user $i$, allowing for the prioritization of different metrics based on the network's needs. The Base Station (BS) sets these weights. The vector $\Phi = \{ \gamma_{i,1}, \ldots, \gamma_{i,n} \}$ represents the collection of all weights for user $i$.

In summary, the Diversity Index offers a systematic approach to evaluate and rank users based on how diverse their characteristics are. This can inform decisions such as which users to prioritize for tasks like data processing or network maintenance. It's an attempt to capture a complex multi-dimensional attribute (diversity) in a single, quantifiable metric that can be used to optimize network functions in a data-driven manner.



# Optimization Problem
The optimization problem presented in the paper outlines the challenge of scheduling users in a Hybrid Split and Federated Learning (HSFL) framework to minimize energy consumption while also maximizing user diversity.

The optimization problem $OP_1$ is given as:

$$
\min_{b_i, \{a_{ij}\}} \sum_{i=1}^{N} \sum_{j \in J} a_{ij}(E_{ij} - l_{ij})
$$

Subject to the constraints:

- $C1: \sum_{j \in J} a_{ij}T_{ij} \leq T$
- $C2: a_{ij} \in \{0, 1\}, \forall j \in J, \forall i \in N$
- $C3: \sum_{j \in J} a_{ij} \leq 1, \forall i \in N$
- $C4: \sum_{i=1}^{N} \sum_{j \in J} a_{ij}b_{i} \leq 1$
- $C5: 0 \leq b_i \leq 1, \forall i \in N$

Here's what the terms and constraints represent:

- $\sum$: The summation symbol, indicates the sum over a range of values.
- $N$: Total number of users in the network.
- $J$: Set of possible training methods, which are Federated Training (FT) and Split Training (ST).
- $a_{ij}$: Binary decision variable indicating whether the user $i$ uses training method $j$. If $a_{ij}$ is 1, the method is selected; if 0, it is not.
- $E_{ij}$: The energy consumption of the user $i$ when using a training method $j$.
- $l_{ij}$: The diversity index or benefit of selecting a user $i$ with training method $j$.
- $b_i$: Bandwidth allocation ratio for user $i$.
- $T_{ij}$: Time is taken for the user $i$ using training method $j$.
- $T$: Maximum allowed time for one round of training, ensuring that the training is completed within a specified time frame.

Constraints:

- **$C1$**: The total time for each user must not exceed the threshold $T$. This ensures that training is completed within an acceptable duration.
- **$C2$**: $a_{ij}$ can only take values 0 or 1, representing a binary decision.
- **$C3$**: Each user can be scheduled with at most one training method.
- **$C4$**: The sum of the bandwidth allocated to all users cannot exceed the total available bandwidth $B_w$.
- **$C5$**: The bandwidth allocation ratio for each user must be between 0 and 1.

The objective function aims to minimize the total energy consumed by all users while considering the diversity of the users, which is represented as a subtraction of $l_{ij}$ from $E_{ij}$. The problem is formulated as a Multiple-Choice Knapsack Problem (MCKP) due to the binary decision variables and multiple constraints.

To solve $OP_1$, the paper suggests ignoring the time constraint $C1$ to transform it into $OP_2$, a standard MCKP problem, and then solve it using a Linear MCKP (LMCKP)-greedy algorithm. After solving $OP_2$, they incorporate the time constraint $C1$ to find a feasible solution that respects the maximum training time $T$.




# OP1 -> OP2 -> OP3

The final optimization problem in the paper evolves through a series of formulations, starting from an initial problem $OP_1$ and then transforming into $OP_2$ and $OP_3$ to deal with the complexity and solvability issues. Here's how the final optimization problem was obtained:

### Initial Problem $OP_1$:

- **Objective**: Minimize the total energy consumption and maximize the user diversity.
- **Decision Variables**: $\alpha_{ij}$ indicating the selection of the training method $j$ for user $i$, and $b_i$ indicating the bandwidth allocation ratio.
- **Constraints**: 
  - $C1$: The total computation time must not exceed the maximum round latency $T$.
  - $C2$: $\alpha_{ij}$ are binary decision variables.
  - $C3$: Each user can only choose one training method.
  - $C4$: The sum of the bandwidth allocated to all users must not exceed the total available bandwidth.
  - $C5$: Bandwidth allocation ratios are between 0 and 1.

### Transformation to $OP_2$ (Standard MCKP Problem):

- **Simplification**: The time constraint $C1$ is initially ignored to simplify the problem.
- **Objective**: Same as $OP_1$, but without the time constraint.
- **Constraints**: Same as $OP_1$, excluding $C1$.

### Final Problem $OP_3$ (Simplified MCKP Problem):

- **Maximization Objective**: Instead of minimization, the problem is reframed to maximize the profit of selecting training methods.
- **Profit Definition**: $p_{ij} = C + (I_{ij} - E_{ij})$, where $C$ is a large constant ensuring profits are non-negative.
- **Relaxed Decision Variables**: $\alpha_{ij}$ can now take any value between 0 and 1 instead of being binary, making the problem linear (LMCKP).
- **Constraints**: $C2$ and $C4$ remain the same, $C3$ ensures that each user can be assigned to only one training method or not be selected at all (due to the inclusion of $m_j = 0$ as a possible 'non-selection' method).

The final optimization problem $OP_3$ maximizes the weighted sum of profits derived from user diversity and energy consumption savings across all users and their chosen training methods, subject to the constraints of user selection and bandwidth allocation. This formulation is more amenable to solution by linear programming and greedy algorithms, making it practical for implementation in real-world systems.



# Removing Dominated Training Mechanisms
The equations related to Removing Dominated Training Mechanisms are conditions that help identify which training mechanisms are less efficient and therefore can be removed from the optimization problem.

- **Equation (11a)**:
  - $w_{ir} \leq w_{is} \leq w_{it}$: Denotes the weights of training mechanisms for user $i$, with $r$, $s$, and $t$ as different training methods.
  - $p_{ir} \leq p_{is} \leq p_{it}$: Denotes the profits of the training mechanisms.

- **Equation (11b)**:
  - $\lambda_{i,r\rightarrow s} \leq \lambda_{i,r\rightarrow t}$: Represents the efficiency of switching from one training method to another.

- **Equation (11c)**:
  - $\frac{p_{it} - p_{ir}}{w_{it} - w_{ir}}$ and $\frac{p_{is} - p_{ir}}{w_{is} - w_{ir}}$: Actual calculations of the efficiency $\lambda$ for changing methods.



A method $m_{is}$ would only be considered dominated by $m_{ir}$ if it offers no improvement in profit despite having an equal or greater weight, or if it offers a lower profit for the same weight. However, if $m_{is}$ provides the same or higher profit for the same or lesser weight compared to $m_{ir}$, it is not dominated and remains a viable option. The efficiency of each method is further assessed in equation 11b to determine dominance.


# Algorithm 2


The LMCKP-greedy User Scheduling Algorithm is designed to select users and their training methods for a distributed machine learning task. Here's a breakdown of how the algorithm works:

1. **Initialization**: 
   - Inputs are taken for the diversity index $I_i$ for each user $i$, and the energy consumption $E_{ij}$ for each learning mode $j$.
   - A threshold $T_{h}$ is set to 10.

2. **Learning Process**:
   - For each round of training $t$ until the maximum number $T$:
     - Compute the profit $p_{ij}$ for each user and learning mode, and initialize a weight matrix $b_{ij}$ with values $1/N$ if the mode is either Split Learning (S) or Federated Learning (F), and 0 otherwise.
     - Run the LMCKPGreedy subroutine with the calculated profits and weights to get a candidate set of users $N_{candi}$.
     - For each user in the candidate set:
       - If the user's training method is F and the required time $\tau_i$ is within the threshold, perform model updates using the Federated Learning method.
       - If the user's training method is S and the time $\tau_i$ is within the threshold, perform model updates using the Split Learning method.
     - The Base Station (BS) aggregates the model updates received from all users.

3. **LMCKPGreedy Subroutine**:
   - Remove dominated training methods for each user according to a set of criteria.
   - Sort the remaining training methods for each user based on the efficiency of updating from one training method to another in non-decreasing order.
   - Update the training method of each user based on sorted efficiencies, and adjust the total bandwidth allocation $b$ accordingly.
   - Continue this process until the next update violates the bandwidth constraint $C_4$.
   - Reverse the last update if it's not integer-feasible to ensure a feasible solution.
   - Return the set of users with the scheduled training method as $N_{candi}$.

The result is a user scheduling plan that optimizes for the given profit and weight within the system constraints, including time and bandwidth limitations.


# Simulation
The "Simulation Results" section presents the outcomes of experiments conducted on the MNIST dataset to evaluate the learning performance of the user scheduling scheme within the proposed Hybrid Split and Federated Learning (HSFL) framework. Here's a summary of the key findings:

- The convergence performance of the HSFL framework with MCKP-based user scheduling is evaluated under various data distributions: IID, nonIID, Dirichlet Imbalanced (Dir-ImD), and Dirichlet nonIID-Imbalanced (Dir-ImD-nonIID). The results depicted in Fig. 2 (a) of the paper indicate that diverse user selection and large local model updates significantly impact the model's convergence rate.

- The percentage of scheduled users choosing Split Training (ST) over Federated Training (FT) is higher under Imbalanced (ImD) data distribution. This preference is attributed to the energy savings achieved by users with smaller local datasets when they select the ST method.

- Energy consumption comparison among FL, Split FL (SFL), and HSFL shows that HSFL consumes the lowest energy while maintaining comparable test accuracy to FL and SFL, as illustrated in Fig. 2 (c) and (d) of the paper. The energy savings are mainly due to reduced communication overhead, as ST is selected for users with smaller datasets, and FT is selected for users with larger datasets, which reduces the amount of data transmitted and thus energy consumption, especially under the ImD data distribution.

- The HSFL framework utilizes a similar parallel training mechanism and model aggregation rule as FL and SFL, which allows it to achieve similar training results while being more energy-efficient.

These simulation results underscore the efficacy of the HSFL framework in energy conservation and its potential for equal test accuracy performance when compared to existing distributed learning algorithms like FL and SFL, particularly in scenarios with imbalanced data distribution among users.


