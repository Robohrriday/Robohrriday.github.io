---
layout: blog_template
title: "Simple Linear Regression and Correlation"
subtitle: "Understanding the relationship between slope parameter and correlation coefficient"
date: 2025-09-27
author: Robohrriday
tags: [statistics]
---

In simple linear regression, the slope parameter is a simple function of the correlation between the targets and predictors. I derive this result and discuss a few consequences.

Consider *simple linear regression* or linear regression with a single independent variable,

$$y_n = \alpha + \beta x_n + \varepsilon_n. \tag{1}$$

$\beta$ is the model's *slope*, and $\alpha$ is the model's *intercept*. There is an interesting relationship between the estimated linear coefficient $\hat{\beta}$ and Pearson's correlation coefficient between the predictors and targets, $\rho_{xy}$. The goal of this post is to understand this relationship better.

## Univariate normal equation

Let's rederive the normal equations for ordinary least squares (OLS), which minimizes the sum of squared residuals:

$$J(\beta, \alpha) = \sum_{n=1}^{N} (y_n - \alpha - \beta x_n)^2, \tag{2}$$

$$\hat{\alpha}, \hat{\beta} = \underset{\alpha,\beta}{\text{argmin}} \, J(\beta, \alpha).$$

We can find the minimizers for $\beta$ and $\alpha$ by differentiating $J$ w.r.t. these parameters and solving for them after setting the derivative equal to zero. (We are ignoring the endpoints and second-order conditions since this is an established result.)

First, let's solve for intercept $\alpha$. We take the derivative of the objective function w.r.t. to $\alpha$,

$$\frac{dJ}{d\alpha} = \sum_{n=1}^{N} \frac{d}{d\alpha} (y_n - \alpha - \beta x_n)^2$$

$$= \sum_{n=1}^{N} 2(y_n - \alpha - \beta x_n)(-1) \tag{3}$$

Setting this equal to zero and solving for $\alpha$:

$$\sum_{n=1}^{N} 2(y_n - \alpha - \beta x_n)(-1) = 0$$

$$\sum_{n=1}^{N} (y_n - \alpha - \beta x_n) = 0$$

$$\sum_{n=1}^{N} y_n - N\alpha - \beta \sum_{n=1}^{N} x_n = 0$$

$$\hat{\alpha} = \frac{1}{N} \sum_{n=1}^{N} y_n - \hat{\beta} \frac{1}{N} \sum_{n=1}^{N} x_n = \bar{y} - \hat{\beta} \bar{x} \tag{4}$$

## The slope-correlation relationship

Now let's solve for the slope $\beta$. Taking the derivative w.r.t. $\beta$:

$$\frac{dJ}{d\beta} = \sum_{n=1}^{N} 2(y_n - \alpha - \beta x_n)(-x_n) = 0$$

Substituting our expression for $\hat{\alpha}$ from equation (4):

$$\sum_{n=1}^{N} (y_n - (\bar{y} - \hat{\beta} \bar{x}) - \hat{\beta} x_n) x_n = 0$$

$$\sum_{n=1}^{N} ((y_n - \bar{y}) + \hat{\beta}(\bar{x} - x_n)) x_n = 0$$

$$\sum_{n=1}^{N} (y_n - \bar{y}) x_n + \hat{\beta} \sum_{n=1}^{N} (\bar{x} - x_n) x_n = 0$$

After some algebraic manipulation, this leads to:

$$\hat{\beta} = \frac{\sum_{n=1}^{N} (x_n - \bar{x})(y_n - \bar{y})}{\sum_{n=1}^{N} (x_n - \bar{x})^2} = \frac{\text{Cov}(x,y)}{\text{Var}(x)} \tag{5}$$

## Connection to correlation

The Pearson correlation coefficient is defined as:

$$\rho_{xy} = \frac{\text{Cov}(x,y)}{\sqrt{\text{Var}(x)} \sqrt{\text{Var}(y)}} \tag{6}$$

Substituting this into our expression for $\hat{\beta}$:

$$\hat{\beta} = \frac{\text{Cov}(x,y)}{\text{Var}(x)} = \rho_{xy} \frac{\sqrt{\text{Var}(x)} \sqrt{\text{Var}(y)}}{\text{Var}(x)} = \rho_{xy} \frac{\sqrt{\text{Var}(y)}}{\sqrt{\text{Var}(x)}} \tag{7}$$

Therefore:

$$\boxed{\hat{\beta} = \rho_{xy} \frac{\sigma_y}{\sigma_x}} \tag{8}$$

## Implications

This fundamental relationship reveals several important insights:

1. **Sign correspondence**: The slope $\hat{\beta}$ has the same sign as the correlation $\rho_{xy}$
2. **Scaling effect**: The slope is scaled by the ratio of standard deviations
3. **Standardized regression**: When variables are standardized ($\sigma_x = \sigma_y = 1$), then $\hat{\beta} = \rho_{xy}$

This connection between correlation and regression slope is fundamental to understanding linear relationships in data analysis.