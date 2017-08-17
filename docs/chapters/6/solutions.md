---
layout: page
title:  "Chapter 6: Linear Model Selection and Regularization"
category: "solution"
chapter: 6
use-math: true
---

<h1 class="post-subtitle">Conceptual</h1>

### 1.

**a)**

The best subset selection model for a given number of predictors will have an $RSS$ either smaller than or equal to the RSS of either stepwise selection model for the same number of predictors. This is because the metric determining model selection for a given count of predictors $k$ is minimization of RSS and best subset selection explores every possible combination of predictors $\binom{p}{k}$, whereas forward and backward stepwise selection only evaluate $(p-k)$ and $(k-1)$ models respectively.

**b)**

Unable to say as there's no suitable test error estimate taken into account when selecting a model for a particular number of predictors $k$. Generally speaking this is dependent on the extent to which the chosen learning method overfits the training data. Assuming overfit is not a huge problem then you would expect best subset selection to give the lowest test RSS, but the assumption cannot be tested without an appropriate validation strategy such as cross-validation in the first place.

**c)**

**i.** True

**ii.** True

**iii.** False

**iv.** False

**v.** False


### 2. 

**a)**

iii. The lasso is simply least squares with the following additional constraint on the coefficient estimates.

$$
\sum\limits_{j=1}^p |\beta_j| \leq s
$$

The additional constraints means higher bias, if the increase in bias error is lower than the decrease in variance then prediction accuracy is improved.

**b)**

iii. For the same reasons as above, but the constraint for ridge regression is:

$$
\sum\limits_{j=1}^p \beta_j^2 \leq s
$$

**c)**

ii. Non linear methods are more flexible than least squares, hence variance will be greater. But if the underlying relationship is truly non-linear the decrease in bias will be greater and prediction accuracy will be increased.

### 3.

**a)**

iv. Steadily decrease. When s = 0 all coefficients are constrained to 0 and training RSS will be maximized. When s is sufficiently large we obtain the ordinary least squares coefficient estimates and hence the lowest training RSS.

**b)**

ii. Decrease initially, then increase. The OLS model will likely start overfitting the training data with a less strict constraint which lowers training RSS but doesn't generalize to test RSS. 

**c)**

iii. As the constraint is relaxed more variance is introduced to the model.

**d)**

iv. As the constraint is relaxed the squared bias of the model is reduced.

**e)**

v. Remain constant, it's called irreducible for a reason.

### 4.

**a)**

iii. When $\lambda$ is zero we have OLS which has the minimum training RSS by definition. As $\lambda$ is increased training RSS will decrease.

**b)**

ii. We expect the ridge regression model to generalize better as it's less prone to overfitting, hence test RSS will follow the usual characteristic U shape.

**c)**

iv. As shrinkage parameter grows, flexibility decreases, hence variance decreases.

**d)**

iii. As shrinkage parameter grows, flexibility decreases, hence bias increases.

**e)**

v. *IRREDUCIBLE*.

### 5.

**a)**

$$
\begin{align*}
f(\beta_1, \beta_2) &= \sum\limits_{i=1}^n(y_i - \beta_0 - \sum\limits_{j=1}^p\beta_jx_{ij})^2 + \lambda\sum\limits_{j=1}^p\beta_j^2 \\
\end{align*}
$$

Under conditions:

$$
\beta_0 = 0 \\
x_{11} = x_{12} = x_1 \\
x_{21} = x_{22} = x_2 \\
y_1 + y_2 = 0 \\
x_{11} + x_{21} = 0 \\
x_{12} + x_{22} = 0
$$

Simplifies to:

$$
\begin{align*}
f(\beta_1, \beta_2) &= 2(y_1 - x_1(\beta_1 + \beta_2))^2 + \lambda(\beta_1^2 + \beta_2^2)
\end{align*}
$$

**b)**

Partial derivatives:

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_1} &= 4(y_1 - x_1(\beta_1 + \beta_2))(-x_1) + 2\lambda\beta_1 \\
&= -2x_1(y_1 - x_1\beta_1 -x_1\beta_2) + \lambda\beta_1 \\
&= \beta_1(\lambda + 2x_1^2) + 2x_1^2\beta_2 - 2x_1y_1
\end{align*}
$$

and by clear symmetry,

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_2} &= \beta_2(\lambda + 2x_1^2) + 2x_1^2\beta_1 - 2x_1y_1
\end{align*}
$$

Set partial derivatives equal to zero.

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_1} &= 0 = \beta_1(\lambda + 2x_1^2) + 2x_1^2\beta_2 - 2x_1y_1 \\
\lambda\beta_1 &= 2x_1y_1 - 2x_1^2(\beta_1 + \beta_2)
\end{align*}
$$

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_1} &= 0 = \beta_2(\lambda + 2x_1^2) + 2x_1^2\beta_1 - 2x_1y_1 \\
\lambda\beta_2 &= 2x_1y_1 - 2x_1^2(\beta_1 + \beta_2) = \lambda\beta_1
\end{align*}
$$

Hence $\beta_1 = \beta_2$.

**c)**

We can borrow most of the math from part a as the penalty term is the only part that changes. Hence:

$$
\begin{align*}
f(\beta_1, \beta_2) &= 2(y_1 - x_1(\beta_1 + \beta_2))^2 + \lambda(|\beta_1| + |\beta_2|)
\end{align*}
$$

**d)**

The lasso coefficients can't be unique because taking the partial derivatives of the optimization function results in multiple cases as we're taking the derivative of an absolute value. i.e.

For $\beta_1 > 0$,

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_1} &= 4(y_1 - x_1(\beta_1 + \beta_2))(-x_1) + \lambda\\
\end{align*}
$$

For $\beta_1 < 0$,

$$
\begin{align*}
\frac{\partial f(\beta_1, \beta_2)}{\partial \beta_1} &= 4(y_1 - x_1(\beta_1 + \beta_2))(-x_1) - \lambda\\
\end{align*}
$$

And similarly for $\beta_2$, these solutions are found by setting each of these cases to 0.

### 6.

**a)**

<p align="center">
  <img src="img/6a.png"/>
</p>

**b)**

<p align="center">
  <img src="img/6b.png"/>
</p>

### 7.

Not entirely sure how to go about this.


<h1 class="post-subtitle">Applied</h1>

### 8.

