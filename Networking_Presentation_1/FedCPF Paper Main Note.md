#FL 
	# FedCPF An Efficient-Communication Federated Learning Approach for Vehicular Edge Computing in 6G Communication Networks



# <u>Abstract</u>

## Summary
The selected text is an abstract of a research paper that discusses the use of Federated Learning (FL) in Vehicular Edge Computing (VEC) within 6G networks. FL is used to protect consumer data privacy, but it can lead to expensive communication overheads. The authors propose an efficient-communication approach called FedCPF, which consists of three parts: Customized, Partial, and Flexible. FedCPF provides a customized local training strategy for vehicular clients, introduces a partial client participation rule, and presents a flexible aggregation policy for valid updates. Experimental results show that FedCPF outperforms the traditional FedAVG algorithm in terms of testing accuracy and communication optimization. Compared with the baseline, FedCPF achieves efficient communication with faster convergence speed and improves test accuracy by 6.31% on average, while the average communication optimization rate is improved by 2.15 times.

## <u>Important Terms</u>

#### ![[Federated Learning]]



# <u>Proposed Methods (IV)</u>

## <u>A. System Model</u>

##### <u>Notations</u>
$K =$ Total number of clients
$k =$ Index  of the clients
$D_k =$ Local Dataset of each client
$| . |$  Denotes the size of the set

${D_1,D_2, ......D_k} =$ Whole dataset

$|D| = \sum_{k=1}^{K} |D_k|$ 

{$x_k$} some local dataset with label set {$y_k$} in $D_k$ 

##### <u>Objective</u>
for some input $x_i$ in the neural network (local) $y_i$ is the desired output with some loss function $f_i(\omega)$ .

For some client $k$ the loss function on the data set is defined as:
$min_\omega F_k(\omega) =\frac{1}{|D_k|} \sum_{i \in D_k} f_i(\omega)$


$\omega^0 =$  Initial global parameter
$\omega_k^t =$ Local model parameters of the $k_{th}$ client for the $t_{th}$ communication round
$F(\omega) =$ Averaged global model parameters after the aggregate phase
$f_k(\omega_k) =$ Loss function of the $k_{th}$ client

Generalized Loss function,
$min_\omega F(\omega) = \sum_{k=1}^{K} \frac{|D_k|}{|D|}F_k(\omega_k)$                                    (4)

Optimizing the loss function $F(\omega)$ in FL is equivalent to minimizing the weighted average of local loss function $F_k(\omega_k)$ . Each client performs the training locally and shares their own local parameters.

## <u>B. Total Communication Cost</u>

$n(t) =$ Number of devices that participate in the $t_{th}$ communication round  \[ $n(t) \le K$ ]
$T =$ Total communication rounds in the FL process
$\omega^* =$ Number of model parameters
$W =$ Total communication cost in FL 

Total Communication cost,

$W=\sum_{t=1}^{T} \{n(t) + K\}.\omega^*$

Upper bound of communication overheads,
$\tilde{W}= 2T*(K.\omega^*)$                                                   (6)

##  <u>C. A customized Local training Strategy</u>

#### ![[Gradient Diversity]]

#### ![[Earth Mover's Distance (EMD)]]


#### <u>Approach to reduce Gradient Diversity</u>

Instead of minimizing the local loss function $F_k(.)$ , client $k$ minimizes the following objective equation,
$min_\omega  g_k(\omega_k;\omega^t)=F_k(\omega_k)+\frac{\epsilon}{2} ||\omega_k-\omega^t||^2$ 

##### $\theta_k^t$ Customized Local Training : 
$\theta_k^t$ Denotes running $\theta$ epochs on client $k$ at the $t_{th}$ federated training. 
$\hat{\omega_k}$ is an intermediate solution of equation (6)

The constraint $\frac{\epsilon}{2} ||\omega_k-\omega^t||^2$ is beneficial for two reasons,
- Alleviates the statistical heterogeneity by limiting the number of local updates closer to the global model without manually setting the local epochs.
- Allows for safely incorporating variable amounts of local training resulting from systems heterogeneity. 

## <u>D. Partial Client Participation Rule</u>

### <u>Problem : Too many clients communicating with the  parameter server</u>
**Fl Efficiency is effected by two things**
- Limitations of uplink communication
- Some clients only have a small amount of data which will become noise in the aggregation phase which will cause the global model to be more biased
### <u>Solution</u>
- A subset of the clients denoted as $\{S_t\}$ are selected and local models on those clients are used to optimize equation (4)
- In the uplink phase clients upload the $\omega_k$ also transmit the size of the local data set to the parameter server
- Parameter server calculates the probability of each client being selected, denotes as $p_k$ 
- Subset of selected clients in each round is different
- Equation (4) is changed to 
$min_\omega F(\omega)=\sum_{k=1}^{|S_t|}pk.gk(\omega_k;\omega^t)$
Where, $\sum_{k=1}^{|S_t|} p_k=1$

- The partial client participation rule contains more information about the client data set avoiding the development of a global model in some personalized direction

## <u>E. A Flexible Aggregation Policy</u>

- Since the local training process is  highly dynamic a flexible aggregation policy is required to maintain synchronicity
### <u>Problem</u>
- The most time consuming phase is the uplink communication. Because,
	- The server needs to wait for all the clients to upload the local training results and aggregate them
### <u>Solution</u>
- A flexible aggregation policy to limit the time of the uplink communication phase.
- $t_{th}$ uplink communication phase begins at time $r_s^t$ and finishes at time $r_e^t$ 
- $r_k$ denotes the time when the $k_{th}$ client finishes the local training time. 
- We add the following restriction
	- $r_s^t \le r_k \le r_e^t$
$T_g$ = Running time of a complete FL round
$T_{co}$ = Communication time
$T_{cp}$ = Time for local training epoch

$\theta_k^t$ = number of epochs for client $k$ 
$T_g=T_{co}+\theta_k^t.T_{cp}$

we will try to minimize $T_{co}$ using the flexible aggregation policy

## <u>FedCPF Algorithm (Pseudocode)</u>


![[Pasted image 20230729232957.png]]

## <u>F. Convergence Analysis</u>

#### IID : Independent and Identically Distributed
In the context of federated learning, an IID ideal federated network refers to a network where the data on each client is assumed to be independently and identically distributed. This means that the data on each client is assumed to be drawn from the same underlying distribution and is independent of the data on other clients. This is an idealized assumption that may not hold in real-world scenarios, where the data on different clients can be non-IID, meaning that it is not independently and identically distributed

