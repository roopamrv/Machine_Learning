# Machine_Learning

Principal Component Analysis:
PCA is an unsupervised learning model used to reduce the data's dimensionality. Usually in machine learning, we have high dimensionality dataset which includes lot of features. This is a method to reduce the number of features, these reduced features are called principal components. But at the same time, most of the information is tried to retain even though the number of features is reduced. By doing this the performance of the model is increased.
Advantages of using PCA:
•	PCA can counteract the issues of a high-dimensional data set
•	One of the main issues when analyzing a high-dimensional data set is the overfitting: this happens when there are too many variables in the data set. Using PCA to lower the dimensions of the data set can prevent such an overfit.
•	It improves visualization.
•	It helps us to reduce a very large dataset by removing correlated features.
Disadvantages of using PCA:
•	Data normalization needs to be performed before applying PCA
•	There could be a loss of information if we do not choose the right number of components. 

Independent Component Analysis:
Independent Component Analysis (ICA) is used to distinguish distinct sources from a mixed input. In contrast to principal component analysis, which emphasizes maximum data point variance, independent component analysis emphasizes independence, or independent components.
Advantages of using ICA:
•	ICA works well for separating signals that are difficult to separate by other techniques, such as linear regression or PCA, since it presupposes that the source signals are non-Gaussian. 
•	ICA can separate signals even when it isn't aware of the sources or how they are related. Applications where the sources are unknown, such speech separation or EEG signal processing, might benefit from this. 
•	ICA methods are effective at handling enormous datasets and are computationally efficient. 
•	 ICA offers a representation of the data that is understandable, with each component standing in for a single source signal. Making defensible conclusions about the data and comprehending the underlying structure of the data can both benefit from this.
Disadvantages of using ICA:
•	 The ICA issue does not have a singular solution, and it is possible that the estimated independent components do not correspond to the real sources. This could result in less-than-ideal outcomes or misinterpretations. 
•	Certain ICA algorithms have the potential to provide different outcomes each time they are applied to the same set of data. 
•	If the source signals are not non-Gaussian, ICA may not work well and other techniques like PCA or linear regression may be better suitable.

Dataset:
Dataset used: Labeled Faces in the Wild (LFW) people dataset
13,233 face pictures from the internet have been collected for the LFW dataset. The 5749 IDs with 1680 individuals who have two or more photos make up this dataset. The verification accuracy rates for 6000 face pairings are stated in the standard LFW evaluation technique.

Eigenfaces extracted using PCA using Randomized SVD:
 
 <img width="406" alt="image" src="https://user-images.githubusercontent.com/89948461/225787475-a13e6aae-b560-40fa-a8a9-2691080b0cab.png">


Eigenfaces extracted using ICA - FastICA :
 

<img width="409" alt="image" src="https://user-images.githubusercontent.com/89948461/225787489-ce4073ea-2e5d-453b-98a1-29b7e32f9787.png">


Quantitative results of different parameters for both PCA and ICA (one table with different parameters for each method)
PCA:
 ![image](https://user-images.githubusercontent.com/89948461/225787498-078a4c42-1df3-47a0-addc-94c545670325.jpeg)


DISCUSSION:
PCA:
We get maximum accuracy for PCA when considered the below components,
•	svd_solver = ‘full’
•	Whiten = True
•	iterated_power = 75
•	iterated_power = 275
Accuracy is 89% approximately
1.	Why svd_solver is considered ‘full’:

SVD_solver as full in PCA is used because it is the most accurate and stable way to decompose the matrix. It is also used to reduce the dimensionality of the data as it can provide the most accurate representation of the data with the least amount of information lost. Additionally, it is useful for reducing noise and removing correlations between variables.

Other parameter values available are: - auto, randomized, arpack, full

2.	Why whiten is considered True:

Whiten as true in PCA should be used to ensure that the components extracted from the decomposition have unit variance. This helps to ensure that the data is properly scaled before further processing. It also helps to reduce the effects of correlated variables on the data and can help to reduce the number of components needed for the final model.

3.	Why n_components to be considered less which is 75:

n_compnents is considered as the hyperparameter in the PCA algorithm as we know this parameter defines the principal components to be chosen for the selected dataset and based on what we are trying to analyze. There is no specific number as an optimal number to choose for this parameter. We must manually enter and modify the value to fine-tune the algorithm to best match the scenario we are dealing with. 
4.	Why Iterated_power to be considered more which is 275:

Iterated_power in PCA should be considered more in this situation because in our observation we have approximate value of around 275 to get the best accuracy of the decomposition. This value is used to perform the set iterations until the desired accuracy is obtained. This is used to increase the refinement of the selected components. 

ICA:
 ![image](https://user-images.githubusercontent.com/89948461/225787517-79260166-d386-42ae-927d-51ab6f12eea1.jpeg)

From the above data and observation, we can see that maximum accuracy is achieved when we use following parameter set:
N_components: 250
•	algorithm (for FastICA): Parallel
•	whiten: unit-variance
•	function: exp (exponential)
•	max_iter: 100
•	whiten_solver: eigh
Parameter used:
1.	N_components: Number of components to be extracted from the table above, components ranging between 100-250 have been used for performing extraction using FastICA. As we increase the components number, we get better accuracy along with other parameters included.
2.	Algorithm: Algorithm can be of two types either “parallel” or “deflation”. If the algorithm for FastICA is parallel, then components are extracted simultaneously. On the other hand, if the algorithm is deflation, then components are extracted one by one.
3.	Fun: FastICA uses approximations to neg-entropy (J), which are more reliable than kurtosis-based measurements and calculate quickly, to quantify non-gaussianity. The approximate formula is
 J(y) = [E{G(y)} - E{G(v)}]2  where v is a N(0,1) 
Options for the variable G include G(u) = 1 logcosh(u) and G(u) = exp (u2 /2).

4.	Whiten: The solution to whiten images. 
 	If the issue is degenerate, "svd" is numerically more stable and frequently runs quicker when n 	samples = n features. 
With n samples >= n features, "eigh" is often more memory-efficient and may be quicker for n 	samples >= 50 * n features. 
From observation It can be said that when no. of components is large, and iterations are less then ICA gives the best Accuracy with exponential function. i.e., 86.6% 
At last, we can conclude that when considering components and iterations, PCA perform good when components are less and iterations are more whereas ICA performs better in more no. of components with very less iterations.

References:
•	https://towardsdatascience.com/using-principal-component-analysis-pca-for-machine-learning-b6e803f5bf1e
•	https://www.geeksforgeeks.org/python-variations-of-principal-component-analysis/
•	https://towardsdatascience.com/using-principal-component-analysis-pca-for-machine-learning-b6e803f5bf1e
