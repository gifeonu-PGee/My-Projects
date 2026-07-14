# Project 02 — Cats vs Dogs Image Classification

## Objective

Build a convolutional neural network (CNN) from scratch that can examine an image and classify it as either a **cat** or a **dog**.

**Problem type:** Binary image classification
**Framework:** TensorFlow / Keras
**Dataset:** [`cats_vs_dogs`](https://www.tensorflow.org/datasets/catalog/cats_vs_dogs) via `tensorflow_datasets`

---

## Overview

This project builds a CNN entirely from scratch (no pretrained weights) to classify images of cats and dogs. It follows on from Project 01 (CIFAR-10), applying the same core CNN principles to a binary classification problem, with deeper convolutional layers and dropout regularization to control overfitting.

---

## Methodology

### 1. Data Pipeline
- Loaded via `tensorflow_datasets` (`cats_vs_dogs`), split 80% train / 20% validation.
- Images resized to 150×150 and pixel values normalized to the [0, 1] range.
- Batched (batch size 32), shuffled, and prefetched for training efficiency.

### 2. Model Architecture

A sequential CNN with four convolution + max-pooling blocks, increasing in filter depth:

| Layer | Details |
|---|---|
| Input | 150 × 150 × 3 |
| Conv2D + MaxPooling | 32 filters, 3×3 kernel, ReLU |
| Conv2D + MaxPooling | 64 filters, 3×3 kernel, ReLU |
| Conv2D + MaxPooling | 128 filters, 3×3 kernel, ReLU |
| Conv2D + MaxPooling | 128 filters, 3×3 kernel, ReLU |
| Flatten | — |
| Dropout | 0.5 |
| Dense | 512 units, ReLU |
| Dense (output) | 1 unit, Sigmoid |

**Why this design:**
- Filter counts increase with depth (32 → 64 → 128 → 128) — early layers detect simple features like edges and colors; deeper layers combine these into complex shapes (fur texture, ears, snouts).
- **Dropout(0.5)** is applied before the final dense layers to reduce overfitting, randomly deactivating half the neurons during each training step so the network learns general patterns rather than memorizing training images.
- **Sigmoid** (rather than softmax) is used in the output layer since this is a binary classification problem (cat vs. dog) — softmax is reserved for 3+ mutually exclusive classes.

### 3. Training
- Optimizer: Adam
- Loss: Binary crossentropy
- Metric: Accuracy
- Trained for multiple epochs with training/validation accuracy and loss tracked after each epoch.

### 4. Real-World Validation
- Tested the trained model on an original, unseen uploaded photo (not part of the training/validation dataset).
- Model produced a correct classification with high confidence, confirming it generalizes beyond the benchmark dataset.

---

## Key Takeaways

- Building a CNN from scratch requires the network to learn all visual features (edges, textures, shapes) from the training data alone — this makes architecture choices (filter depth, dropout, layer count) especially important.
- Dropout was essential to prevent the model from overfitting, especially given the relatively small effective dataset size compared to how much a CNN can potentially memorize.
- This project set a useful baseline for comparison against transfer learning (see Project 03), which achieved higher validation accuracy in far fewer training epochs using a pretrained MobileNetV2 base.

---

## How to Run

1. Open the notebook in Google Colab.
2. Run all cells in order (Runtime → Run all).
3. In the final cell, upload your own image to test the model's prediction on a new, real-world photo.

**Requirements:** TensorFlow, TensorFlow Datasets — pre-installed in Google Colab.

---

## Tech Stack

- Python
- TensorFlow / Keras
- TensorFlow Datasets (`tfds`)
- Matplotlib (visualization)
- Google Colab (training environment, GPU-accelerated)

- ## Results

| Metric | Value |
|---------|---------|
| Training Accuracy | ~94.5% |
| Validation Accuracy | ~88.9% |
| Training Loss | ~0.14 |
| Validation Loss | ~0.28 |

### Observations

- Training accuracy steadily improved throughout training.
- Validation accuracy reached approximately **89%**.
- Validation loss remained relatively stable, indicating reasonable generalization.
- Mild overfitting appeared in later epochs as training accuracy continued to improve while validation performance plateaued.

- ## Challenges Encountered

During development several challenges were encountered:

- Initial dataset download failed due to compatibility issues with TensorFlow Datasets.
- TensorFlow package conflicts required updating the runtime.
- Different approaches (manual download vs TFDS) were evaluated before selecting the final pipeline.
- Model architecture was adjusted to improve validation performance and reduce overfitting.

- ## Future Improvements

Possible improvements include:

- Apply data augmentation.
- Introduce EarlyStopping.
- Save the best model using ModelCheckpoint.
- Evaluate on an independent test set.
- Compare performance against pretrained models such as MobileNetV2.

- ## Potential Business Applications

The techniques demonstrated in this project can be adapted for:

- Product image verification
- Manufacturing quality inspection
- Animal species recognition
- Medical image screening
- Inventory automation
- Agricultural crop monitoring
- Retail product classification
