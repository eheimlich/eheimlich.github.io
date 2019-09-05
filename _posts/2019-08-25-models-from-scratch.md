---
title: "My First Series: Models From Scratch"
date: 2019-08-25
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "My First Series"
mathjax: True
header:
  image: "/images/conference.jpg"
---

Today I am excited to announce my first ever series on my blog called Models from
Scratch. This will be a multi-part series where I go through several popular
machine learning algorithms and code them from scratch in Python.

## Motivation

Machine learning is an incredibly valuable tool in a Data Scientist's toolkit. With the advent of
packages for every single machine learning algorithm it is very easy to lose sight of
what is being done "under the hood". Running a machine learning model can be done with just a few
lines of code without really understanding the math behind the package.

In this series I am going to be sharpening my theoretical knowledge of machine learning algorithms by translating the mathematics of the algorithms
into code. The code won't be optimized for large datasets, because the goal of the code is to help understand the theoretical aspects of the model.

## Potential posts

I am hoping to cover a wide spectrum of both supervised and unsupervised learning
models in the series. I may add or remove some models form the list depending on my time, interests, and new methods I learn in class.

### Supervised learning
1. Linear Regression
2. Penalized Regression: Lasso, Ridge, and Elastic Net
2. Logistic Regression
3. K-Nearest Neighbors
4. Tree Based Methods: Decision Trees, Random Forests, and Gradient Boosted Machines

### Unsupervised Learning
1. k-Means Clustering
2. Hierarchical Clustering
3. PCA

## Object Oriented Design

Many machine learning models are extensions of other machine learning models. For example, LASSO regression
is merely an extension of linear regression with an added penalty term. When designing the code for each model we
want to be cognisant of how the code could be used later on. In the case of the LASSO we would want to inherit most of the code
from linear regression and only override what is necessary to change. As a result, my goal is to heavily utilize object oriented software design principles when writing the code.

## Feedback

As a young data scientist it is important to continuously be learning. Please
comment down below any advice or suggestions that you have. I may make mistakes along the way
and I appreciate all constructive feedback. If you don't feel comfortable commenting on the blog,
feel free to email or connect with me on LinkedIn.
