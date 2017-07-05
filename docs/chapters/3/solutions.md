---
layout: page
title:  "Chapter 3: Linear Regression"
category: "solution"
use-math: true
---

<h1 class="post-subtitle">Conceptual</h1>

### 1.
Each p-value corresponds to the probability that the null hypothesis is true, the null hypothesis being that there is no relationship between the predictor (one of TV, radio or newspaper) and sales given the other two predictors are held constant. *i.e. There is no relationship between TV advertising spend and sales given the advertising spend on radio and newspaper is held constant.*

Given the p-values we can conclude that both TV and radio advertising spend have a relationship to sales while newspaper does not.

### 2.
Simply the difference between classification and regression. Classification involves identifying which category an observation belongs to, regression involves predicting a quantifiable output value.

### 3.
**a)**

Let's construct the entire model so it's easier to look at.

$$ Salary = 50 + 20(GPA) + 0.07(IQ) + 35(Female) + 0.01(GPA)(IQ) - 10(GPA)(Female) $$

The correct answer is  iii. For a fixed value of IQ and GPA, males earn more on average than females provided that the GPA is high enough. Simplify the form of the equation to the following:

$$ Salary = 50 + 20(GPA) + 0.07(IQ) + (Female)(35 - 10(GPA)) + 0.01(GPA)(IQ) $$

We see that only females suffer the negative affect on starting salary due to term $\hat{\beta_5}$ depending on GPA. Let's run a test case between a male and female with GPA 4.0 to prove it though.

Male, GPA 4: $ Salary = 50 + 80 + 0.07(IQ) + 0 + 0.04(IQ) $

Female, GPA 4: $ Salary = 50 + 80 + 0.07(IQ) - 5  + 0.04(IQ) $

Hence, provided GPA is quite high males will earn more on average than females.

**b)**

We can reuse the previous equation luckily!

$$ Salary = 50 + 80 -5 + 0.11(110) = 137.1 * ($1000)$$

**c)**

False. You need to compute the ratio of the coefficient to the standard error associated with the predictor to determine if there is a relationship between the predictor and the output. Despite the coefficient being small, if the standard error is significantly smaller that still indicates strongly that the interaction effect has a relationship to the output.

### 4.

**a)**

The training RSS for the cubic regression will never be larger than the linear regression, it will only be equal to or smaller. This is just a consequence of the mathematics of using least-squares. Consider the respective formulas for the RSS of each regression.

$$ RSS_{linear} = \sum\limits_{i=1}^n (y_i - \beta_0 - \beta_1x_i)^2 $$

$$ RSS_{cubic} = \sum\limits_{i=1}^n (y_i - \beta_0 - \beta_1x_i - \beta_2x_i^2 - \beta_3x_i^3)^2 $$

Least squares picks coefficients which minimise RSS by definition. Now consider the case where $\beta_2, \beta_3$ are non-zero and the training RSS for cubic is worse than linear. This is clearly impossible because the least squares method minimises RSS and the cubic regression can simply be made equivalent to the linear regression by setting $\beta_2 = \beta_3 = 0$. Hence the training RSS of the cubic regression can never be more than the training RSS of the linear regression. This concept can also be extended. The addition of any predictor to an existing regression model will never increase the RSS calculated on the same training set.

**b)**

I would expect the test RSS for the linear regression to be smaller than that of the cubic regression as a simply consequence of it matching the true relationship to a greater degree. It should be noted that this is not deterministic unlike part a, it is possible (though unlikely) for the test RSS of the cubic regression to be smaller.

**c)**

Using the same argument as in part a, the training RSS for the cubic regression will always be smaller.

**d)**

In this case I would expect the test RSS for the cubic regression to be smaller, as a simple consequence of it being able to adapt to some degree of non-linearity. Again this is not deterministic.

### 5.

**a)**

We have

$$ \hat{y_i} = x_i\hat{\beta} $$

$$ \hat{beta} = \frac{\sum\limits_{j=1}^nx_jy_j}{\sum\limits_{k=1}^nx_k^2} $$

Note we're not using the $i$ and $i'$ terminology because it's needlessly confusing in this case.

$$ \hat{y_i} = x_i\frac{\sum\limits_{j=1}^nx_jy_j}{\sum\limits_{k=1}^nx_k^2} $$

Take $x_i$ inside the summation term as it's a constant in this case.

$$ \hat{y_i} = \frac{\sum\limits_{j=1}^nx_ix_jy_j}{\sum\limits_{k=1}^nx_k^2} $$

Take the summation over j over the fraction as the denominator has no relation to it. Take $y_j$ outside the numerator for clarity.

$$ \hat{y_i} = \sum\limits_{j=1}^n\frac{x_ix_j}{\sum\limits_{k=1}^nx_k^2}y_j $$

This is the form we want, therefore:

$$ a_j = \frac{x_ix_j}{\sum\limits_{k=1}^nx_k^2} $$

### 6.

$$ \hat{y_i} = \hat{\beta}_0 + \hat{\beta_1}x_i $$

Substitute in the point ($\overline{x}, \overline{y}$)

$$
\begin{align*}
\overline{y} &= \hat{\beta_0} + \hat{\beta_1}\overline{x} \\
 &= \overline{y} - \hat{\beta_1}\overline{x} + \hat{\beta_1}\overline{x} \\
 &= \overline{y}
\end{align*}
$$

Thereforce the point satisfies the equation, the least squares line in simple regression will always pass through the point.

### 7.

$$ R^2 = \frac{TSS-RSS}{TSS} $$

$$ Cor(X,Y) = \frac{\sum\limits_{i=1}^n x_iy_i}{\sqrt{\sum\limits_{i=1}^n x_i^2} \sqrt{\sum\limits_{i=1}^n y_i^2}} $$

Where $TSS = \sum y_i^2$ and $RSS = \sum(y_i - \hat{y_i})^2$ and assuming $\overline{x} = \overline{y} = 0$.

$$
\begin{align*}
R^2 &= \frac{TSS-RSS}{TSS} \\
&= \frac{\sum\limits_{i=1}^n y_i^2 - \sum\limits_{i=1}^n(y_i - \hat{y_i})^2}{\sum\limits_{i=1}^n y_i^2} \\
&= \frac{\sum\limits_{i=1}^n y_i^2 - (y_i - \hat{y})^2}{\sum\limits_{i=1}^n y_i^2} \\
&= \frac{\sum\limits_{i=1}^n 2\hat{y}y_i - \hat{y}^2}{\sum\limits_{i=1}^n y_i^2}
\end{align*}
$$

Under the assumption that $\overline{y} = \overline{x} = 0$, $\hat{\beta_0} = 0$ and $\hat{\beta_1} = \frac{\sum x_iy_i}{\sum x_i^2}$. Therefore $\hat{y} = \hat{\beta_1}x$. Substituting that in:

$$
\begin{align*}
R^2 &= \frac{\sum\limits_{i=1}^n 2\beta_1x_iy_i - (\hat{\beta_1}x_i)^2}{\sum\limits_{i=1}^n y_i^2} \\
&= \hat{\beta_1}\frac{2\sum\limits_{i=1}^n x_iy_i - \hat{\beta_1}\sum\limits_{i=1}^n x_i^2}{\sum\limits_{i=1}^n y_i^2} \\
&= \hat{\beta_1}\frac{2\sum\limits_{i=1}^n x_iy_i - \frac{\sum x_iy_i}{\sum x_i^2}\sum\limits_{i=1}^n x_i^2}{\sum\limits_{i=1}^n y_i^2} \\
&= \hat{\beta_1}\frac{2\sum\limits_{i=1}^n x_iy_i - \sum\limits_{i=1}^n x_iy_i}{\sum\limits_{i=1}^n y_i^2} \\
&= \hat{\beta_1}\frac{\sum\limits_{i=1}^n x_iy_i}{\sum\limits_{i=1}^n y_i^2}\\
&= \frac{\sum x_iy_i}{\sum x_i^2}\frac{\sum\limits_{i=1}^n x_iy_i}{\sum\limits_{i=1}^n y_i^2} \\
&= \frac{(\sum\limits_{i=1}^n x_iy_i)^2}{\sum\limits_{i=1}^n x_i^2 \sum\limits_{i=1}^n y_i^2} = Cor(X, Y)^2\\

\end{align*} 
$$




