
Earth Mover’s Distance (EMD) is a measure of the distance between two probability distributions over a region. In the context of the selected text, EMD is used to measure the distance between the data distribution on a client and the whole data distribution.

This EMD distance measurement is affected by factors such as the learning rate, the number of training epochs, and the gradient. The text explains that weight divergence in Federated Learning (FL) is mainly caused by two aspects: \[<u>L^2 Norm</u> : Basically Euclidian Distance.\]
- <mark style="background: #BBFABBA6;">(1)</mark>the weight divergence accumulates after T-1 communication rounds.
- <mark style="background: #BBFABBA6;">(2)</mark> weight divergence is induced by the probability distance for the data distribution on client k compared with the actual distribution for the whole data set. As a result, it is necessary to set an appropriate local training strategy for each client with different training amounts to reduce weight divergence.
		- **(2) Explained :** The 2nd point means that the data distribution on each client may not be representative of the whole data distribution. For example, if the data set is about images of animals, some clients may have more images of cats than dogs, while others may have more images of birds than fish. This means that the probability of each label (such as cat, dog, bird, fish) is different on each client. This probability difference is measured by EMD, and it affects the weight divergence because <u>it influences the direction and magnitude of the gradient updates on each client</u>. Therefore, <u>the global model may not converge well if the data distribution on each client is too different from the whole data distribution</u>. 


