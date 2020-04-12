---
layout: post
title: Weight Initialization and Eigen Vectors
subtitle: Journey from basics to advanced

image: '/img/weight-init.jpg'
share-img: '/img/weight-init.jpg'
published: true
author: Shreyans Dhankhar
date: 2020-04-07
tags:
  - weight
  - initialization
  - deep learning
  - xavier
  - kaiming
  - eigenvalue
  - eigenvector
---
 

*Weight Initialization* is the most underrated concept in the deep learning terminology. I have seen many newbie deep learning practitioners and even some experienced ones ignoring this important concept.
Unlike some already available tutorials or blogs, we will not talk about why you should not initialize your weights with *all zeros or all ones* rather I will give a different perspective to weight initialization using eigenvalues and eigenvectors.

> Note: This post assumes readers to have basic familiarity with eigenvalues and eigenvectors.

*Basic Notations* :
- A: a random matrix whose entries are standard gaussian distributed of dimension (k,k).
- x: a random gaussian vector of dimension (k,1).

We can think of a neural network as a stack of many layers where each layer does a linear transformation followed by a non-linear operation using a function commonly known as *activation function*. To keep this post simple and easily understandable, I will focus only on the linear transformation part.

The linear transformation part in our case is basically a repeated matrix operation A which can be written as:

![eqn](/img/pots1/eqn.JPG)
To start with we will take the value of k as 5 and randomly initializae the matrix A with standard gaussian. 

![Matrix Initialized](/img/pots1/mat1.JPG)

Let us now analyze the repeated multiplication by plotting the norm and the quotients of the norm.

![Matrix Initialized](/img/pots1/norm-quot.png)
