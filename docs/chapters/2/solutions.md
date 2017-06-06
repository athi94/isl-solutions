---
layout: page
title:  "Chapter 2: Statistical Learning"
category: "solution"
use_math: true
---

Conceptual
==========

### 1.

**a)** More data means that the zero-mean error should itself play a smaller part in the overall estimate, as you're taking a larger sample of the error distribution as well which should tend to zero. Thus the tendency for a flexible method to overlearn would be diminished.

**b)** With a small dataset and a large amount of predictors a flexible method will almost be guaranteed to overfit the data. Hence an inflexible method is better in this case.

**c)** Highly non-linear responses require more flexible learning methods. Inflexible methods won't be able to adapt appropriately and will resut  a high bias term.

**d)** An inflexible method will be better as the high variance in the error terms will make a flexible method overfit the data.

### 2. 

**a)** Regression, Inference. $n=500$, $p=3$. 

**b)** Classification, Prediction. $n=20$, $p=13$.

**c)** Regression, Prediction. $n=52$, $p=3$.

> Just remember that the output variable is not a predictor despite the question wording grouping them together.

### 3.

**a)** 

![Exercise 3A]({{site.baseurl}}/img/ch2/3a.jpg)

**b)** Bias is a result of the mathematical form of the training model not being matched to the underlying mathematical reality of the system being studied. Generally speaking, the more flexible the training model is the more likely it is to match the mathematical form of the system in question.

Variance refers to the change in our estimate of the systematic information function $\hat{f}$ when we use different sets of training data. It is minimal when flexibility is minimal, as is expected. When more flexibility is introduced variance will change as the learning method will be able to adapt to points easier as it has more degrees of freedom.

Test error is minimal at the point where flexibility most closely matches the underlying mathematical form of the system. Note that test error can never be below the Baye's error.

Training error is reduced as more flexibility is introduced due to the tendency for the model to incorporate the error in each point into it's estimate.

Baye's error is an irreducible constant that exists with no relation to the choice of learning model.

### 4.

**a)** Predicting the winner in a horse race. Predictors would be race history, frequency, fitness etc.

Using a classification of what political parties people vote for to infer information about what underlying demographic correspond to each political party. Predictors can again be age, salary, ethnicity, occupation, etc. 

Classifying observed astronomical objects automatically. Predictors would be luminosity, color, etc. This is a prediction problem.

**b)** Predicting salary of an individual. Predictors would be education level, age, ethnicity, sex. Prediction is the goal.

Inferring cause of unit defects in a manufacturing process where failure rate is the output variable. Predictors would be machinery, group, process variations, bins, variation in purchased component supplier.

Predicting budget necessary for a project. Predictors would be staff, length, scope, departments, licensing, etc.

**c)** Targeted marketing. Want to cluster consumers into known demographics to better target advertising towards each individual.

Cluster movies into groups by their characteristics. Allows you to predict content which a particular user may enjoy based on their own vieweing history.

Animal clustering. Group animals by characteristics to more easily understand possible evolutionary processes.

### 5.

|               | Advantages                                 | Disadvantages                                                                                |
|---------------|--------------------------------------------|----------------------------------------------------------------------------------------------|
| More Flexible | Better for highly non-linear relationships | More difficult to compute <br> <br> Can overfit data, incorporating  irreducible error into the model |
| Less Flexible | Easy to compute <br><br> Minimal variation         | Cannot fit non-linear data adequately                                                        |
{:.mtablestyle}

<br>
### 6.

|                | Advantages                                                                                                   | Disadvantages                                                                                                                   |
|----------------|--------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| Parametric     | Problem reduced to predicting a set of parameters for f                                                      | Assuming a form for f can restrict the accuracy of the generated model, aka high bias low variance.                             |
| Non-Parametric | No form assumption taken for f so same process can be used to fit highly varied and non-linear sets of data. | Very difficult to compute in comparison to a parametric model. <br><br> Need a greater number of observations to generate a good model. |
{:.mtablestyle}
<br>

### 7. 

**a)**

| Obs. | Distance $\pmb{(0, 0, 0)}$ |
|------|--------------------|
| 1    |                  3 |
| 2    |                  2 |
| 3    |           $\sqrt{10}$ |
| 4    |           $\sqrt{5}$ |
| 5    |           $\sqrt{2}$ |
| 6    |           $\sqrt{3}$ |
{:.mtablestyle}
<br>

**b)** Green. With K=1 our prediction is simply based on the output of a single nearest neighbour, which is Observation 5 as found in question 1.

**c)** Observations 3, 5, and 6 are included. That's two red, one green outcome. Hence red is the prediction.

**d)** Small K is better for highly non-linear decision boundaries. Including less items in the nearest neighbour calculations means there is less overlap of observations used among varying points, allowing subsequent points to vary more rapidly in their decision predictions.