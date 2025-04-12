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

https://www.runoob.com/sklearn/sklearn-intro.html  
Sklearn provides a unified and concise API to implement a variety of machine learning algorithms and processes that can help us quickly realize a variety of machine learning tasks.  



