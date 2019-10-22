---
title: "Introduction to generalized linear models"
date: 2019-10-22
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
---

## Introduction
I recently came across generalized linear models in one of my statistics classes at the University of Toronto. I was blown away by the power and simplicity of GLM's and how applicable they can be in industry.  

Generalized linear models are simply a generalization of linear regression to fit other types of data. In today's post I am going to be walking through the basics of GLM's by first introducing linear regression.

## Linear Regression
Linear regression is such a common and versatile tool that many students learn linear regression even
if it's the only statistical model they ever learn. Students in social sciences, physical sciences,
economics, statistics, mathematics, and computer science are probably exposed to linear regression at some point in their coursework.

### Theory
If you have seen the formalization of linear regression before, you may have seen this notation:
$$ y = \beta_0 + \beta_1 x + \epsilon $$
