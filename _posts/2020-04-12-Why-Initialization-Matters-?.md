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

# Overview 

*Weight Initialization* is the most underrated concept in the deep learning terminology. I have seen many newbie deep learning practitioners and even some experienced ones ignoring this important concept.
Unlike some already available tutorials or blogs, we will not talk about why you should not initialize your weights with *all zeros or all ones* rather I will give a different perspective to weight initialization using eigenvalues and eigenvectors.

> Note: This post assumes readers to have basic familiarity with eigenvalues and eigenvectors.

*Basic Notations* :
- A: a random matrix whose entries are standard gaussian distributed of dimension (d,d).
- x: a random gaussian vector of dimension (d,1).
