---
title: "Models from Scratch Part 1: Linear Regression"
date: 2019-09-01
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
header:
  image: "/images/conference.jpg"
---

Starting off my first series with linear regression is quite fitting since this was the first model
that I learned about in university(Shoutout Professor Mark Ebden). In fact,
linear regression is so common and versitile that many students learn linear regression even
if it's the only ML model they ever learn. Students in social sciences, physical sciences,
economics, statistics, mathemtatics, computer science and more all utilize linear regression
in their fields.

Machine learning models are often used for two primary purposes: prediction and inference. Prediction
is when we have some training data and our goal is to predict an outcome for fresh data. In this situation,
we don't particularly care **how** we get the prediction as long as it performs well.

Inference on the other hand focuses on how the fuetures effect the outcome variable. We care about
how specific changes in our feutures end up effecting the outcome.

While these ideas may feel abstract, let's think about them more concreatly. Let's put ourselves in the shoes
of a data scientist for a major global airline. In order to know how many extra seats to sell on any given flight we would want a model to predict how many passengers would show up for a flight.  In this case we may not care about why the passengers are not showing up, only that we can accuratly predict how many show up. 
about which factors lead
