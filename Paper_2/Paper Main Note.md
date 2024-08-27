# Abstract

### What we're trying to do
- Considering the vehicle position and velocity formulate a min-max optimization problem in order to optimize
	- Computation Capability
	- Transmission Power
	- Local Model Accuracy to get min cost in worst case of FL
- The formulated problem is a [[Nonlinear Programming]] problem subdivided into two problems
	- **For resource allocation:** Lagrangian Dual + Subgradient Projection method
	- **local model accuracy:** And adaptive harmony algorithm

# Introduction

## <u>Challenges to be solved in Autonomous Driving</u>

###  Service Switching between edge servers efficiently

- In the context of vehicular edge computing (VEC), service switching between edge servers refers to the process of vehicles moving between the coverage areas of different edge servers while still maintaining their connection to the network. 
#### How to select vehicles with the best image quality for training

### Models training time is strongly associated with model accuracy

- The higher the local models accuracy the longer the local iteration time and greater computational energy consumption. But the number of updates to the edge server will decrease so that the transmission energy consumption will be reduced.
# <u>System Model</u>


## Notations
![[Pasted image 20230818203343.png | 1200x750]]

## <u>A. Connected and Autonomous Vehicles Modeling</u>

### C-V2X Technology

C-V2X, or Cellular Vehicle-to-Everything, is a wireless communication technology that enables vehicles to communicate with each other, as well as with other smart devices and infrastructure in their surroundings. C-V2X uses cellular networks and direct short-range communications to transmit information between vehicles and their environment.

### Poisson Process

A Poisson process is a mathematical model that describes the occurrence of random events over time. It is often used to model the arrival of customers, requests, or vehicles in a system. A Poisson process has two main characteristics: the number of events in any interval of time is independent of the number of events in any other disjoint interval, and the probability of a single event occurring in a small interval of time is proportional to the length of that interval.

## <u>B. Federated Learning in Vehicular Edge Computing</u>


