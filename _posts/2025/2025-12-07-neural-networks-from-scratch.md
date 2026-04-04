---
title: "Neural Networks from Scratch [In Progress]"
date: 2025-12-07
tags: [Projects, AI]
github_url: https://github.com/JNPyles/Neural-Networks-from-Scratch
description: "Building a neural network entirely from scratch using Python and NumPy to truly understand the underlying mathematics of deep learning."
---

## Overview
Through this project, I am learning the underlying mechanics and math of deep learning models by building neural networks from the ground up using core Python and the NumPy library. The codebase is modeled after the principles and lessons outlined in the book [*Neural Networks from Scratch*](https://nnfs.io/) by Harrison Kinsley and Daniel Kukieła. 

## Key Concepts & Implementations
* **No High-Level Frameworks:** The core neural network architecture is built completely from scratch without relying on ML frameworks like TensorFlow or PyTorch.
* **Core Mathematics & Operations:** Demonstrates fundamental linear algebra concepts including dot products, matrix multiplications, vector addition, and transpositions using NumPy.
* **Object-Oriented Architecture:** Implements neural network components as distinct Python classes, including:
  * `Layer_Dense`: Fully-connected layers featuring forward pass logic and weight/bias initialization.
  * **Activation Functions:** Custom implementations of Step, Linear, and Softmax activation functions.
  * **Loss Functions:** A base `Loss` class and specific algorithmic implementations for Mean Squared Error (for regression) and Categorical Cross-Entropy (for classification).
* **Batch Processing:** Implements batched input processing to ensure training stability, model generalizability, and parallelization efficiency. 