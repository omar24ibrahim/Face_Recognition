# Face Recognition

## Why is PCA used in Face Recognition?

In face recognition, images of faces are typically high-dimensional data, with each pixel representing a feature. These high-dimensional data can be computationally expensive to work with and may lead to overfitting. PCA helps reduce the dimensionality of the data by transforming it into a lower-dimensional space while retaining as much variance as possible. This reduction in dimensionality simplifies subsequent processing steps and improves computational efficiency.

## Data Set

The dataset contains images from 40 individuals, each of them providing 10 images. The pixel intensities of the 400 face images will be used training and testing our face recognition model.

## Procedures

1.	Read images from files and reshape its vector representation from 112 x 92 to 1 x 10304.
2.	Split the produced data matrix into two submatrices:

    A.	Two equally sized matrices each of size 200 x 10304 which corresponds to taking 5 images for each person as training samples and 5 as testing samples.
  
    B.	Two matrices one of size 280 x 10304 for training samples and another of size 120 x 10304 for testing samples which corresponds to taking 7 images for each person for training and 3 for testing.

3.	Perform the classification using Principal Component Analysis (PCA):

  	A.	Mean calculation

  	  Forming a vector with entities equivalent to the mean of each feature.

  	B.	Data Centring

  	  Shifting all the training samples by subtracting the previously calculated mean vector to centre the data around the mean of each feature (pixel value).

  	C.	Covariance Matrix Calculation

  	  Multiplying the transpose of the data matrix by the data matrix and dividing each element of the produced matrix by the number of samples (200 in case of 5-5 division and 280 in case of 7-3 division).

  	D.	Eigenvalues and Eigenvectors Computation

  	  Finding both eigenvalues and eigenvectors for the previously calculated covariance matrix.

  	E.	Fraction of Total Variance Calculation

  	  Eigenvalues are ordered in a descending order and the eigenvectors are in an order such that each eigenvector is in the place corresponding to its eigenvalue.
      Number of needed eigen vectors is calculated by accumulative summation of eigenvalues divided by the overall sum of all eigen values which gives a value between 0 and 1 that corresponds to the amount of variance that can be accepted for the model.
      In this project this amount of variance is one of these 4 values: 0.8, 0.85, 0.9, and 0.95.

  	F.	Eigenvectors Reduction

  	  According to each one of the previously mentioned 4 values, an index is returned referring to the minimum number of eigenvectors needed to achieve this goal.

  	G.	Projection of Data Matrix

  	  This is done by multiplying the reduced eigenvectors’ matrix transposed by the centred data matrix.

4.	Use K Nearest Neighbours (KNN) classifier to produce the trained model:

    A.	Perform the previous steps with each of the given values for the variable K: 1, 3,5, and 7.

      These values determine how many points is considered by the classification to take a decision and predict the corresponding class for a given image.

      This method chooses the most common class of the K points and assign it to the sample given. In case a tie occurred, the classifier chooses the first class to appear from these tied classes.

    B.	Show the accuracy of prediction of test set samples with all possible combinations of K and α values.

  	Note:
	    For K = 7, if the data set was 5-5 divided, the accuracy will decrease as a tie will mostly occur which will probably cause some prediction errors. However, the accuracy will increase in case of 7-3 division.





## Graphs
 
Fig. 06: Accuracy for α = 0.8 and 5-5 Data Split
 
Fig. 07: Accuracy for α = 0.85 and 5-5 Data Split
 
Fig. 08: Accuracy for α = 0.9 and 5-5 Data Split
 
Fig. 09: Accuracy for α = 0.95 and 5-5 Data Split
 
Fig. 10: Accuracy for α = 0.8 and 7-3 Data Split
 
Fig. 11: Accuracy for α = 0.85 and 7-3 Data Split
 
Fig. 12: Accuracy for α = 0.9 and 7-3 Data Split
 
Fig. 13: Accuracy for α = 0.95 and 7-3 Data Split
