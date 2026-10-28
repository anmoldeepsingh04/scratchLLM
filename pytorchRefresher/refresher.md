# Introduction to PyTorch
It is a open source python-based DL library which is quite flexible and user-friendly.

## The three core components of PyTorch
1. Tensor library: a fundamental building block for efficient computing with the option to use GPUs for faster computations
2. Automatic differentiation engine or Autograd: utilities to automatically compute gradients for tensor operations, simplifying backpropagation and model optimization
3. DL library: utility functions that make it easier to implement and train deep neural networks.

## What is deep learning
- AI is concerned with creating computer systems that can perform tasks that require human intelligence. 
- ML is a sub-field of AI that focuses on developing algorithms by which the a machine can learn. The idea behind this is to allow machines to learn from available data, make predictions or decisions without being told to do so.
- DL is a sub-field of ML which focuses on learning algorithms inspired by the human brain (using deep "neural" networks). The "deep" here means the use of many hidden layers of neurons that allow the model to learn complex and non-linear relationships. 
- Typical supervised-learning setup looks like the following picture: 

![alt text](image.png)

## PyTorch
Pytorch has the capability to use GPUs for accelerated computing by utilizing parallelism. Depending on the machine and OS, we can have different options. For Mac machines like mine, we can use the MPS. Alternatively, if a GPU isn't present, one can use various cloud platforms that provide free but limited GPU compute.

## Understanding Tensors
Tensors are a generalization of vectors/matrices to higher dimensions. They can be characterized by their order (or rank), which gives the number of dimensions. Tensors serve as the containers that hold multidimensional data.

* Creating tensors
```
import torch

tensor0d = torch.tensor(1)
tensor1d = torch.tensor([1,2,3])
tensor2d = torch.tensor([[1,2], [3,4]])
tensor3d = torch.tensor([[[1,2],[3,4]],
                        [[5,6], [7,8]]])
```

* Checking and modifying a tensor's data type
```
print(tensor1d.dtype)
tensor1d = tensor1d.to(torch.float32)
```

* Shape and reshaping of a tensor
```
(tensor2d.shape)
tensor2d = tensor2d.reshape(3,2)
print(tensor2d.view(3,2))
```

* Transposing a tensor
```
print(tensor1d.T)
```

* Multiplying two matrices
```
print(tensor2d.matmul(tensor2d.T))
print(tensor2d @ tensor2d.T)
```

## Models as computation graphs
