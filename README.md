# SpeakerClusteringAndTrackingBM
In this document we are going to describe our implementation details of the given project. We different files in this project. We will describe each files independently. So the files we have is:
1.	URBM training and saving weights.
2.	RBM adaptation using URBM weights and saving adapted weights.
3.	RBM super-vectorsPCA RBM vectorsClustering.
4.	Speech segmentationRBM vectorsTracking score.

1.	URBM training and saving weights:
We have a file related to this called urbm_train_save_weights.py. In this file we performed everything needed to train the URBM model and hence after training weights will be saved. The large amount of back ground data will be given as input to this model. In fact, we have to run this file very first. 
2.	RBM adaptation using urbm weights and saving adapted weights: 
We have then the next file to adapt each speaker on the pre-trained URBM model. That is we train each speaker based on an RBM model whose weights are taken initially from pre-trained URBM model. We save weights of each speaker in different files. The file where we do this is rbm_adaptation_urbm_weights.py. 
3.	RBM super-vector extraction, PCA, RBM vectors, and Clustering:
We reload the weight matrix for each speaker and then we linearize the weight matrix with biases. This linearized weight matrix with biases is the RBM super-vector for a speaker. Then we apply PCA on all the RBM super-vectors. After application of PCA we get the RBM vectors for each speaker. Then we perform clustering on the RBM vectors. This is done on the file named, rbm_vectors_PCA_clustering.py
4.	Speech Segmentation, RBM vectors, and speaker tracking: 
We perform speaker segmentation, and then we generate RBM vectors for each segments. Now each segment is checked with each speaker to find the match. The matching with the RBM vectors from speaker segments to the RBM vectors of speaker is done via cosine scoring.  In fact, cosine score is a similarity measure between two vectors. So for each segment the speaker with highest cosine similarity will be assigned as the speaker of the segment. The whole thing is done in file named, rbm_vectors_speaker_tracking.py.

Order of execution is as the numerical order here. That means run in order of 1, 2, 3, and 4.
Results: 
1.	Speaker clustering: the speaker clustering results we have achieved using this very small number of samples is promising. It can be extrapolated that if we have better data then we can have better results.
2.	Speaker tracking: For speaker tracking task our results can be improved if we have more sample on background training of RBMs. Now the results is on average. 


Now something on the basic training algorithm of RBMs. We used CD-1 learning algorithm here. Why this is CD-1. In the part of CD-1 algorithm we have perform gibbs sampling. Gibbs sample is an iterative process. If we have an k-step gibbs sampling in our basic learning algorithm then we say it is as CD-k algorithm. In our case, we used just a single sampling of gibbs process that’s why it is said as CD-1 algorithm. Why we say CD. CD means contrastive divergence. Here we have both an positive gradient and negative gradient. Positive gradient from in input data and the negative gradient from the sampled data. As we want to give more importance of the input data than on the sampled data, therefore we add positive gradient and negate the negative gradient from our updates.



