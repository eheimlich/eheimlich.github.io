---
title: "Introduction to generalized linear models"
date: 2019-10-22
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
---

## 1. Introduction
I recently came across generalized linear models in one of my statistics classes at the University of Toronto. I was blown away by the power and simplicity of GLM's and how applicable they can be in industry.  

Generalized linear models are simply a generalization of linear regression to fit other types of data. In this post I am going to be walking through the basics of GLM's by first quickly recapping linear regression.

I am going to be assuming that you have an understanding of multiple linear regression. If not, I highly recommend brushing up before reading the rest of this post.

##2. Linear Regression
Linear regression is such a common and versatile tool that many students learn linear regression even
if it's the only statistical model they ever learn. Students in social sciences, physical sciences,
economics, statistics, mathematics, and computer science are probably exposed to linear regression at some point in their coursework.

If you have seen the formalization of multiple linear regression before, you may have encountered notation similar to the following:

$$ y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + ...+ \beta_k x_k + \epsilon $$

Where $$y$$ is the response, and there are $$k$$ predictor variables. In order to infer
meaning from the coefficients, we assume that the residual terms of the model, $$\epsilon$$, are normally
distributed.
