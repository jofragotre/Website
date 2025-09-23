---
title: "Neural Network from Scratch (NumPy)"
summary: "A modular neural network built using only NumPy — layers, forward/backward, gradients, and Iris demo."
tags: ["NumPy", "Neural Networks", "ML Foundations", "From Scratch"]
thumbnail: "thumbnail.png"   # optional: add a simple diagram or screenshot
weight:  10
showToc: false
---

I built this project as hands-on way to re-discover the basics of neural networks. By buiding everything from scratch, I feel the intuition for some of the common issues with training and deploying neural networks is improved. This repository is a clean, educational **neural network implementation** using only **NumPy**. It includes modular layers, forward/backward propagation, gradient-based updates, and examples (including the **Iris** dataset).


# Implementation details

{{< button href="https://github.com/jofragotre/ml-from-scratch" >}}Code on GitHub{{< /button >}}

## Features
- Modular layer system (Linear, ReLU, Softmax; easy to extend)
- End-to-end forward and backward propagation
- Gradient descent updates, batch processing
- Multiple weight initialization schemes (Kaiming/Zero/Random)
- Iris dataset example and a minimal training script

## Project structure

```
ml-from-scratch/
├── layers.py        # Neural network layer implementations
├── network.py       # Neural network class
├── iris_example.py  # Example using Iris dataset
└── train_example.py # Basic training example
```

## Components

### Layers (layers.py)
- `Module` — base class
- `Neuron` — single neuron abstraction
- `LinearLayer` — fully connected layer
- `ReLU` — nonlinearity
- `Softmax` — for multi-class classification

### Network (network.py)
- Arbitrary depth via layer list
- Forward/backward passes with gradient propagation
- Simple optimizer step via network.update()

## Usage

Basic example:
```python
import numpy as np
from network import Network
from loss_functions import CategoricalCrossEntropy

# Example inputs/labels
X_train = np.random.randn(64, 4)  # batch of 64, 4 features
y_train = np.eye(3)[np.random.randint(0, 3, size=64)]  # one-hot labels

# Build a 4 -> 8 -> 3 MLP
net = Network([4, 8, 3])  # Linear->ReLU->Linear->Softmax internally

# Forward
preds = net.forward(X_train)

# Loss and gradient
loss_fn = CategoricalCrossEntropy()
loss = loss_fn.forward(y_train, preds)
grad = loss_fn.backward(y_train, preds)

# Backward + update
net.backward(grad)
net.update(learning_rate=0.01)
```

Iris example:
```bash
python iris_example.py
```

## Technical details

- Forward propagation: layer-by-layer `y = Wx + b`, activations applied
- Backpropagation: gradients via chain rule through each layer
- Update step: gradient descent on parameters
- Activations: ReLU, Softmax
- Initializations: Kaiming/Zero/Random

## Requirements
- numpy
- scikit-learn  # for the Iris example

Install:
```bash
pip install numpy scikit-learn
```

## Roadmap / TODO
- Param class to encapsulate weights + gradients
- Optimizer abstraction (SGD, Momentum, Adam)
- Additional layers: Conv2d, BatchNorm, Sigmoid, etc.

## License
MIT