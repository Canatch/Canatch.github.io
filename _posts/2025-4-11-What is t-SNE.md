# What is t-SNE
Reference from [here](https://zhuanlan.zhihu.com/p/148170862)

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

### Principles of Mathematics
Mathematically, the equation for the normal distribution is as follows.  
![1](/images/a1.png)

If we drop everything in front of the exponent and replace the mean with another point while solving for the scale problem discussed earlier, we get the equation:  
![2](/images/a2.png)  

If we take a similar approach as above (measuring distances between points and mapping them to a probability distribution), we get the following equation.  
![3](/images/a3.png)  


As before, we take the equation for a normal distribution, put everything in front of us, and divide the probability of one point with another, instead of implying that the sum that accounts for the scale is divided by the probability of all the other points (don't ask me why we got rid of the standard deviation). If we can make the probability distributions of the points in the simplified feature space approximate the points in the original feature space, we get well-defined clusters.

To do this, we use something called KL scatter.KL scatter is a measure of how different one probability distribution is from another.

![v2-456fd5a12c77f994b4fee7d98e52cae9_1440w](https://github.com/user-attachments/assets/7d5db1cc-0b5f-4031-8904-c6608e31f563)

The lower the value of KL scatter, the closer the two distributions are. a KL scatter of 0 means that the two distributions are identical.

This should hopefully lead to tons of ideas. Recall how, in the case of linear regression, we determined the line of best fit by minimizing the cost function (i.e., mean square error) using gradient descent. In t-SNE, we use gradient descent to minimize the sum of the Kullback-Leiber differences across all data points.

![4](/images/a4.png)  

![v2-2ff8846c929ef9e863194e2eb47f8357_1440w](https://github.com/user-attachments/assets/cc088889-c081-4d6b-b168-79aa81b49d50)

We take the partial derivative of the cost function with respect to each point in order to get the direction of each update.

![5](/images/a5.png )  

## Python code implementation

Reference from [here](https://blog.csdn.net/haoji007/article/details/94962952) and  [here](https://www.cnblogs.com/PythonLearner/p/12903615.html)

Sklearn provides a unified and concise API to implement a variety of machine learning algorithms and processes that can help us quickly realize a variety of machine learning tasks.  

A list of function parameters:
- `parameters` : discribe
- `n_components`: Dimension of the embedding space.
- `perpexity`: he degree of perplexity, it means how many neighboring points are considered in the optimization process of t-SNE, the default is 30, it is recommended to take a value between 5 and 50.
- `early_exaggeration`: indicates the size of cluster spacing in the embedding space, the default is 12, the larger the value is, the larger the cluster spacing is after visualization.
- `learning_rate`: ndicates the speed of gradient descent, the default is 200, it is recommended to take the value between 10 and 1000.
- `n_iter`: the number of iterations, the default is 1000, custom settings should be guaranteed to be greater than 250
- `min_grad_norm`: Stop optimization if the gradient is less than this value. Default is 1e-7
- `metric`: Indicates how to measure the distance between vectors, default is Euclidean distance. If precomputed, the input X is the computed distance matrix. It can also be a custom distance metric function.
- `init`: Initialization, default is random, value is random for random initialization, value is pca for initialization using PCA (commonly used), value is numpy array must be shape=(n_samples, n_components).
- `verbose`: whether to print optimization information, take value 0 or 1, default is 0 => do not print information. The information to be printed are: number of nearest neighbors, time, σ, KL scatter, error, etc.
- `random_state`: Random number seed, integer or RandomState object.
- `method`: Two optimization methods: barnets_hut and exact, the first one takes O(NlogN), the second one takes O(N^2) but with small error, and the second one can't be used for millions of samples.
- `angle`: When method=barnets_hut, this parameter is useful to equalize the efficiency and error, the default value is 0.5, the larger the value, the higher the efficiency & the larger the error, otherwise vice versa. When the value is between 0.2-0.8, there is no change.

