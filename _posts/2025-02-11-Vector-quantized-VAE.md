---
title: "Vector-quantized-VAE"
date: 2025-02-11 20:05:00 +0800
categories: [Data Science]
tags: [Math]
mathjax: true
---



## Overview

A VQ-VAE is a neural network model that compresses (encodes) data into a simpler form and then reconstructs (decodes) it. Unlike a regular Variational Autoencoder (VAE) that uses continuous values in its latent space (the “hidden” representation), a VQ-VAE uses a **discrete** latent space. This means that instead of any real number, the latent representation is chosen from a fixed set of “prototype” vectors (called the **codebook** or **embedding space**).

---

## How It Works – Layman’s Terms

Imagine you have a huge box of colored beads (your data). Instead of using every possible color, you decide to pick just a limited palette (your codebook) to represent all the beads. Here’s how you’d do it:

1. **Encoding:**  
   You look at an image (or any input) and break it down into features (like shapes or textures).

2. **Quantization (Discretization):**  
   Instead of using the exact features (which might be very detailed), you choose the closest match from your limited palette. In our bead example, this is like replacing each bead color with the nearest color from your chosen palette.

3. **Decoding:**  
   You use these “palette” colors (the discrete codes) to reconstruct the image. Even though you lost some detail, you still capture the essential structure.

Over time, the model learns the best “palette” (codebook) that can efficiently represent the recurring patterns in the data.

---

## How It Works – Academic Explanation

### 1. **Components**

- **Encoder:**  
  Maps an input $x$ (e.g., an image) to a continuous latent representation, denoted by $z_e(x)$.

- **Codebook (Embedding Space):**  
  A set of $K$ learnable embedding vectors,  
  $$
  e = \{ e_1, e_2, \dots, e_K \}, \quad e_k \in \mathbb{R}^D,
  $$
  where $D$ is the dimensionality of each code.

- **Vector Quantization:**  
  Each continuous latent vector $z_e(x)$ is replaced by the closest codebook vector. Mathematically, for each location (or element) in $z_e(x)$, we find:
  $$
  k^* = \arg\min_{k} \| z_e(x) - e_k \|_2,
  $$
  and then set the quantized latent vector as:
  $$
  z_q(x) = e_{k^*}.
  $$

- **Decoder:**  
  Reconstructs the input from the quantized latent representation $z_q(x)$, resulting in the reconstruction $\hat{x}$.

### 2. **Loss Function**

The VQ-VAE is trained with a combination of three loss terms:

1. **Reconstruction Loss:**  
   Ensures that the output $\hat{x}$ is close to the input $x$. A common choice is the Mean Squared Error (MSE):
   $$
   \mathcal{L}_{\text{recon}} = \| x - \hat{x} \|^2.
   $$

2. **Codebook Loss:**  
   Forces the codebook vectors to be close to the encoder’s outputs. However, gradients are prevented from flowing into the encoder using the “stop-gradient” operator (denoted as $\text{sg}[\cdot]$):
   $$
   \mathcal{L}_{\text{codebook}} = \| \text{sg}[z_e(x)] - e_{k^*} \|^2.
   $$

3. **Commitment Loss:**  
   Encourages the encoder to commit to the codebook vector it is assigned by penalizing the difference between $z_e(x)$ and the selected code $e_{k^*}$ (here, the gradient flows only to the encoder):
   $$
   \mathcal{L}_{\text{commit}} = \| z_e(x) - \text{sg}[e_{k^*}] \|^2.
   $$
   A hyperparameter $\beta$ is used to balance this term.

The total loss is a sum of these parts:
$$
\mathcal{L} = \mathcal{L}_{\text{recon}} + \mathcal{L}_{\text{codebook}} + \beta\, \mathcal{L}_{\text{commit}}.
$$

---

## Concrete Example: Image Compression with VQ-VAE

### Scenario

Imagine you want to compress images of handwritten digits (such as MNIST digits) using a VQ-VAE.

### Step-by-Step Process

1. **Input:**  
   You have a 28×28 grayscale image of a digit (say, the digit “7”).

2. **Encoding:**  
   The encoder network processes the image and outputs a latent representation. For instance, the encoder might produce a grid of latent vectors with a shape of $7 \times 7 \times D$ (i.e., 49 vectors, each of $D$ dimensions).

3. **Quantization:**  
   - You have a codebook containing $K = 512$ embeddings, each of dimension $D$.  
   - For each of the 49 latent vectors, the VQ-VAE finds the closest codebook vector using the Euclidean distance:
     $$
     k^* = \arg\min_{k \in \{1, \dots, 512\}} \| z_e(x)_{ij} - e_k \|_2.
     $$
   - The encoder’s output at position \((i,j)\) is then replaced by $e_{k^*}$.  
   - Now, instead of 49 continuous vectors, you have 49 discrete codes (indices ranging from 1 to 512).

4. **Decoding:**  
   The decoder receives the quantized latent representation (the 49 codebook vectors) and reconstructs the original 28×28 image, trying to capture the key features (like the strokes that form the digit “7”).

5. **Training:**  
   - **Reconstruction Loss:**  
     The difference between the original image and the reconstructed image is measured (using MSE).  
     For example, if the original image $x$ and reconstructed image $\hat{x}$ differ pixel by pixel, the reconstruction loss will sum the square of those differences.
   - **Codebook and Commitment Losses:**  
     These ensure that the latent vectors produced by the encoder are close to the codebook vectors and that the codebook is updated to best represent the encoder’s outputs.

6. **Outcome:**  
   After training, the VQ-VAE learns a codebook that efficiently represents common features of handwritten digits. When you feed a new digit image, it is encoded into one of these discrete representations, compressed, and then decoded back to a high-quality reconstruction.

---

## Recap in Simple Terms

- **Imagine** you are compressing a photo using a small palette of colors.
- **The encoder** breaks the photo into features.
- **Quantization** replaces those features with the closest matching “color” (codebook entry).
- **The decoder** then uses these limited colors to recreate the photo.
- **The loss function** (which combines reconstruction and regularization terms) teaches the system to pick a palette that represents the data well and to reconstruct the image accurately.
