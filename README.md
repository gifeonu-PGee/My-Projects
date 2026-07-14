# Project 01 — CIFAR-10 Image Classification using Convolutional Neural Networks (CNN)

## Objective

Design, train, and evaluate a **Convolutional Neural Network (CNN)** from scratch to classify images into one of **10 object categories** using the CIFAR-10 dataset.

**Problem Type:** Multi-Class Image Classification

**Framework:** TensorFlow / Keras

**Dataset:** CIFAR-10

---

# Overview

This project marks my first implementation of a **Convolutional Neural Network (CNN)** using TensorFlow and Keras.

The objective was to understand how CNNs learn visual patterns from images by progressively extracting features such as edges, textures, and shapes before making a final classification.

Unlike later projects that use pretrained models, this CNN was trained **entirely from scratch**, allowing me to understand each stage of the deep learning pipeline.

---

# Dataset

The CIFAR-10 dataset contains **60,000 color images**.

- 50,000 Training Images
- 10,000 Test Images

Each image has dimensions:

```text
32 × 32 × 3
```

The dataset contains ten classes:

- Airplane
- Automobile
- Bird
- Cat
- Deer
- Dog
- Frog
- Horse
- Ship
- Truck

---

# Methodology

## 1. Data Preparation

The dataset was loaded directly from TensorFlow.

Images were normalized by dividing pixel values by **255**, converting pixel intensities from:

```text
0–255
```

to

```text
0–1
```

This improves numerical stability during neural network training.

---

## 2. CNN Architecture

A Sequential CNN was built using TensorFlow.

| Layer | Description |
|---------|-------------|
| Input | 32 × 32 × 3 |
| Conv2D | 32 filters, 3×3 kernel, ReLU |
| MaxPooling2D | 2×2 |
| Conv2D | 64 filters, 3×3 kernel, ReLU |
| MaxPooling2D | 2×2 |
| Flatten | Converts feature maps into a vector |
| Dense | 64 neurons, ReLU |
| Dense | 10 neurons, Softmax |

---

## Understanding the CNN Pipeline

During this project I learned the purpose of each major CNN component.

### Convolution Layer (Conv2D)

Extracts important visual features such as:

- edges
- curves
- textures
- simple shapes

---

### ReLU Activation

Removes negative activations while preserving useful feature information, allowing the network to learn more complex patterns.

---

### Max Pooling

Reduces image dimensions while preserving the strongest visual features.

Benefits include:

- Faster computation
- Reduced memory usage
- Lower risk of overfitting

---

### Flatten

Transforms the feature maps into a one-dimensional vector so they can be processed by dense layers.

---

### Dense Layer

Acts as the classifier by combining learned visual features into class scores.

---

### Softmax

Converts the output scores into probabilities across the ten classes.

The class with the highest probability becomes the final prediction.

---

## 3. Model Compilation

Optimizer:

- Adam

Loss Function:

- Sparse Categorical Crossentropy

Evaluation Metric:

- Accuracy

---

## 4. Training

The model was trained using multiple epochs.

During training, TensorFlow recorded:

- Training Accuracy
- Validation Accuracy
- Training Loss
- Validation Loss

These metrics were used to evaluate learning progress and identify signs of overfitting.

---

# Results

| Metric | Result |
|---------|---------|
| Validation Accuracy | ~73% |

### Observations

- The model successfully learned meaningful visual patterns from the dataset.
- Validation accuracy steadily improved during training.
- After approximately the seventh epoch, validation accuracy began to plateau while training accuracy continued increasing, indicating the beginning of overfitting.
- Increasing the CNN depth improved overall performance compared with the initial architecture.

---

# Challenges Encountered

Throughout the project several improvements were explored:

- Added additional convolutional layers.
- Increased filter depth from 32 to 64.
- Increased the number of training epochs.
- Compared validation accuracy across different architectures.
- Learned how model complexity affects training time and generalization.

---

# Key Lessons Learned

This project introduced the core building blocks of computer vision using deep learning.

Major concepts learned included:

- Convolution
- Feature Extraction
- ReLU Activation
- Max Pooling
- Flattening
- Dense Layers
- Softmax Classification
- Epochs
- Batch Size
- Validation Split
- Loss Functions
- Optimizers (Adam)

This project also demonstrated how deeper CNNs can improve performance, while excessive training may lead to overfitting.

---

# Future Improvements

Potential improvements include:

- Data Augmentation
- Dropout Regularization
- EarlyStopping
- ModelCheckpoint
- Learning Rate Scheduling
- Transfer Learning using MobileNetV2

These improvements are explored further in Project 02 and Project 03.

---

# Potential Business Applications

The techniques learned in this project can be applied to:

- Product Recognition
- Manufacturing Quality Control
- Medical Image Classification
- Retail Automation
- Agricultural Disease Detection
- Wildlife Monitoring
- Autonomous Vehicle Vision Systems

---

# Skills Demonstrated

- Python
- TensorFlow
- Keras
- Convolutional Neural Networks
- Computer Vision
- Image Classification
- Data Preprocessing
- Model Evaluation
- Deep Learning Fundamentals
- GPU Training (Google Colab)

---

# How to Run

1. Open the notebook in Google Colab.
2. Run all notebook cells in sequence.
3. Train the CNN on the CIFAR-10 dataset.
4. Observe the learning curves.
5. Evaluate the trained model on unseen test images.

---

# Tech Stack

- Python
- TensorFlow
- Keras
- NumPy
- Matplotlib
- Google Colab

---

# Key Takeaway

Project 01 established the foundation for my computer vision journey by teaching how Convolutional Neural Networks learn visual features directly from data.

The concepts learned here became the basis for subsequent projects involving deeper CNN architectures and Transfer Learning, ultimately leading to significantly higher-performing image classification models.
