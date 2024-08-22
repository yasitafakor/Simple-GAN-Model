# Simple GAN Model

## Project Overview

This project implements a basic Generative Adversarial Network (GAN) for generating images using the MNIST dataset. The GAN consists of two main components: the Generator and the Discriminator. The Generator creates images from random noise, while the Discriminator distinguishes between real and generated images.

## Generator Class

The `Generator` class creates synthetic images from random input vectors. It uses transposed convolutional layers to progressively upsample the input vector into an image.

### Layers

1. **First Transposed Convolutional Layer**:
   - **Input Channels**: `z_dim`
   - **Output Channels**: 256
   - **Kernel Size**: 4x4
   - **Stride**: 2
   - **Padding**: 1
   - **BatchNorm**: Applied
   - **Activation Function**: ReLU

2. **Second Transposed Convolutional Layer**:
   - **Input Channels**: 256
   - **Output Channels**: 128
   - **Kernel Size**: 4x4
   - **Stride**: 2
   - **Padding**: 1
   - **BatchNorm**: Applied
   - **Activation Function**: ReLU

3. **Third Transposed Convolutional Layer**:
   - **Input Channels**: 128
   - **Output Channels**: 1
   - **Kernel Size**: 3x3
   - **Stride**: 1
   - **Padding**: 1
   - **Activation Function**: Tanh

### Forward Method

Processes the input vector through each transposed convolutional layer and activation function to generate an image.

## Discriminator Class

The `Discriminator` class determines whether an image is real or generated. It uses convolutional layers to extract features and a final linear layer to output a probability score.

### Layers

1. **First Convolutional Layer**:
   - **Input Channels**: 1
   - **Output Channels**: 64
   - **Kernel Size**: 4x4
   - **Stride**: 2
   - **Padding**: 1
   - **Activation Function**: LeakyReLU

2. **Second Convolutional Layer**:
   - **Input Channels**: 64
   - **Output Channels**: 128
   - **Kernel Size**: 4x4
   - **Stride**: 2
   - **Padding**: 1
   - **Activation Function**: LeakyReLU
   - **BatchNorm**: Applied

3. **Third Convolutional Layer**:
   - **Input Channels**: 128
   - **Output Channels**: 256
   - **Kernel Size**: 4x4
   - **Stride**: 2
   - **Padding**: 1
   - **Activation Function**: LeakyReLU

4. **Linear Layer**:
   - **Input Size**: Flattened feature map
   - **Output Size**: 1
   - **Activation Function**: Sigmoid

### Forward Method

Processes the image through convolutional layers and a final linear layer to output a probability score.

## Training Process

The training process alternates between updating the Discriminator and Generator to improve the quality of generated images.

### Steps to Train the GAN

1. **Define Loss Function**:
   - Use Binary Cross-Entropy (BCE) loss.

2. **Set Up Optimizers**:
   - Use Adam optimizers for both Generator and Discriminator.
     
3. **Training Loop**:
   - For each epoch:
     1. **Train the Discriminator**:
        - **Real Images**: Compute loss with real labels and perform backpropagation.
        
        - **Fake Images**: Generate fake images and compute loss with fake labels.
   
        - **Update Discriminator**: Step the optimizer.

     2. **Train the Generator**:
        - Generate fake images and compute loss with real labels to fool the Discriminator.
        
        - **Update Generator**: Step the optimizer.

4. **Visualize Results**:
   - Plot generated images periodically to track improvements.

   After several epochs, the generated images should begin to resemble MNIST digits.

