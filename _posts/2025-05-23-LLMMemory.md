---
layout: post
title: Train Big, Plan Smart - How to Calculate Memory and Estimate GPUs for LLMs
subtitle: Unlocking the Basics

image: '/img/llm_training.png'
share-img: '/img/llm_training.png'
published: false
author: Shreyans Dhankhar
date: 2025-05-06
tags:
  - LLMTraining
  - Memory estimation
  - GPU sizing
  - Generative AI
  - Model Scaling
---
 
Training large language models isn’t just a question of can you do it—it’s a question of how smartly you do it. If you've ever wondered how researchers train those massive AI models with billions of parameters, it all starts with smart planning. Behind every successful LLM training run is a well-thought-out estimate of memory usage and compute resources.

In this guide, we’ll break down the key factors that influence GPU selection, memory allocation, and the complex relationship between them—empowering you to make smarter decisions when scaling LLMs for efficient, high-quality training..

> Note: This blog assumes that readers have a basic understanding of deep learning concepts such as model parameters, gradients, backpropagation etc.

## Step 1: Estimating Memory Requirements :

To begin our planning, let’s assume we’re training a transformer-based language model with 1 billion parameters. Before we consider how many GPUs we’ll need—or how many tokens we want to process—we first need to understand the core memory requirements for training the model in a mixed precision setting.

Mixed precision training, which typically uses FP16 for storage and FP32 for some operations, significantly reduces memory usage while maintaining training stability. This is especially important when scaling to large models.

In this step, we'll estimate the memory consumed by:
- Model weights
- Gradients
- Optimizer states (Adam)

These three components form the base memory footprint of the model—excluding activation memory, which we’ll address later when discussing token throughput and batch size.

### Step 2: Byte-by-Byte Memory Breakdown

In a mixed precision setting, different components of the training process are stored at different precisions. Here’s how it breaks down:

#### 1. Model Weights
- Each parameter is stored in **FP16 (2 bytes)**.
- For 1 billion parameters:
1B × 2 bytes = 2 GB
> 1B × 2 bytes = 2 GB


#### 2. Gradients
- Gradients are also stored in **FP16 (2 bytes)** per parameter.
- For 1 billion parameters:
> 1B × 2 bytes = 2 GB 


#### 3. Optimizer States (Adam)
- Adam optimizer maintains **three additional states** per parameter:
  - *Momentum Term*
  - *Variance Term*
  - *Gradients*
- Each of these are stored in **FP32 (4 bytes)** for numerical stability.
- So, each parameter requires 12 bytes 
> 1B × 12 bytes = 12 GB  

#### 4. Activations
- Depends on the batch size and context length. 


---

### Total Memory (Model Parameters Only)

| Component         | Precision | Size per Param | Total (1B params) |
|------------------|-----------|----------------|-------------------|
| Weights          | FP16      | 2 bytes        | 2 GB              |
| Gradients        | FP16      | 2 bytes        | 2 GB              |
| Optimizer States | FP32      | 12 bytes        | 12 GB              |
| **Total**        | —         | —              | **16 GB**         |

This **16 GB** is the **base memory** required per model replica—not including activations or temporary memory used during forward/backward passes. In practice, you'll need additional memory headroom for:

- Activation storage
- CUDA workspace
- Data loading overhead
- Checkpointing buffers 

> Total memory required ≈ 16× the number of model parameters
