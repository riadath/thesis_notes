Certainly, here are the bullet points summarizing the Problem Formulation section:

- **Objective**: To minimize the total energy consumption of users while maximizing user diversity in a wireless network, under a specific latency constraint.
  
- **Energy and Diversity**: The problem considers both the computation and communication energy of the users, promoting diversity among the scheduled users.

- **Multiple-Choice Knapsack Problem (MCKP)**: The user scheduling problem is modeled as an MCKP, where each user selects a training method, optimizing for energy efficiency and diversity.

- **Constraints**:
  - Each user’s training method selection and bandwidth allocation must not exceed the predefined latency and bandwidth limits.
  - Each user can only be scheduled with one training method at a time.
  - Binary decision-making is used for selecting the training method for each user.

- **Solution Approach**: Due to the complexity of the problem, a linear relaxation and a greedy algorithm are proposed for finding a near-optimal solution.