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

This isn't correct whatsoever. You need to compute the ratio of the coefficient to the standard error associated with the predictor to determine if there is a relationship between the predictor and the output. Despite the coefficient being small, if the standard error is significantly smaller that still indicates significant evidence that the interaction effect is significant.

