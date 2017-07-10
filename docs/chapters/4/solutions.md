---
layout: page
title:  "Chapter 4: Classification"
category: "solution"
chapter: 4
use-math: true
---

<h1 class="post-subtitle">Conceptual</h1>

### 1.

Let $A = e^{\beta_0 + \beta_1X}$ and $P = p(X)$.

$$
\begin{align*}
P &= \frac{A}{1+A} \\
P(1+A) &= A \\
P + PA &= A \\
&= A - PA \\
&= A(1 - P) \\
\therefore A &= \frac{P}{1 - P}
\end{align*}
$$

### 2.

$$
\begin{align*}
p_k(x) = \frac{\pi_k\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{1}{2\sigma^2}(x-\mu_k)^2)}{\sum \pi_l\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{1}{2\sigma^2}(x-\mu_l)^2)}
\end{align*}
$$

Observe that the denominator is a constant, it's not dependent on the index k in any way. Furthermore $\pi_l$, $\sigma$ and $\exp(z)$ are always $> 0$. Hence it's a positive constant which we'll denote as $c$ onwards.

$$
\begin{align*}
p_k(x) &= \frac{\pi_k\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{1}{2\sigma^2}(x-\mu_k)^2)}{c} \\
log(p_k(x)) &= log(\frac{\pi_k\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{1}{2\sigma^2}(x-\mu_k)^2)}{c}) \\
&= log(\pi_k\frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{1}{2\sigma^2}(x-\mu_k)^2)) - log(c) \\
&= log(\frac{\pi_k}{\sqrt{2\pi}\sigma}) - \frac{1}{2\sigma^2}(x-\mu_k)^2 - log(c) \\
&= log(\pi_k) - log(\sqrt{2\pi}\sigma) - \frac{x^2}{2\sigma^2} + \frac{\mu_kx}{\sigma^2} - \frac{\mu_k^2}{2\sigma^2} - log(c)
\end{align*}
$$

Now notice that there are two terms in this expression that are not reliant on k, $log(\sqrt{2\pi}\sigma)$ and $\frac{x^2}{2\sigma^2}$. These can then be deemed constants and easily lumped in with a new constant term we'll call $log(c')$, an important note to make is that $\sqrt{2\pi}\sigma$ and $\exp(\frac{x^2}{2\sigma^2})$ are both positive terms so $c'$ is still a strictly positive constant.

$$
\begin{align*}
log(p_k(x)) &= x\frac{\mu_k}{\sigma^2} - \frac{\mu_k^2}{2\sigma^2} + log(\pi_k) - log(c') \\
log(p_k(x)) + log(c') &= x\frac{\mu_k}{\sigma^2} - \frac{\mu_k^2}{2\sigma^2} + log(\pi_k) \\
log(c'p_k(x)) &= \delta_k(x)
\end{align*}
$$

Where $c'$ is strictly positive and the log function is monotonically increasing, hence maximising $\delta_k(x)$ maximises $p_k(x)$ as required.

### 3.

So this question is very wordy but really easy to answer given the proof we did in the previous question. Recall that we only eliminated the quadratic term $\frac{x^2}{2\sigma^2}$ because it had no reliance on k. But in the case of QDA the covariance matrix (which simplifies down to variance for a single predictor) is class specific, thus the terms will be $\frac{x^2}{2\sigma_k^2}$ and it cannot be eliminated as a constant. So the new discriminant will be a quadratic in terms of $x$.

### 4.

**a)**

10%, ignoring the edge cases at $X < 0.05$ and $ X > 0.95$.

**b)**

1%

**c)**

$0.1^{100}$

**d)**

We can see that when p is large and n is relatively small we're only using an extremely small subset of overall data to determine the classification of an observation. Or more accurately as in KNN a fixed amount of points are always used to determine classification, these points will not lie 'closely' to the observation and hence cause a poor fit.

**e)**

Shortcut, the side of the hypercube will always be equal to $s = 0.1^{1/p}$.

So assuming a fixed range of [0, 1] for each predictor and a uniform distribution means points are distributed evenly over the hypervolume. We want a hypervolume that corresponds to 10% of the total hypervolume of the cube which will always be 1, thus $V_{class} = S_{class}^p = 0.1$.

### 5.

**a)**

Expect QDA to perform better on the training data as it will overfit, expect LDA to perform better on the test data as it represents the underlying truth more accurately.

**b)**

Expect QDA to perform better on both.

**c)**

QDA performance will relatively improve with more observations, as is the general case for models with higher flexibility.

**d)**

False. QDA will model the noise present in the system given the extra quadratic term and thus have a higher test error rate.

### 6.

**a)**

$$
\begin{align*}
p(x) &= \frac{e^{\beta_0 + \beta_1x_1 + \beta_2x_2}}{1 + e^{\beta_0 + \beta_1x_1 + \beta_2x_2}} \\
&= \frac{0.61}{1 + 0.61} \\
&= 38\%
\end{align*}
$$

**b)**

$$
\begin{align*}
e^{\beta_0 + \beta_1x_1 + \beta_2x_2} &= \frac{p(x)}{1-p(x)} \\
&= \frac{0.5}{1-0.5} = 1 \\
\end{align*}
$$

Take the log of both sides.

$$\beta_0 + \beta_1x_1 + \beta_2x_2 = 0 \\$$

$$
\begin{align*}
x_1 &= \frac{-\beta_0 - \beta_2x_2}{\beta_1} \\
&= 50
\end{align*}
$$

### 7.

Let's use LDA.

$$
\pi_{no} = 0.2,~\pi_{yes} = 0.8,~\sigma = 6\\
f_{no}(4) = \frac{1}{6\sqrt{2\pi}}\exp(\frac{-1}{72}(4)^2) = 0.053\\
f_{yes}(4) = \frac{1}{6\sqrt{2\pi}}\exp(\frac{-1}{72}(-6)^2) = 0.040\\
$$

Then:

$$
\begin{align*}
p_{yes}(x) &= \frac{\pi_{yes}f_{yes}(x)}{\sum \pi_lf_l(x)} \\
&= \frac{0.8 \times 0.040}{(0.2 \times 0.053) + (0.8 \times 0.040)} \\
&= 0.75
\end{align*}
$$

### 8.

KNN (n=1) training error rate is always 0% by definition, which means the test error rate has to be 36% for the average to be 18%. Thus you should use logistic regression as it has a lower test error rate of 30%.

### 9.

**a)**

$$
\begin{align*}
p(x) &= \frac{e^{0.37}}{1+e^{0.37}} \\
&= 0.59
\end{align*}
$$

**b)**

$$
\begin{align*}
odds &= \frac{0.16}{1-0.16} \\
&= 0.19
\end{align*}
$$
