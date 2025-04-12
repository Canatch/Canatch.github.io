# What is t-SNE
Reference from: https://zhuanlan.zhihu.com/p/148170862

t-Distributed Stochastic Neighbor Embedding (t-SNE) is a dimensionality reduction technique used to visualize high-dimensional datasets by representing them in a low-dimensional space in two or three dimensions.  

At the high level, t-SNE constructs a probability distribution for high-dimensional samples, where similar samples have a high probability of being selected and different points have a very low probability of being selected. Then, t-SNE defines a similar distribution for points in the low-dimensional embedding. Finally, t-SNE minimizes the Kullback-Leibler (KL) scatter between the two distributions with respect to the location of the embedded points.

##  Arithmetic

Suppose we have a dataset consisting of 3 different classes.  

![v2-c29ca0c35015476d6c41ab37fc467cd5_1440w](https://github.com/user-attachments/assets/e49d9e1c-a338-458d-b67d-6f17aae1f93c)

We would like to downscale and cluster them, but projecting their data directly onto the lower dimensional axes leads to a lot of data loss.We therefore use the t-SNE algorithm. The first step of this algorithm is to measure the distance of a point with respect to other points.  

![v2-68686d2e177ec02746354e7396658ee4_1440w](https://github.com/user-attachments/assets/9e574c46-7ee2-41ee-ac1b-bd32cc90e775)

In the distribution, the point with the smallest distance relative to the current point has a high probability, while the point far from the current point has a low probability.  
Looking at the 2D plot again, note that the blue dot clusters are more spread out than the green ones. If we don't address the difference in proportions, the green dots will be more likely than the blue dots. To account for this fact, we divide by the sum of the probabilities.  

![v2-938345ba69b133bef833fdaf251f32b0_1440w](https://github.com/user-attachments/assets/c39a71f2-23a2-4cd5-a24f-abe8f0f71920)

Thus, although the absolute distances between the two points are different, they are considered to be similar.

## Python code implementation

https://blog.csdn.net/haoji007/article/details/94962952
Sklearn provides a unified and concise API to implement a variety of machine learning algorithms and processes that can help us quickly realize a variety of machine learning tasks.  

A list of function parameters:
-parameters 描述
-n_components: Dimension of the embedding space.
-perpexity: he degree of perplexity, it means how many neighboring points are considered in the optimization process of t-SNE, the default is 30, it is recommended to take a value between 5 and 50.
-early_exaggeration: indicates the size of cluster spacing in the embedding space, the default is 12, the larger the value is, the larger the cluster spacing is after visualization.
-learning_rate: ndicates the speed of gradient descent, the default is 200, it is recommended to take the value between 10 and 1000.
-n_iter: the number of iterations, the default is 1000, custom settings should be guaranteed to be greater than 250
-min_grad_norm: Stop optimization if the gradient is less than this value. Default is 1e-7
-metric: Indicates how to measure the distance between vectors, default is Euclidean distance. If precomputed, the input X is the computed distance matrix. It can also be a custom distance metric function.
-init: Initialization, default is random, value is random for random initialization, value is pca for initialization using PCA (commonly used), value is numpy array must be shape=(n_samples, n_components).
-verbose: whether to print optimization information, take value 0 or 1, default is 0 => do not print information. The information to be printed are: number of nearest neighbors, time, σ, KL scatter, error, etc.
-random_state: Random number seed, integer or RandomState object.
-method: Two optimization methods: barnets_hut and exact, the first one takes O(NlogN), the second one takes O(N^2) but with small error, and the second one can't be used for millions of samples.
-angle: When method=barnets_hut, this parameter is useful to equalize the efficiency and error, the default value is 0.5, the larger the value, the higher the efficiency & the larger the error, otherwise vice versa. When the value is between 0.2-0.8, there is no change.

