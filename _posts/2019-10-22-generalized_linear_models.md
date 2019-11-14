---
title: "Introduction to generalized linear models"
date: 2019-10-22
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "Linear Regression"
mathjax: True
---

## Introduction
I recently came across generalized linear models in one of my statistics classes at the University of Toronto. I was blown away by the power and simplicity of GLM's and how applicable they can be in industry. In this post I am going to be walking through what they are, how to use them, and some examples of GLM's used on real world data.  

Generalized linear models are simply a **generalization** of linear regression to fit other types of data. In this post I am going to be walking through the basics of GLM's by first quickly recapping linear regression.

I am going to be assuming that you have an understanding of multiple linear regression and very basic linear algebra. If not, I highly recommend brushing up before reading the rest of this post.

## Linear regression

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

## Generalized linear models

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

Well there is a slight problem with this notation. We can see here that $$\mu_i$$ can be any positive or negative number as it just depends on $$X_i^T \beta$$. However, the parameter for the Bernoulli distribution must be between 0 and 1 since it is a probability. This leads us to the next topic of this post, link functions.

## Link functions
In order to make sure that the input to the Bernoulli distribution is between 0 and 1, let's add what's called a link function to transform the output from the covariates into something that our distribution can handle.

$$Y_i \sim Bernoulli(\mu_i)$$

$$log(\frac{\mu_i}{1- \mu_i}) = X_i^T \beta $$

We added what's called the logit link function to turn the output of $$X_i^T \beta$$ into a value between 0 and 1. You can verify yourself that this guarantees that $$\mu_i$$ will be between 0 and 1.

In fact, you may have come across this model before, this is simply **logistic regression**. Let's take a step back for a second, logistic regression is just a generalized linear model with the logit link function.

In fact, every single GLM has a link function. Wait a second, didn't we say that linear regression is a GLM? Shouldn't it have a link function? Let's go back to the notation for linear regression.

$$Y_i \sim N(\mu_i, \sigma^2)$$

$$\mu_i = X_i^T \beta $$

There is a link function in there, it's just slightly hidden. It's called the identity link function because it doesn't change $$\mu_i$$ at all. Remember, we don't need to change $$\mu_i$$ because the supported domain of the normal distribution is all real numbers.

Every single GLM has a link function associated with it, and usually there is a standard link function for each distribution. For example,
if we were doing a Poisson GLM we would use the log link which is just the natural logarithm. We use the log link because it guarantees us that $$\mu_i$$ is positive, which is needed for a Poisson distribution.

We can see this simply when we solve for $$\mu_i$$:

$$ln(\mu_i) = X_i^T \beta$$

That implies that:

$$\mu_i = e^{X_i^T \beta}$$

Which means that $$\mu_i$$ must be positive.




## Finally an example

If your head is spinning with all this math, don't worry we are about to apply our knowledge on a real world data set. We will be looking at the Titanic dataset from Kaggle [(Titanic Datset)](https://www.kaggle.com/c/titanic)

```python
my_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>PassengerId</th>
      <th>Survived</th>
      <th>Pclass</th>
      <th>Name</th>
      <th>Sex</th>
      <th>Age</th>
      <th>SibSp</th>
      <th>Parch</th>
      <th>Ticket</th>
      <th>Fare</th>
      <th>Cabin</th>
      <th>Embarked</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>0</td>
      <td>3</td>
      <td>Braund, Mr. Owen Harris</td>
      <td>male</td>
      <td>22.0</td>
      <td>1</td>
      <td>0</td>
      <td>A/5 21171</td>
      <td>7.2500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>1</td>
      <td>1</td>
      <td>Cumings, Mrs. John Bradley (Florence Briggs Th...</td>
      <td>female</td>
      <td>38.0</td>
      <td>1</td>
      <td>0</td>
      <td>PC 17599</td>
      <td>71.2833</td>
      <td>C85</td>
      <td>C</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>1</td>
      <td>3</td>
      <td>Heikkinen, Miss. Laina</td>
      <td>female</td>
      <td>26.0</td>
      <td>0</td>
      <td>0</td>
      <td>STON/O2. 3101282</td>
      <td>7.9250</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>1</td>
      <td>1</td>
      <td>Futrelle, Mrs. Jacques Heath (Lily May Peel)</td>
      <td>female</td>
      <td>35.0</td>
      <td>1</td>
      <td>0</td>
      <td>113803</td>
      <td>53.1000</td>
      <td>C123</td>
      <td>S</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>0</td>
      <td>3</td>
      <td>Allen, Mr. William Henry</td>
      <td>male</td>
      <td>35.0</td>
      <td>0</td>
      <td>0</td>
      <td>373450</td>
      <td>8.0500</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>




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
    Date:                Thu, 14 Nov 2019   Deviance:                       1117.6
    Time:                        11:15:20   Pearson chi2:                     934.
    No. Iterations:                     5   Covariance Type:             nonrobust
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     -0.9413      0.095     -9.895      0.000      -1.128      -0.755
    Fare           0.0152      0.002      6.809      0.000       0.011       0.020
    ==============================================================================
