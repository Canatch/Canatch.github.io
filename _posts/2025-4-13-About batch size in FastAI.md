# About batch size in FastAI

## [About FastAI](https://docs.fast.ai/)

FastAI is a Python based deep learning framework , built on PyTorch , aims to lower the threshold of deep learning , it has a high degree of integration , comprehensive tutorials and documentation , highly encapsulated API and high flexibility.  

### An example of how to use fastai

1. Download and unzip the data
2. Load images, divide training and test sets, get labels, transform, and other preprocessing.
3. Show batch data
4. Select model for training and save
5. Show results
6. confusion matrix

## About the batch size

fastai is usually selected automatically based on GPU memory (default bs=64) and can be adjusted in the following ways:  

```
dls = dls.new(batch_size=32)  # Modification of existing DataLoaders
# or specified at creation
dls = ImageDataLoaders.from_folder(path, bs=32)
```
  
###  Comparison of different sizes  

| dimension             | small batch size (16-32)   | big batch size (128+)                         |
|  ----------------     | -------------------------  |-----------------------                        |
| training speed        | slow (More iterations)     | fast (High utilization of parallel computing) |
| memory utilization    | low                        | high                                          |
| gradient estimation   | Noisy, good generalization | More accurate, but may be overfitted          | 
| convergence stability | volatile                   | smoother                                      |
