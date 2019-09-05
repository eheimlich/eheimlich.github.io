---
title: "Models from Scratch Part 1: Linear Regression"
date: 2019-09-01
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
header:
  image: "/images/conference.jpg"
---
## Introduction

Starting off my first series with linear regression is quite fitting since this was the first model
that I learned about in university. Thank you Professor Mark Ebden. In fact,
linear regression is so common and versatile that many students learn linear regression even
if it's the only machine learning model they ever learn. Students in social sciences, physical sciences,
economics, statistics, mathematics, and computer science are probably exposed to linear regression at some point in their coursework.

## Prediction & Inference

Machine learning models are often used for two primary purposes: prediction and inference. Prediction
is when we have some training data and our goal is to predict an outcome for fresh data. In this situation,
we don't particularly care **how** we get the prediction as long as it performs well.

Inference on the other hand focuses on how the features effect the outcome variable. We care about
how specific changes in our features end up effecting the outcome.

While these ideas may feel abstract, let's think about them more concretely. Let's put ourselves in the shoes
of a data scientist at a major global airline. In order to know how many extra seats to sell on any given flight we would want a model to predict how many passengers would show up for a flight.  In this case we may not care about why the passengers are not showing up, only that we can accurately predict how many show up. In this business situation we may not care about model **interpretability**.

However, if we were interested in knowing **how much** emailing passengers before the flight impacted passengers showing up
we would care more about model **interpretability**.  

Why did we spend the time talking about prediction vs inference? It sets the stage for understanding where linear regression
shines and what functionality we want to code up.

## Linear Regression

In this post I am going to be using matrix notation for defining and solving the linear regression. Linear regression is a model
that at its' core fits a straight line through a set of points in $$R ^ N  $$.
