---
title: "Models from Scratch Part 1: Linear Regression"
date: 2019-09-01
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
header:
  image: "/images/Rplot02.png"
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

### 1. Overview
Linear regression is a model that at its' core models the relationship between a continuous outcome and one or more independent variables.

We can formalize this intuition with mathematical notation in the case of a single independent variable:

$$ y = \beta_0 + \beta_1 x + \epsilon $$

In the rest of this post we will be using matrix notation and we want to generalize to data with n rows and p independent features. So let's rewrite the previous equation with matrix notation:

$$ y = X \beta + \epsilon $$

Where y is a $$ n \times 1 $$ matrix containing the outcome values. $$ X $$ is a $$n \times p + 1 $$ matrix containing the feature data. $$\beta$$ is a $$p + 1 \times 1$$ matrix of the coefficients of the model. Finally, $$\epsilon$$ is a $$n \times 1 $$ matrix of the error terms.
