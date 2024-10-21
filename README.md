# DeTextify (SNN-VAE Text Remover)

## Overview

This project implements a **SNN** using a **Convolutional VAE** architecture with **LIF Neurons**. The network is designed for image reconstruction tasks, such as removing text from images, and incorporates the temporal dynamics characteristic of spiking neural networks.

The primary goal of this project is to explore how spiking neurons, which mimic the behavior of biological neurons, can be used in deep learning models for image processing. The spiking neurons accumulate input over multiple time steps and generate spikes that contribute to the overall output of the network.

## Architecture

The model is a **Spiking VAE** that consists of the following components:

### Encoder
- **Convolutional layers**: Extract feature maps from input images.
- **LIF Neurons**: Leaky integrate-and-fire neurons that process inputs over multiple time steps (default: 16).
- **Latent Space**: The latent space is parameterized by `mu` and `logvar`, and Bernoulli sampling is used to introduce stochasticity.

### Decoder
- **Transposed convolutional layers**: Used to upsample the latent representation back to the original image size.
- **LIF Neurons**: Reintroduced in the decoder to incorporate temporal information into the reconstruction.

### Temporal Dynamics
The model processes inputs over multiple timesteps (`T=16`). Each timestep integrates spikes generated by LIF Neurons, allowing for richer temporal dynamics and better feature representation.

## Features

- **Leaky Integrate-and-Fire (LIF) neurons**: These neurons accumulate input over time and fire when a threshold is reached, mimicking biological neurons.
- **Bernoulli sampling**: Used in the VAE's latent space to sample from the learned distribution.
- **Temporal processing**: Inputs are processed over multiple time steps to fully utilize the spiking dynamics of the network.
- **Customizable architecture**: Easily adjustable convolutional layers, latent dimensions, and spiking behavior.

## Performance Evaluation
### Structural Similarity Index (SSIM)

During training, we evaluate the model's performance using the **Structural Similarity Index (SSIM)** to measure the similarity between the original and reconstructed images.

- **SSIM Score**: The SSIM score ranges from 0 to 1, with 1 indicating a perfect match between the images.
- **Temporal Dynamics**: The introduction of LIF neurons and time steps helps in capturing more complex patterns, but tuning is required to find the optimal balance between time steps and accuracy.

## Overfitting and Underfitting Indicators
To monitor overfitting and underfitting, we track:

- **Training Loss**: Should decrease steadily during training.
- **Validation Loss**: Should not diverge from training loss; if it does, the model may be overfitting.

Loss and SSIM scores are plotted at the end of training to visualize performance.