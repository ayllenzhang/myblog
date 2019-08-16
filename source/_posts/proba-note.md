---
title: Probability statistics notes
date: 2019-07-24 19:31:19
tags: [Probablistic, Math, Note]
categories: 科研 / Research
mathjax: true
---

Some notes I took down last summer, when I was reviewing *statistics* and *probability*.

<escape><!-- more --></escape>

## Basic Probability

### Bayes' Theorem
For two random events A, B
$$
P(B|A)=\frac{P(AB)}{P(A)}=\frac{P(AB)}{P(B)}\cdot\frac{P(B)}{P(A)}=\frac{P(B)}{P(A)}\cdot P(A|B)
$$
namely,
$$
P(B|A)P(A)=P(AB)=P(A|B)P(B)
$$

### Independent events
Events A and B are independent events if the occurrence of one of them does not affect the probability of the occurrence of the other. That is, two events are independent if either
$$
P(B|A)=P(B)
$$
or
$$
P(A|B)=P(A)
$$
Meanwhile, (A', B), (A, B'), (A', B') are also independent events if A, B are independent events.

### PMF, CDF and PDF
* __PMF__ means probability mass function. Suppose that $X: S → A (A \subseteq R$) is a discrete random variable defined on a sample space $S$. Then the probability mass function $f_X: A → [0, 1]$ for $X$ is defined as
  $$
  f_{X}(x)=\Pr(X=x)=P(\{s\in S:X(s)=x\})
  $$
  __Hyper geometric distribution__ is one of those common discrete distributions. If we randomly select n items without replacement from a set of N items of which:

  * m of the items are of type-1
  * and N − m of the items are of type-2

  then the PMF of X, the discrete variable defined as the number of selected type-1 items, is called hyper-geometric distribution, which is:
  $$
  P(X=x)=f(x)=\frac{\binom mx\binom {N\,-\,m}{n\,-\,x}}{\binom Nn}
  $$

* __CDF__, also called cumulative distribution function, is generally a function of a real-valued random variable $X$ given by
  $$
  F_{X}(x)=\operatorname {P} (X\leq x)
  $$
  The CDF of a continuous random variable $X$ can be expressed as the integral of its probability density function $f_X$ as follows:
  $$
  F_{X}(x)=\int _{-\infty }^{x}f_{X}(t)\,dt
  $$

* __PDF__, known as probability density function, is similar with __PMF__ while it's defined for continuous random variable. PDF is defined as follows.
  $$
  \Pr[a\leq X\leq b]=\int _{a}^{b}f_{X}(x)\,dx.
  $$
  Hence, if $F_X$ is the cumulative distribution function of continuous random variable $X$, then:
  $$
  F_{X}(x)=\int _{-\infty }^{x}f_{X}(u)\,du
  $$
  namely, if $f_X$ is continuous at $x$,
  $$
  f_{X}(x)={\frac {d}{dx}}F_{X}(x)
  $$
  __uniform distribution__ is a common continuous distribution, in which the continuous random variable X has average probability in $[a, b]$, denoted as $X\sim U(a, b)$. Its probability density function is 
  $$
  $$f(x)=\frac{1}{a-b}~~~(a\leq x\leq b)
  $$
  

## Expectation and variance

### Expectation

For discrete variable $X \in S$, expectation of $x$ is defined as:
$$
E(X)=\sum_{x\in S}{x\cdot p(X=x)}
$$
e.g. the expectation of hyper-geometric distribution can be calculated as follow:
$$
\begin{align}E(X)
&=\sum_{x\in S}x\cdot\frac{\binom mx\binom {N\,-\,m}{n\,-\,x}}{\binom Nn} \\
&=\sum_{x\in S}\frac{\frac{m!}{(x-1)!(m-x)!}\binom {N\,-\,m}{n\,-\,x}}{\binom Nn} \\
&=\sum_{x\in S}\frac{m\cdot\binom{m-1}{x-1}\binom {N\,-\,m}{n\,-\,x}}{\binom Nn} \\
&=\sum_{x\in S}\frac{m\cdot\binom{N-1}{n-1}}{\binom Nn} \\
&=\frac{mn}{N}
\end{align}
$$
For continuous variable $X\in \mathbb{R}$, expectation is defined as:
$$
{E} [X]=\int _{\mathbb {R} }xf(x)\,dx
$$
The expectation operator is linear in the sense that
$$
E(aX+bY)=aE(X)+bE(Y)
$$

### Variance
The variance of a random variable $X$ is the expected value of the squared deviation from the mean of $X$. Let  $\mu = E[X]$,
$$
\operatorname {Var}(X)=E\left[(X-\mu)^{2}\right]\
$$
Substitute with $\mu = E[x]$, we can have
$$
\begin{align}
\operatorname{Var}(X)&=E\left[(X-E[X])^{2}\right]\\
&=E\left[X^2-2XE[X]+E[X]^2\right]\\
&=E[X^2]-2E[X]E[X]+E[X]^2 \\
&=E[X^2]-E[X]^2
\end{align}
$$
The variance of a sum of random variables and constants is given by
$$
\operatorname {Var} (aX+bY+c)=a^{2}\operatorname {Var} (X)+b^{2}\operatorname {Var} (Y)+2ab\,\operatorname {Cov} (X,Y)
$$
where $\operatorname{Cov}(\cdot,\cdot)$ is the covariance.

### Covariance
The covariance between two jointly distributed real-valued random variables $X$ and $Y$ is defined and transformed as:
$$
\begin{align}
\operatorname{Cov}(X, Y)&=E[(X-E(X))(Y-E(Y)]\\
&=E[XY-XE(Y)-YE(X)+E(X)E(Y)]\\
&=E[XY]-E[X]E[Y]
\end{align}
$$
Note that $\operatorname{Var}(X) = \operatorname{Cov}(X, X)$. Meanwhile, for random variables X, Y in joint support S, suppose $f(x,y)$ is the joint probability density function defined on $(x,y)\in S$.

For X and Y are discrete random variables,
$$
\operatorname{Cov}(x,y)=\sum_{(x,y)\in S}(x-\mu_x)(y-\mu_y)f(x,y)
$$
and for X and Y are continuous random variables,
$$
\operatorname{Cov}(x,y)=\iint_{(x,y)\in S}(x-\mu_x)(y-\mu_y)f(x,y)dxdy
$$


### Correlation

The correlation is defined as:
$$
\rho_{xy}=\operatorname{Corr}(X,Y)=\frac{\operatorname{Cov}(X,Y)}{\sigma_x\sigma_y}=\frac{\sigma_{xy}}{\sigma_x\sigma_y}\in[-1,1]
$$
When $\operatorname{Corr}(X,Y)$ is close to $\pm 1$, a strong linear relationship between $X$ and $Y$ is indicated.

### Sample expectation and variance
Here we suppose $X_1$, $X_2$, $\dots$ , $X_n$ are observations of a random sample of size n. Then

* $\bar{X}=\frac{1}{n}\sum_{i=1}^{n}{X_i}$ is the sample mean of the n observations, and
* $S^2=\frac{1}{n-1}\sum_{i=1}^{n}{(X_i-\bar{X})^2}$ is the sample variance of the n observations

Proof: Here we assume the original expectation(mean) and variance of $X_i$ to be $\mu, \sigma^2$. Then we have:
$$
E(\bar{X})=E(\frac{1}{n}\sum_{i=1}^{n}{X_i})=\frac{1}{n}\sum_{i=1}^{n}{E(X_i)}=\frac{1}{n}\sum_{i=1}^{n}{\mu}=\mu
$$

$$
\begin{align}
E(S^2)&=E\left[\frac{1}{n-1}\sum_{i=1}^{n}{(X_i-\bar{X})^2}\right]\\
&=\frac{1}{n-1}\sum_{i=1}^{n}E\left(X_i-\frac{\sum_{j=1}^{n}X_j}{n}\right)^2\\
&=\frac{1}{n-1}\sum_{i}E\left[X_i^2-2\frac{X_i\sum_{j}X_j}{n}+\frac{(\sum_j{X_j})^2}{n^2}\right]\\
&=\frac{1}{n-1}\left\{\sum_i{E(X_i^2})-E\left[\frac{(\sum_i{X_i})^2}{n}\right]\right\}\\
&=\frac{1}{n-1}\left[\frac{n-1}{n}\sum_i{E(X_i^2)}-\frac{1}{n}\sum_{i,j\neq i}E(X_iX_j)\right]\\
\end{align}
$$

Notice that $X_1, X_2, ..., X_n$ are independent variables, which means $\forall i,j \in 1,\dots,n, Cov(X_i, X_j)=0$. Namely, $E(X_iX_j)=E(X_i)E(X_j)$. So we have
$$
\begin{align}
E(S^2)&=\frac{1}{n-1}\left[\frac{n-1}{n}\sum_i{E(X_i^2)}-\frac{1}{n}\sum_{i,j\neq i}E(X_i)E(X_j)\right]\\
&=\frac{1}{n-1}\cdot\frac{n-1}{n}\sum_i{\left[E(X_i^2)-E(X_i)^2\right]}\\
&=\frac{1}{n}\cdot n\operatorname{Var}(X_i)\\
&=\sigma^2
\end{align}
$$
It can be proved that $S^2$ and $\bar{X}$ are independent. In addition, if $X_1, X_2, \dots, X_n$ subject to normal distribution, then
$$
\frac{(n-1)S^2}{\sigma^2}=\frac{\sum_{i=1}^{n}{(X_i-\bar{X})^2}}{\sigma^2}\sim \chi^2(n-1)
$$

### Moment Generating Function
Consider the Taylor expansion form of exponential function $e^{tx}$ at $x=0$, which is
$$
e^{tx} = 1+tx+\frac{(tx)^2}{2!}+\frac{(tx)^3}{3!}+\cdots
$$
If we replace x with random variable X, and consider the expected value of both sides, the result will be
$$
E(e^{tX})=1+tE(X)++\frac{t^2E(X^2)}{2!}+\frac{t^3E(X^3)}{3!}+\cdots
$$
Here, we define the moment generating function of a continuous random variable X, if it exists, to be
$$
M(t)=E(e^{tX})=\int_{-\infty}^{+\infty}e^{tx}f(x)dx
$$
for $-h<x<h$. From the equations above, it's clearly that
$$
M^{(r)}{(0)}=E(X^r)+\sum_{i\geq 1} a_it^i
$$
Meanwhile, let $S$ be the set of possible values of $X$, then
$$
M(t)=E(e^{tX})=\sum_{x\in S}e^{tx}f(x)
$$
Therefore, the coefficient of $e^{tx}$ is the probability:
$$
f(x)=P(X=x)
$$


## Typical discrete distributions
### Binomial Distributions
$2$ results, $n$ samplings. Let $X$ to be the frequency of the result with probability $P$ to be selected in a single sampling. Then we say X subjects to binomial distribution, write as $X\sim B(n,p)$. And we have:
$$
\begin{align}
P(X=k)&={n \choose k}p^{k}(1-p)^{n-k}\\
E[X]&=np\\
\operatorname{Var}(X)&=np(1-p)
\end{align}
$$

### Poisson Distributions
A Poisson distribution tries to describe such a situation: an event can occur 0, 1, 2, … times in an interval. The average number of events in an interval is designated $\lambda$. Lambda is the event rate, also called the rate parameter. Let random variable $X$ to note the number of observed events in an interval. Then we have
$$
 P(X=k)=e^{-\lambda }{\frac {\lambda ^{k}}{k!}}
$$
The mean and variance for Poisson distribution are both $\lambda$. Besides, notice that $\sum_{i}\lambda^i/i!$ is the Taylor series of $e^x$ at $x_0=0, x=\lambda$. Therefore, we can say definitely that
$$
\sum_{k=0}^{+\infty}P(X=k)=1
$$
In fact, Poisson distribution could be derived from binomial distribution. Suppose $n\rightarrow +\infty$ while $np = const$. Let $np = \lambda$, then
$$
\begin{align}
P(X=k)&=\lim_{n\rightarrow +\infty}{n\choose k}p^k(1-p)^{n-k}\\
&=\lim_{n\rightarrow +\infty}\frac{n(n-1)\cdots(n-k+1)}{k!}\cdot\frac{\lambda^k}{n^k}(1-\frac{\lambda}{n})^{n-k}\\
&=e^{-\lambda}\lim_{n\rightarrow +\infty}(1-\frac{1}{n})(1-\frac{2}{n})\cdots(1-\frac{k-1}{n})\frac{\lambda^k}{k!}\\
&=e^{-\lambda}\frac{\lambda^k}{k!}
\end{align}
$$
With $n\geq 20, p\leq 0.05$, the Poisson distribution can be used to approximate the binomial distribution by setting $\lambda=np$.

## Typical continuous distributions
### Uniform Distributions
We have introduced this kind of distributions above, here are some other properties of it. For $a\leq x\leq b$, we have
$$
\begin{align}
F(x)&=\frac{x-a}{b-a}\\
\mu=E(X)&=\frac{a+b}{2}\\
\sigma^2=\operatorname{Var}(X)&=\frac{(b-a)^2}{12}
\end{align}
$$

### Exponential Distribution
The continuous random variable X follows an exponential distribution if its probability density function is:
$$
f(x)=\frac{1}{\theta}e^{-x/\theta}~~~(x\geq0,\theta>0)
$$
For $x\geq0,\theta>0$. Besides, 
$$
\begin{align}
F(x)&=-e^{-x/\theta}+1\\
\mu=E(X)&=\theta\\
\sigma^2=\operatorname{Var}(X)&=\theta^2
\end{align}
$$
Here's an derivation of exponential distribution. Suppose a random event $e$ happens randomly in $t\in [0,\infty)$, with an average frequency $\lambda$ to happen in an interval of length 1. This is to say that the number of $e$ in an interval follows Poisson distribution. Let $X$ note the distribution of the first appearance of $e$. Then we have
$$
\begin{align}
F(X=x)&=P(X\leq x)=1-P&(e~happens~0~time~in~[0,x])\\
&=1-e^{-\lambda x}\frac{(\lambda x)^0}{0!}~~~&\text{(from Poisson distribution)}\\
\Rightarrow f(x)&=F'(x)=\lambda e^{-\lambda x}
\end{align}
$$
Let $\theta = \frac{1}{\lambda}$, then
$$
f(x)=\frac{1}{\theta}e^{-x/\theta}
$$

### Gamma Distribution
#### _Derivation of Gamma Distribution_
Consider the derivation of exponential distribution. In the same way, we suppose a random event $e$ happens randomly in $t\in [0,\infty)$, with an average frequency $\lambda$ to happen in an interval of length 1. However, we let $X$ note the distribution of the $\alpha^{th}$ appearance of $e$. Then:
$$
\begin{align}
F(X=x)&=P(X\leq x)=1-\sum_{i=0}^{\alpha-1}P(e~happens~i~time~in~[0,x])\\
&=1-\sum_{i=0}^{\alpha-1}e^{-\lambda x}\frac{(\lambda x)^i}{i!}~~~~~\text{(from Poisson distribution)}\\
\Rightarrow f(x)&=F'(x)=\lambda e^{-\lambda x}\left\{1+\sum_{i=1}^{\alpha-1}\left[\frac{(\lambda x)^i}{i!}-\frac{(\lambda x)^{i-1}}{(i-1)!}\right]\right\}\\
&=\lambda^\alpha e^{-\lambda x}\cdot\frac{x^{\alpha-1}}{(\alpha-1)!}
\end{align}
$$
Let $\theta = \frac{1}{\lambda}$, then
$$
f(x)=\frac{1}{\theta^\alpha(\alpha-1)!}e^{-x/\theta}x^{\alpha-1}
$$
When $\alpha=1$, gamma distribution turns out to be exponential distribution. In the other hand, when $\theta=2$, $\alpha=r/2$, gamma distribution becomes Chi-square distribution.

The Gamma distribution has a mean of $\mu=\alpha\theta$ and a variance of $\sigma^2=\alpha\theta^2$.

#### _The Gamma Function_
The gamma function, denoted $\Gamma(t)$, is defined, for $t\geq 0$, by:
$$
\Gamma(t)=\int_0^\infty y^{t-1}e^{-y}dy
$$
Moreover,
$$
\Gamma(t)=\frac{y^t}{t}\cdot e^{-y}\,\bigg|_0^{\infty}-\int_0^\infty\frac{y^t}{t}\cdot(-e^{-y})dy=\frac{1}{t}\Gamma(t+1)
$$
therefore we have $\Gamma(t+1)=t\,\Gamma(t)$.

In addition, when $t=1$,
$$
\Gamma(t)=\int_0^\infty e^{-y}dy=-e^{-y}\,\bigg|_0^{\infty}=1
$$
In conclusion, for $n\in\mathbb{N}$,
$$
\Gamma(n)=(n-1)!
$$

#### _Chi-square Distribution_
Let $X$ follow a gamma distribution with $\theta=2$ and $\alpha=r/2$, where r is a positive integer. Then the probability density function of X will be:
$$
f(x)=\frac{1}{2^{r/2}\Gamma(\frac{r}{2})}e^{-x/2}x^{r/2-1}(x>0)
$$
Notice that the Gamma function is the analytic continuation of the factorial function. As $r/2$ can be non-integer while $r$ is an integer, we use the Gamma function here to replace the factorial function here.

The expectation of $\chi^2$-distribution is $\mu=r$, while the variance is $\sigma^2=2r$. $r$ is called degree of freedom in $\chi^2$-distribution.

In addition, we have
> **Theorem 1**. If $Z_1,\dots,Z_k\sim\mathcal{N}(0,1)$ are independent, then the sum of their squares,
> $$
> Q\ =\sum _{i=1}^{k}Z_{i}^{2}
> $$
> is distributed according to the chi-squared distribution with k degrees of freedom.
>
> **Theorem 2**.  Let $X_i$ denote $n$ independent random variables that follow these chi-square distributions, e.g., $X_1\sim\chi^2(r_1)$, $X_2\sim\chi^2(r_2)$, etc. Then, the sum of the random variables
> $$
> Y=X_1+X_2+\cdots+X_n
> $$
> follows a chi-square distribution with $r_1+r_2+\dots+r_n$ degrees of freedom. That is:
> $$
> Y\sim\chi^2(r_1+r_2+\dots+r_n)
> $$

While this can be proved with [MGF](https://newonlinecourses.science.psu.edu/stat414/node/72/), we're not going to introduce the proof here. Just take it as a conclusion.

### An interesting story of Beta/Dirichlet distribution

See [here](https://cosx.org/2013/01/lda-math-beta-dirichlet).

### Normal Distribution (or Gaussian Distribution)
The probability density function of $\mathcal{N}(\mu, \sigma)$ is
$$
{\displaystyle f(x)=\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}}
$$
We can know from the last chapter (_Basic knowledge in calculus_) that
$$
\int_{-\infty}^{\infty}{\frac{1}{\sqrt{2\pi\sigma^2}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}dx} = 1
$$
In addition, we have
> **Theorem**.  Let $X_i$ denote $n$ independent random variables that follow these normal distributions.
> e.g., $X_1\sim\mathcal{N}(\mu_1,\sigma_1^2)$, $X_2\sim\mathcal{N}(\mu_2,\sigma_2^2)$, etc. Then, the linear combination
> $$
> Y=c_1X_1+c_2X_2+\cdots+c_nX_n
> $$
> follows the normal distribution:
> $$
> Y\sim\mathcal{N}(\sum_{i=1}^nc_i\mu_i,\sum_{i=1}^nc_i^2\sigma_i^2)
> $$
> 

#### _Z Scores_
It can be proved that, for $X\sim \mathcal{N}(0,1)$,
$$
Z=\frac{x-\mu}{\sigma}\sim \mathcal{N}(0,1)
$$
This formula is also the defination of Z score.

#### _Relationship of Normal Distribution and $\chi^2$ Distribution_
> **Theorem**.  If $X$ is normally distributed with mean $\mu$ and variance $\sigma^2\geq 0$, then:
> $$
> V=\left(\frac{X-\mu}{\sigma}\right)^2=Z^2
> $$
> is distributed as a chi-square random variable with 1 degree of freedom.

Proof:
Namely it's to prove that
$$
P(Z^2=v)=P(V=v)=g(v)=\frac{1}{\Gamma(1/2)2^{1/2}}e^{-v/2}v^{-1/2}
$$
Meanwhile,
$$
\begin{align}
G(v)=P(Z^2\leq v)&=P(-\sqrt{v}\leq Z\leq\sqrt{v})\\
&=\int_{-\sqrt v}^{\sqrt v}\frac{1}{\sqrt{2\pi}}e^{-x^2/2}dx\\
&=2\int_0^{\sqrt v}\frac{1}{\sqrt{2\pi}}e^{-x^2/2}dx\\
&=\int_0^{v}\frac{1}{\sqrt{2\pi}}z^{-1/2}e^{-z/2}dz\\
\Rightarrow g(v)&=\frac{dG(v)}{dv}=\frac{d\left(\int_0^{v}\frac{1}{\sqrt{2\pi}}z^{-1/2}e^{-z/2}dz\right)}{dv}\\
&=\frac{1}{\sqrt{2\pi}}v^{-1/2}e^{-v/2}
\end{align}
$$
Also,
$$
\begin{align}
\Gamma(1/2)&=\int_0^\infty y^{-1/2}e^{-y}dy\\
&=\int_0^\infty 2e^{-u^2}du\\
&=\int_{-\infty}^\infty e^{-u^2}du=\sqrt{\pi}
\end{align}
$$
Therefore,
$$
g(v)=\frac{1}{\Gamma(1/2)2^{1/2}}e^{-v/2}v^{-1/2}
$$
Our proof is complete. Moreover, we have
$$
\frac{(n-1)S^2}{\sigma^2}=\frac{\sum_{i=1}^{n}(X_i-\bar{X})^2}{\sigma^2}\sim\chi^2(n-1)
$$


## Central limit theorem
### Definition
Let $X_1, X_2, \dots, X_n$ be a random sample from any distribution with (finite) mean $\mu$ and (finite) variance $\sigma^2$. If the sample size $n$ is sufficiently large, then:

- the sample mean $\bar{X}$ follows an approximate normal distribution
- with mean $E(\bar{X})=\mu$ and variance $Var(\bar{X})=\frac{\sigma^2}{n}$


## Statistical Hypothesis Test
### About _Null Hypothesis_
The null hypothesis is a general statement or default position that there is no relationship between two measured phenomena, or no association among groups. Testing (trying to accept or reject) the null hypothesis — and thus concluding that there is or is not a relationship between two phenomena— is a central task in the modern practice of science.

Null Hypothesis is often denoted as $H_0$, while the hypothesis being tested against it, also called the alternative hypothesis, is often denoted as $H_1$. $p$ is generally used for denoting the probability of $H_0$, namely, the probability of there's no real difference.

### Student's t-Test
The t-test is any statistical hypothesis test in which the test statistic follows a Student's t-distribution under the null hypothesis. It was introduced in 1908 by William Sealy Gosset under his pen name "Student".

> __t-distribution__ 
> Definition. If $Z\sim\mathcal{N}(0,1)$ and $U\sim\chi^2(r)$ are independent, then the random variable:
> $$
> T=\frac{Z}{\sqrt{U/r}}
> $$
> follows a t-distribution with $r$ degrees of freedom.  We write $T\sim t(r)$. The p.d.f. of $T$ is:
> $$
> \frac{\Gamma \left(\frac{\nu+1}{2} \right)} {\sqrt{\nu\pi}\,\Gamma \left(\frac{\nu}{2} \right)} \left(1+\frac{x^2}{\nu} \right)^{-\frac{\nu+1}{2}}\!
> $$
> It's clear that, for $X_1,X_2,\dots,X_n\sim\mathcal{N}(\mu,\sigma^2)$, 
> $$
> \frac{\bar{X}-\mu}{\sigma/\sqrt{n}}\sim\mathcal{N}(0,1)
> $$
> And now we have:
> $$
> \frac{\bar{X}-\mu}{s/\sqrt{n}}\sim t(n-1)
> $$
> where $s$ is the sample standard deviation.

Most test statistics have the form $t=Z/S$, where $Z$ and $S$ are functions of the data.

- $Z$ may be sensitive to the alternative hypothesis (i.e., its magnitude tends to be larger when the alternative hypothesis is true)
- $S$ is a scaling parameter that allows the distribution of t to be determined.
- $S^2$ should follow a $\chi^2$ distribution with $p$ degrees of freedom under the null hypothesis, where $p$ is a positive constant

#### _One-sample t-test_
Let $Z=\bar{X}-\mu,\,S=s/\sqrt{n}$, then
$$
{\displaystyle t={\frac {\bar{x}-\mu_{0}}{s/\sqrt {n}}}}
$$
Note that
$$
S^2=\frac{s^2}{n}=\sum_{i=1}^n\frac{(X_i-\bar{X})^2}{n(n-1)}
$$


#### _Two-sample t-test_

|           When to do this test           |                             $S$                              |                      Degree of Freedom                       |
| :--------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|  Small sample, $\sigma_1^2=\sigma_2^2$   | ${\displaystyle \sqrt{s^2_{pool}\left(\frac{1}{n_1}+\frac{1}{n_2}\right)}}$ |                         $n_1+n_2-2$                          |
| Small sample, $\sigma_1^2\neq\sigma_2^2$ | ${\displaystyle \sqrt{\frac{s^2_1}{n_1}+\frac{s^2_2}{n_2}}}$ | ${\displaystyle \left.{\left({\frac {s_{1}^{2}}{n_{1}}}+{\frac {s_{2}^{2}}{n_{2}}}\right)^{2}}\middle/\left(\frac {\left(s_{1}^{2}~/~n_{1}\right)^{2}}{n_{1}-1}+\frac {\left(s_{2}^{2}~/~n_{2}\right)^{2}}{n_{2}-1}\right)\right.}$ |


### Z-Test
A Z-test is any statistical test for which the distribution of the test statistic under the null hypothesis can be approximated by a normal distribution. Because of the central limit theorem, many test statistics are approximately normally distributed for large samples. 

#### _Relationship with Student's t-Test_
For each significance level, the Z-test has a single critical value which makes it more convenient than the Student's t-test which has separate critical values for each sample size. Statistical tests with large sample size or known population variance can be conveniently performed as approximate Z-tests. If the population variance is unknown (and therefore has to be estimated from the sample itself) and the sample size is not large (n < 30), the Student's t-test may be more appropriate.

### Pearson's chi-squared test
Pearson's chi-squared test is used to assess three types of comparison: 

* goodness of fit
* homogeneity
* independence

It tests a null hypothesis stating that:

> The frequency distribution of certain events observed in a sample is consistent with a particular theoretical distribution.

The events considered must be mutually exclusive and have total probability 1.

#### _Testing for statistical independence_
For a contingency table with $r$ rows and $c$ columns, the value of the test-statistic is

$$
\chi ^{2}=\sum_{i=1}^{r}\sum_{j=1}^{c}{(O_{i,j}-E_{i,j})^{2}\over E_{i,j}}
$$
in which $O_{i,j},E_{i,j}$ notes the observation and expectation in each cell, and the number of degrees of freedom $DF=(r-1)(c-1)$.

#### _Yates' Correction for Continuity_
The approximation to the chi-squared distribution breaks down if expected frequencies are too low.

* Normally the approximation is acceptable when no more than 20% of the events have expected frequencies below 5.
* Where $DF=1$, the approximation is acceptable when expected frequencies are no less than 10.

In this case, a better approximation can be obtained by reducing the absolute value of each difference between observed and expected frequencies by 0.5 before squaring; this is called Yates's correction for continuity.

### ANOVA
ANOVA, an abbreviation of _Analysis of Variance_, is a collection of statistical models and their associated estimation procedures used to analyze the differences among group means in a sample.

In ANOVA, we generally make the following assumptions:

- Independence of observations – this is an assumption of the model that simplifies the statistical analysis.
- Normality – the distributions of the residuals are normal.
- Equality (or "homogeneity") of variances, called homoscedasticity — the variance of data in groups should be the same.

#### _One-way ANOVA_
Suppose we did a research about personal annual income in several major cities, and here's the survey result:

|  Cities   |           Samples            |
| :-------: | :--------------------------: |
|  Beijing  | $X_{11},X_{12},X_{13},\dots$ |
| Shanghai  | $X_{21},X_{22},X_{23},\dots$ |
| Guangzhou | $X_{31},X_{32},X_{33},\dots$ |

Cities are called affect factor here. Now we want to know if there is a relationship between people's annual income and cities. For each group, assume the data obey a normal distribution $\mathcal{N}(\mu_i, \sigma^2)$, then the null hypothesis can be:
$$H_0:\mu_1=\cdots=\mu_g$$
in which $g$ is the number of groups.
Here we consider three statistics, which is:

- The total sum of squares, namely the variance: $$S_T^2=\sum_{i=1}^{g}\sum_{j=1}^{n_i}(X_{ij}-\bar{X})^2$$
- The intragroup sum of squares, introduced by affect factors: $$S_A^2=\sum_{i=1}^{g}n_i(\bar{X_i}-\bar{X})^2$$
- The intergroup sum of squares, introduced by stochastic error: $$S_E^2=\sum_{i=1}^{g}\sum_{j=1}^{n_i}(X_{ij}-\bar{X_i})^2$$

We can easily prove that:
$$
S_T^2=S_A^2+S_E^2
$$
When $H_0$ is true, we have:
$$
S_A\sim\chi^2(g-1),S_E\sim\chi^2(n-g)
$$
Define $F$ as the ratio of the between group variance and the within group variance, namely, 
$$
F=\frac{S_A/(g-1)}{S_E/(n-g)}\sim F(g-1,n-g)
$$
$F(g-1,n-g)$ here means the F-distribution.

> __Definition of F-distribution__
> A random variate of the F-distribution with parameters d1 and d2 arises as the ratio of two scaled chi-squared variates:
> $$
> X=\frac{U_1/d_1}{U_2/d_2}
> $$
> where:
>
> - U1 and U2 have chi-squared distributions with d1 and d2 degrees of freedom respectively, and
> - U1 and U2 are independent.

Therefore, under a given significance level $\alpha$, the rejection region is
$$
K_0={F>F_{1-\alpha}(g-1,n-g)}
$$

## Basic knowledge in calculus
Some basic knowledge should be introduced ahead of normal distribution, as they can be helpful to understand the distribution function of normal distribution.
### Jacobi Matrix
$$\mathbf {J} = {\begin{bmatrix}{
\dfrac{\partial \mathbf {f} }{\partial x_{1}}} &
\cdots &
{\dfrac {\partial \mathbf {f} }{\partial x_{n}}}\end{bmatrix}}={\begin{bmatrix}
{\dfrac {\partial f_{1}}{\partial x_{1}}} & \cdots & {\dfrac {\partial f_{1}}{\partial x_{n}}} \\
\vdots &\ddots &\vdots \\
{\dfrac {\partial f_{m}}{\partial x_{1}}} & \cdots & {\dfrac {\partial f_{m}}{\partial x_{n}}}
\end{bmatrix}}$$

### Integration by substitution
Let $x = \varphi(u)$, then we have
$$
\begin{align}
\int_{\varphi(a)}^{\varphi(b)}{f(x)}\,dx &= \int_{\varphi(u)=\varphi(a)}^{\varphi(b)}{f(\varphi(u))}\,d\varphi(u)\\
&=\int_a^b{f(\varphi(u))\varphi'(u)\,du}
\end{align}
$$
Further, let $(x, y) = (x(a, b), y(a, b))$, then
$$
\iint_{(x,y)\in C} f(x, y)\,dx\,dy = \iint_{(x(a,b),y(a,b))\in C}{f(x(a,b), y(a,b))\big|\mathbf{J}\big|\,da\,db}
$$
in which $\mathbf{J} = {\begin{bmatrix}
{\dfrac {\partial x}{\partial a}}&
{\dfrac {\partial x}{\partial b}}\\
{\dfrac {\partial y}{\partial a}}&
{\dfrac {\partial y}{\partial b}}
\end{bmatrix}}$ is the **Jacobi** matrix in the instance. $\big|\mathbf{J}\big|$ means the determinant of the matrix.

In particular, when replacing Cartesian coordinate system by polar coordinate system, we have
$$
\begin{cases}
	x = rcos{\theta}\\
	y = rsin{\theta}
\end{cases}
$$
therefore,
$$
\mathbf{J}=\dfrac{\partial (x,y)}{\partial (r, \theta)}={\begin{bmatrix}
cos{\theta}&-rsin{\theta}\<span class=""></span>\
sin{\theta}&rcos{\theta}
\end{bmatrix}} \Rightarrow|\mathbf{J}| = r
$$


### Integration by parts
If $u = u(x)$ and $du = u'(x)dx$, while $v = v(x)$ and $dv = v'(x)dx$, then integration by parts states that:
$$
\begin{aligned}
\int _{a}^{b}u(x)v'(x)\,dx&=[u(x)v(x)]_{a}^{b}-\int _{a}^{b}u'(x)v(x)dx\\
&=u(b)v(b)-u(a)v(a)-\int _{a}^{b}u'(x)v(x)\,dx
\end{aligned}
$$
or, more compactly,
$$
\int u\,dv=uv-\int v\,du.\!
$$


### Kronecker's delta

$$
\delta_{i,j} = \begin{cases}
	1 & \text{if}~~i = j\\
	0 & \text{otherwise}
\end{cases}
$$

### Intergrability of $x^ne^{-x^2/2}$
#### _Hermite Polynomial_
For each n, define the Hermite polynomial $H_n(x)$ by
$$
\frac{d^n}{dx^n}e^{-x^2/2}=(-1)^nH_n(x)e^{-x^2/2}
$$
For example,
$$
H_0(x) = 1\\
\frac{d}{dx}e^{-x^2/2}=-xe^{-x^2/2}\Rightarrow H_1(x)=x\\
\frac{d^2}{dx^2}e^{-x^2/2}=-e^{-x^2/2}+x^2e^{-x^2/2}\Rightarrow H_2(x)=x^2-1\\
\frac{d^3}{dx^3}e^{-x^2/2}=xe^{-x^2/2}+2xe^{-x^2/2}-x^3e^{-x^2/2}\Rightarrow H_1(x)=x^3-3x
$$

It's obvios that $\int H_{n+1}{(x)}\,e^{-x^2/2}=-H_{n}{(x)}\,e^{-x^2/2}+C$, assume that
$$
x^n=a_nH_n+a_{n-1}H_{n-1}+\cdots+a_0H_0
$$
Because $H_k(x)e^{-x^2/2}$ is integrable for $k \geq 1$, the integrability of $x^ne^{-x^2/2}$ then depends on the value of $a_0$.

In linear algebra, ${H_0, H_1, H_2, \cdots}$ form an orthogonal basis, and it has been proved that
$$
\int_{-\infty}^{\infty} H_i(x)H_j(x)\,e^{-x^2}dx=\sqrt{2\pi}\,n!\,\delta(i, j)
$$
Here
$$
a_0=\frac{\left<x^n, H_0\right>}{\left<H_0, H_0\right>}=\frac{1}{\sqrt{2\pi}}\int_{-\infty}^{\infty}x^ne^{-x^2/2}dx~~\begin{cases}>0&n~is~even\\
=0&n~is~odd\end{cases}
$$
So we can say that

* If n is odd, $x^ne^{-x^2/2}$ is intergrable
* Otherwise, if n is even, $x^ne^{-x^2/2}$ is not intergrable

### Calculation of $\int_{-\infty}^{\infty} e^{-x^2}dx$
Though $H_0e^{-x^2}$ is not intergrable, we can calculate the result of $\int_{-\infty}^{\infty} e^{-x^2}dx$. Suppose the result to be $I$. then
$$
\begin{split}
I \times I &= \int_{-\infty}^{\infty}{e^{-x^2}\,dx} \times \int_{-\infty}^{\infty}{e^{-y^2}\,dy} \\
 &= \int_{y=-\infty}^{\infty}\int_{x=-\infty}^{\infty}{e^{-(x^2+y^2)}\,dx\,dy}\\
 &= \int_{\theta=-\pi}^{\pi}\int_{r=0}^{\infty}re^{-r^2}\,dr\,d\theta \\
 &= \int_{\theta=-\pi}^{\pi}\left(-\frac{1}{2}e^{-r^2}\right)\bigg|_{r=0}^{\infty}\,d\theta \\
 &= \int_{\theta=-\pi}^{\pi}{-\frac{1}{2}}\,d\theta \\
 &= \pi
\end{split}
$$
Apparently $I > 0$. Therefore, we have $I = \sqrt{\pi}$

### Calculation of $\int_{-\infty}^{\infty}{x^{2k}e^{-x^2}dx}$
Here we can use integration by parts.

$$
\begin{align}
\int_{-\infty}^{\infty}{x^{2k}e^{-x^2}dx}
&= -\frac{1}{2}\int_{-\infty}^{\infty}{x^{2k-1}\cdot\left(-2xe^{-x^2}\right)dx}\\
&= -\frac{1}{2}\left(x^{2k-1}e^{-x^2}\bigg|_{-\infty}^{\infty}-\int_{-\infty}^{\infty}(2k-1)x^{2k-2}e^{-x^2}dx\right)\\
&= \frac{2k-1}{2}\int_{-\infty}^{\infty}{x^{2k-2}e^{-x^2}dx}\\
&= \frac{(2k-1)!!}{2^k}\int_{-\infty}^{\infty} e^{-x^2}dx \\
&= \frac{(2k-1)!!}{2^k}\sqrt{\pi}
\end{align}
$$
Moreover,
$$
{\displaystyle \int_{-\infty}^{\infty}{x^{2k}e^{-\frac{(x-a)^2}{2b^2}}dx}=(2k-1)!!\sqrt{2\pi b^{2k}}}
$$
