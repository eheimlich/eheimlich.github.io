---
title: "Introduction to generalized linear models"
date: 2019-10-22
tags: [Machine Learning, Python, Mathematics, Statistics]
excerpt: "A look at one of the most fundamental statistical models"
mathjax: True
---

## Introduction
I recently came across generalized linear models in one of my statistics classes at the University of Toronto. I was blown away by the power and simplicity of GLMs and how applicable they can be to solve a wide variety of problems. In this post I am going to be walking through what they are, how to use them, and some examples of GLM's used on real world data.  

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

$$ y_i = X_i \beta + \epsilon_i $$

Where $$y_i$$ is the response for the ith observation. $$ X_i $$ is the vector of covariates
for the ith observation. $$\beta$$ is a vector of the coefficients of the model. Finally, $$\epsilon_i$$ is the residual term for each observation. It is important to note that we haven't changed anything mathematically.

Now let's rewrite multiple linear regression one more time:

$$y_i \sim Normal(\mu_i, \sigma^2)$$

$$\mu_i = X_i \beta $$

What we are saying here is that the outcome for each observation is normally distributed with a mean of $$\mu_i$$ and variance of $$\sigma^2$$. In order to find $$\mu_i$$ for each observation we just find the output of the covariates and coefficients, $$ X_i \beta$$.

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

$$y_i \sim Bernoulli(\mu_i)$$

$$\mu_i = X_i \beta $$

Well there is a slight problem with this notation. We can see here that $$\mu_i$$ can be any positive or negative number as it just depends on $$X_i \beta$$. However, the parameter for the Bernoulli distribution must be between 0 and 1 since it is a probability. This leads us to the next topic of this post, link functions.

## Link functions
In order to make sure that the input to the Bernoulli distribution is between 0 and 1, let's add what's called a link function to transform the output from the covariates into something that our distribution can handle.

$$y_i \sim Bernoulli(\mu_i)$$

$$ln(\frac{\mu_i}{1- \mu_i}) = X_i \beta $$

We added what's called the logit link function to turn the output of $$X_i \beta$$ into a value between 0 and 1. You can verify yourself that this guarantees that $$\mu_i$$ will be between 0 and 1.

In fact, you may have come across this model before, this is simply **logistic regression**. Let's take a step back for a second, logistic regression is just a generalized linear model with the logit link function.

In fact, every single GLM has a link function. Wait a second, didn't we say that linear regression is a GLM? Shouldn't it have a link function? Let's go back to the notation for linear regression.

$$y_i \sim N(\mu_i, \sigma^2)$$

$$\mu_i = X_i \beta $$

There is a link function in there, it's just slightly hidden. It's called the identity link function because it doesn't change $$\mu_i$$ at all. Remember, we don't need to change $$\mu_i$$ because the supported domain of the normal distribution is all real numbers.

Every single GLM has a link function associated with it, and usually there is a standard link function for each distribution. For example,
if we were doing a Poisson GLM we would use the log link which is just the natural logarithm. We use the log link because it guarantees us that $$\mu_i$$ is positive, which is needed for a Poisson distribution.

We can see this simply when we solve for $$\mu_i$$:

$$ln(\mu_i) = X_i \beta$$

That implies that:

$$\mu_i = e^{X_i \beta}$$

Which means that $$\mu_i$$ must be positive.




## Finally an example

If your head is spinning with all this math, don't worry we are about to apply our knowledge on a real world data set.

We will be looking at the Titanic dataset from Kaggle [(Titanic Datset)](https://www.kaggle.com/c/titanic). In this dataset we are looking at how certain characteristics affect the chance of survival for passengers on the Titanic. We will be using Python to do all of our modelling, but all of this can be done in R as well.

The first row of the dataset is shown below. We can see a binary indicator for whether they survived or not, their class of travel, name, sex, age, fare, and more.

```python
my_data.head(1)
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
      <td>7.25</td>
      <td>NaN</td>
      <td>S</td>
    </tr>
  </tbody>
</table>
</div>

Let's start by doing a very simple Bernoulli GLM, also know as a logistic regression. We are using
a Bernoulli GLM because passenger survival is either they survived or didn't, a binary outcome. We are
modeling whether a passenger survived or not based on the fare they paid and their age.

I know I said we were done with the math, but let's recall our mathematical model for a logistic regression:

$$y_i \sim Bernoulli(\mu_i)$$

$$ln(\frac{\mu_i}{1- \mu_i}) = X_i \beta $$


Since we are modeling whether someone survived based off their fare, there are three $$\beta$$'s: intercept, fare, and age coefficients.

We will use the [(Statsmodels package)](https://www.statsmodels.org/stable/glm.html) to run our GLM, which is one of the ways to run GLM in Python. If you wanted to run the same analysis in R you could use the [(glm function)](https://stat.ethz.ch/R-manual/R-devel/library/stats/html/glm.html) in the R stats package.

In the Python code below, we designate the variable Survived as our outcome and Fare as our only independent variable. We then specify the Binomial distribution as our distribution family. Wait a second, didn't we say before that we are using a Bernoulli distribution?

It turns out that the Bernoulli distribution is just a special case of the Binomial distribution with one trial. For more information on the Bernoulli distribution feel free to check out [(Bernoulli distribution)](https://en.wikipedia.org/wiki/Bernoulli_distribution).

```python
model = glm(formula = 'Survived ~ Fare + Age', data = my_data, family = sm.families.Binomial())
model_results = model.fit()
print(model_results.summary())
```

                     Generalized Linear Model Regression Results                  
    ==============================================================================
    Dep. Variable:               Survived   No. Observations:                  714
    Model:                            GLM   Df Residuals:                      711
    Model Family:                Binomial   Df Model:                            2
    Link Function:                  logit   Scale:                          1.0000
    Method:                          IRLS   Log-Likelihood:                -445.67
    Date:                Tue, 26 Nov 2019   Deviance:                       891.34
    Time:                        17:12:30   Pearson chi2:                     785.
    No. Iterations:                     5   Covariance Type:             nonrobust
    ==============================================================================
                     coef    std err          z      P>|z|      [0.025      0.975]
    ------------------------------------------------------------------------------
    Intercept     -0.4171      0.186     -2.243      0.025      -0.782      -0.053
    Fare           0.0173      0.003      6.596      0.000       0.012       0.022
    Age           -0.0176      0.006     -3.103      0.002      -0.029      -0.006
    ==============================================================================


Let's check the output from the GLM we just ran. In the top part of the output we have some important metadata,
such as the link function, degrees of freedom, and more. The second part has our estimates for the coefficients in our model, i.e. our $$\beta$$'s.

## Interpretation of logistic regression

We can see in the bottom half of the output table above, three rows, one for the intercept and two for our covariates. We can see that Python's estimate for the fare coefficient is 0.0152 and -.0176 for the age coefficient. What do these numbers even mean?

Let's take a trip back to the start of this post and think about if this were linear regression how would we interpret these  numbers. If this were a linear regression, we would say that a one unit increase in fare leads to a .0152 of whatever our outcome is holding all other covariates in the model equal. The statement for age is exactly the same but with the age coefficient.

However, we know we are working with logistic regression and therefore the logit link function instead of the identity.

Let's look back at our link function:

$$ln(\frac{\mu_i}{1- \mu_i}) = X_i \beta $$

Now, we can say that a one unit increase in fare leads to a .0152 in the log odds of surviving while holding age constant.

What are the log odds? The log odds is the left hand side of the equation above: $$ln(\frac{\mu_i}{1- \mu_i})$$.

The log odds are difficult to interpret so we can take $$e ^ {ln(\frac{\mu_i}{1- \mu_i})} = \frac{\mu_i}{1- \mu_i}$$, and get the odds. Since $$e^{.0152} = 1.0153$$, we can say that the odds of someone surviving the titanic is 1.0153 times the odds of someone who paid $1 less in fare holding their age constant. Which means that if Alice, a 40 year old who paid $100 for their ticket and Daniel, a 40 year old who paid $50 dollars, then Alice would have $$ e^{(100-50) * 0.0173} = 2.375 $$ times the odds of surviving compared to Daniel.

Now that was quite a mouthful, let's try to interpret the age coefficient.

Since we have used the logit link function the coefficient for age represents the log odds. To extract the odds we will first take $$e^{-0.0176} = 0.983$$. Therefore, we can say that if Raphael is 21 years old and paid $200 for their ticket than they would have .983 times the odds of surviving relative to Michael, a 20 years old, who also paid $200 for their ticket.

## Interpretation of other GLMs

It's important to remember that our interpretation relied on the logit link function. The interpretation for different distributions is going to be different, because they may have different link functions.

For example, imagine we were doing Poisson regression with the following form:

$$y_i \sim Poisson(\lambda_i)$$

$$ln(\lambda_i) = X_i \beta $$

Notice how we used the log(natural) link function in the Poisson distribution since the $$\lambda$$ parameter of the Poisson distribution needs to be positive.

Since the link function is ln, there are no odds to speak of. When interpreting the coefficients we would just exponentiate them and then we could say that a one unit change in the variable of interest leads to that amount of change in the expected counts.

## Special thanks

I want to give a special thanks to Professor Patrick Brown at the University of Toronto. He taught my course on applied statistics and most of my knowledge on GLMs can be attributed to his excellent class.
