# CIFAR-10 Image Classification — Deep Learning Study

Exploring how design choices like model depth, regularisation, learning rate and batch size affect CNN performance on the CIFAR-10 image classification dataset

---

## Overview

This project trains and evaluates a series of deep learning models on CIFAR-10, which is a 10-class image classification dataset containing 60,000 32×32 colour images. Starting from a softmax regression baseline, the study progressively builds toward a tuned CNN, isolating the effect of each design decision at each stage.

The experiments cover:
- Softmax regression as a baseline
- CNN depth (number of convolutional layers)
- Regularisation through residual connections, dropout and weight decay
- Learning rate sensitivity
- Mini-batch size trade-offs

---

## Dataset

- 10 classes: plane, car, bird, cat, deer, dog, frog, horse, ship, truck
- 50,000 training images / 10,000 test images
- 10% of training data held out as a stratified validation split
- Training augmentation: random crop and horizontal flip
- Normalised using CIFAR-10 channel mean and standard deviation

---

## Experiments

### 1. Softmax Regression Baseline
A simple linear model (flatten → fully connected) trained on raw pixel values to establish a performance floor.

### 2a. Network Depth Study
`DepthCNN` is built with a configurable number of convolutional layers across 4 stages. Multiple configurations are compared to find the optimal depth before introducing regularisation.

### 2b. Regularisation Study
Using the best depth from 2a, the following regularisation strategies are tested in combination:
- Residual connections (skip connections between conv blocks)
- Dropout (spatial dropout applied after conv blocks)
- Weight decay (L2 regularisation via the optimiser)

### 2c. Learning Rate Study
The best architecture from 2b is trained across a range of learning rates with a fixed schedule to isolate the effect of the learning rate on convergence speed and final accuracy.

### 2d. Mini-Batch Size Study
Batch sizes ranging from 1 to 256 are evaluated, measuring the trade-off between test accuracy and training time per epoch.

---

## Key Findings

| Experiment | Best Configuration | Val Accuracy | Test Accuracy | Train Seconds/Epoch |
|------------|-------------------|-------------|---------------|-------------------|
| Softmax Regression | Linear classifier (baseline) | 40.38% | 40.33% | 3.47s |
| CNN Depth | 8-layer CNN | 62.54% | 62.64% | 11.37s |
| Regularisation | Residual + weight decay | 64.28% | 65.14% | 16.23s |
| Learning Rate | LR = 0.01 | 75.62% | 75.26% | 19.67s |
| Mini-Batch Size | Batch size 8 | 77.37% | 77.37% | 157.84s |

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| Python | Core language |
| PyTorch | Model building and training |
| Torchvision | CIFAR-10 dataset and transforms |
| NumPy / Pandas | Data handling and results aggregation |
| Matplotlib | Training curve and results visualisation |
| Jupyter Notebook | Interactive experimentation environment |

---

## Project Structure

```
├── Deep_learning_study.ipynb   # Full experiment notebook
└── data/                                      # CIFAR-10 data (auto-downloaded)
```

---

## Note
All cell outputs are pre-executed and saved in the notebook.
