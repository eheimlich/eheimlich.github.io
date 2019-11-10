---
title: "Introduction to generalized linear models"
date: 2019-10-22
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
---

## 1. Introduction
I recently came across generalized linear models in one of my statistics classes at the University of Toronto. I was blown away by the power and simplicity of GLM's and how applicable they can be in industry. In this post I am going to be walking through what they are, how to use them, and some examples of GLM's used on real world data.  

Generalized linear models are simply a **generalization** of linear regression to fit other types of data. In this post I am going to be walking through the basics of GLM's by first quickly recapping linear regression.

I am going to be assuming that you have an understanding of multiple linear regression and very basic linear algebra. If not, I highly recommend brushing up before reading the rest of this post.

## 2. Linear Regression

Linear regression is such a common and versatile tool that many students learn linear regression even
if it's the only statistical model they ever learn. Students in social sciences, physical sciences,
economics, statistics, mathematics, and computer science are probably exposed to linear regression at some point in their coursework.

If you have seen the formalization of multiple linear regression before, you may have encountered notation similar to the following:

$$ y_i = \beta_0 + \beta_1 x_{i1} + \beta_2 x_{i2} + ...+ \beta_k x_{ik} + \epsilon_i $$

Where $$y_i$$ is the response for the ith observation, and there are $$k$$ predictor variables. In order to infer
meaning from the coefficients, we assume that the residual term for each observation, $$\epsilon_i$$, follows a normal
distribution.

Now let's rewrite the previous model using matrix notation to make our lives easier:

$$ Y_i = X_i^{T} \beta + \epsilon_i $$

Where $$Y_i$$ is the response for the ith observation. $$ X_i $$ is the vector of covariates
for the ith observation. $$\beta$$ is a vector of the coefficients of the model. Finally, $$\epsilon_i$$ is the residual term for each observation. It is important to note that we haven't changed anything mathematically.

Now let's rewrite multiple linear regression one more time:

$$Y_i \sim N(\mu_i, \sigma^2)$$

$$\mu_i = X_i^T \beta $$

What we are saying here is that the outcome for each observation is normally distributed with a mean of $$\mu_i$$ and variance of $$\sigma^2$$. In order to find $$\mu_i$$ for each observation we just find the output of the covariates and coefficients, $$ X_i^T \beta$$.

In this third formulation of multiple linear regression, we still haven't changed anything mathematically. We are only doing this to make it easier to **generalize** multiple linear regression later.   

## 3. Generalized linear models

When we were working with linear regression, we were working with normally distributed outcome data. Now, imagine our outcome was a yes or no, a discrete count, or a continuous variable that isn't normally distributed. Our assumptions for linear regression completely fall apart, and we need a new tool.

This is where our friend generalized linear models comes to help us. It is still a linear model but now our outcome can come from any distribution from the exponential family. The exponential family of distributions is just a collection of distributions that have similar density functions. We won't worry too much in this post about density functions, so if they sound a bit scary don't worry.

The exponential family of distributions include some of the most common distributions:
* Normal
* Bernoulli
* Poisson
* Exponential
* Chi-squared
* Gamma
* and more!

Let's jump into a quick example where we will introduce some new terminology. Imagine we are interested in
modeling a binary outcome. For example, whether or not someone completed rehab treatment. We could try to use a linear regression. However, a linear regression assumes our outcome is normally distributed which means that the outcome could be any continuous value between $$\infty$$ and $$-\infty$$. We can see how this would pose a problem with a binary outcome.  

The Bernoulli distribution has only 1 parameter which is the probability of being assigned a 1. Let's make that a little bit more concrete. In the example of modeling drug rehab completion, we could say that the chances of completion for a specific individual follow a $$Bernoulli(.7)$$. Which means that the person's chances of completing their drug rehab is 70%.

Could this below be a good way to model drug rehab completion?

$$Y_i \sim Bernoulli(\mu_i)$$

$$\mu_i = X_i^T \beta $$

Well there is a slight problem with this notation. We can see here that $$\mu_i$$ can be any positive or negative number as it just depends on $$X_i^T \beta$$. However, the parameter for the Bernoulli distribution must be between 0 and 1 since it is a probability.

This leads us to the next topic of this post, **link functions**. In order to make sure that the input to the Bernoulli distribution is between 0 and 1, we will add what's called a link function to transform the output from the covariates into something that our distribution can handle.

$$Y_i \sim Bernoulli(\mu_i)$$

$$log(\frac{\mu_i}{1- \mu_i})i = X_i^T \beta $$


So what can we do? Let's check back to the distributions we can use with GLM, the exponential family. The Bernoulli distribution seems
like a perfect candidate because it takes a value of 1 or 0 with a certain probability. Let's try to write out our GLM mathematically using the notation we used at the end of section 2.


```python
model = glm(formula = 'Survived ~ Fare', data = my_data, family = sm.families.Binomial())
model_results = model.fit()
print(model_results.summary())
```

                     Generalized Linear Model Regression Results                  
    ==============================================================================
    Dep. Variable:               Survived   No. Observations:                  891
    Model:                            GLM   Df Residuals:                      889
    Model Family:                Binomial   Df Model:                            1
    Link Function:                  logit   Scale:                          1.0000
    Method:                          IRLS   Log-Likelihood:                -558.78
    Date:                Thu, 24 Oct 2019   Deviance:                       1117.6
    Time:                        15:43:46   Pearson chi2:                     934.
    No. Iterations:                     5   Covariance Type:             nonrobust
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     -0.9413      0.095     -9.895      0.000      -1.128      -0.755
    Fare           0.0152      0.002      6.809      0.000       0.011       0.020
    ==============================================================================
