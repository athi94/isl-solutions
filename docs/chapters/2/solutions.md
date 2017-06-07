---
layout: page
title:  "Chapter 2: Statistical Learning"
category: "solution"
use-math: true
---

<h1 class="post-subtitle">Conceptual</h1>

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

**c)** Observations 2, 5, and 6 are included. That's two red, one green outcome. Hence red is the prediction.

**d)** Small K is better for highly non-linear decision boundaries. Including less items in the nearest neighbour calculations means there is less overlap of observations used among varying points, allowing subsequent points to vary more rapidly in their decision predictions.

<br><br>

<h1 class="post-subtitle">Applied</h1>

### 8.

**a)**

``` r
college = read.csv(file = "datasets/College.csv", header = TRUE)
```

**b)**

Fix can take a while... you have to close the window before the program proceeds as well.

``` r
#fix(college)
```

Let's set rownames based on the University names in the first column, then remove that column from the actual data.

``` r
rownames(college)=college[,1]
college = college[,-1]
#fix(college)
```

**c)**

i.

``` r
summary(college)
```

    ##  Private        Apps           Accept          Enroll       Top10perc    
    ##  No :212   Min.   :   81   Min.   :   72   Min.   :  35   Min.   : 1.00  
    ##  Yes:565   1st Qu.:  776   1st Qu.:  604   1st Qu.: 242   1st Qu.:15.00  
    ##            Median : 1558   Median : 1110   Median : 434   Median :23.00  
    ##            Mean   : 3002   Mean   : 2019   Mean   : 780   Mean   :27.56  
    ##            3rd Qu.: 3624   3rd Qu.: 2424   3rd Qu.: 902   3rd Qu.:35.00  
    ##            Max.   :48094   Max.   :26330   Max.   :6392   Max.   :96.00  
    ##    Top25perc      F.Undergrad     P.Undergrad         Outstate    
    ##  Min.   :  9.0   Min.   :  139   Min.   :    1.0   Min.   : 2340  
    ##  1st Qu.: 41.0   1st Qu.:  992   1st Qu.:   95.0   1st Qu.: 7320  
    ##  Median : 54.0   Median : 1707   Median :  353.0   Median : 9990  
    ##  Mean   : 55.8   Mean   : 3700   Mean   :  855.3   Mean   :10441  
    ##  3rd Qu.: 69.0   3rd Qu.: 4005   3rd Qu.:  967.0   3rd Qu.:12925  
    ##  Max.   :100.0   Max.   :31643   Max.   :21836.0   Max.   :21700  
    ##    Room.Board       Books           Personal         PhD        
    ##  Min.   :1780   Min.   :  96.0   Min.   : 250   Min.   :  8.00  
    ##  1st Qu.:3597   1st Qu.: 470.0   1st Qu.: 850   1st Qu.: 62.00  
    ##  Median :4200   Median : 500.0   Median :1200   Median : 75.00  
    ##  Mean   :4358   Mean   : 549.4   Mean   :1341   Mean   : 72.66  
    ##  3rd Qu.:5050   3rd Qu.: 600.0   3rd Qu.:1700   3rd Qu.: 85.00  
    ##  Max.   :8124   Max.   :2340.0   Max.   :6800   Max.   :103.00  
    ##     Terminal       S.F.Ratio      perc.alumni        Expend     
    ##  Min.   : 24.0   Min.   : 2.50   Min.   : 0.00   Min.   : 3186  
    ##  1st Qu.: 71.0   1st Qu.:11.50   1st Qu.:13.00   1st Qu.: 6751  
    ##  Median : 82.0   Median :13.60   Median :21.00   Median : 8377  
    ##  Mean   : 79.7   Mean   :14.09   Mean   :22.74   Mean   : 9660  
    ##  3rd Qu.: 92.0   3rd Qu.:16.50   3rd Qu.:31.00   3rd Qu.:10830  
    ##  Max.   :100.0   Max.   :39.80   Max.   :64.00   Max.   :56233  
    ##    Grad.Rate     
    ##  Min.   : 10.00  
    ##  1st Qu.: 53.00  
    ##  Median : 65.00  
    ##  Mean   : 65.46  
    ##  3rd Qu.: 78.00  
    ##  Max.   :118.00

ii.

``` r
pairs(college[, 1:10])
```

![](/isl-solutions/img/ch2/unnamed-chunk-5-1.png)

iii.

Remember that `plot()` produces boxplots when the x axis variable is categorical, as should be expected. If it's numerical it will produce scatterplots. Hence remember to order the arguments to the function appropriately.

``` r
attach(college)
plot(Private, Outstate, xlab="Private", ylab="Out-out-state")
```

![](/isl-solutions/img/ch2/unnamed-chunk-6-1.png)

iv.

We first make a vector of "No" for as many universities as there are in the dataset. We then set some elements of that vector to "Yes" when the corresponding university has greater than 50% of their own students coming from the top 10% of their respective high schools. We then simply add the data to the college dataset and view a summary of it.

``` r
Elite = rep("No", nrow(college))
Elite[college$Top10perc>50] = "Yes"
Elite = as.factor(Elite)
college = data.frame(college, Elite)
summary(college$Elite)
```

    ##  No Yes 
    ## 699  78

``` r
plot(Elite, Outstate, xlab="Elite", ylab="Out-of-state")
```

![](/isl-solutions/img/ch2/unnamed-chunk-8-1.png)

v.

``` r
par(mfrow=c(2,2))
attach(college)
```

    ## The following object is masked _by_ .GlobalEnv:
    ## 
    ##     Elite

    ## The following objects are masked from college (pos = 3):
    ## 
    ##     Accept, Apps, Books, Enroll, Expend, F.Undergrad, Grad.Rate,
    ##     Outstate, P.Undergrad, perc.alumni, Personal, PhD, Private,
    ##     Room.Board, S.F.Ratio, Terminal, Top10perc, Top25perc

``` r
hist(Apps, main="Histogram of Applications Received")
hist(perc.alumni, col="red", main="Histogram of Alumni Donation Rate")
hist(S.F.Ratio, col="purple", breaks=10, main="Histogram of Student/Faculty Ratio")
hist(Expend, breaks=100, main="Histogram of Expenditure per Student")
```

![](/isl-solutions/img/ch2/unnamed-chunk-9-1.png)

vi.