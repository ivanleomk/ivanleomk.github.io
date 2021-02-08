# Probability Distributions

# Discrete Distributions

## Bernoulli Trial

There are only two possible outcomes - success and failure.

$$
P(X) = (1-\theta) \text{  if x = 0 else }\theta
$$

## Binomial Distribution

When we have $n$ Bernoulli trials, we end up with a binomial distribution. Our random variable $X$ here represents the number of successes in these $n$ Bernoulli trials.

We therefore have a pdf defined as

$$
P(x=r) = {n \choose r} \theta^r (1-\theta)^{n-r}
$$

where $r$ represents the number of successes.

As $n$ tends to infinity, we find that our binomial distribution in turn tends to a normal distribution.

## Negative Binomial

$X$ here represents the number of bernoulli trials to be observed till a fixed number of successes is observed. $\theta$ here represents the probability of success. This gives us the pdf of

$$
P(X=r) = {r-1 \choose k-1} \theta^k(1-\theta)^{r-k}
$$

The intuition here is that the final trial alwaus involves the $k-th$ success. Therefore we permute the initial $r-1$ trials which involves $k-1$ successes.

The sum of independent negative binomials having the same value of $\theta$ is also interestingly negative binomial.

The expectaiton of this distribution is $\frac{k}{\theta}$ and the variance is $\frac{k(1-\theta)}{\theta^2}$

## Geometric

The geometric distribution is concerned with the number of trials till the first success. We therefore have a pdf of

$$
P(x=k) = (1-\theta)^{k-1}\theta
$$

The expectation of this distribution is $\frac{1}{\theta}$ and its variance is $\frac{1-\theta}{\theta^2}$

## Poisson

The poisson distribution measures the number of events observed in a fixed time period given a rate of occurence.

We have a probability density function of

$$
P(x=r) = \frac{\theta^re^{-\theta}}{r!}
$$

Interestingly, the mean and the variance of the poisson is its rate paramter. In this case, that is $\theta$

## Hypergeometric

The hypergeometric distribution shows the probability of obtaining $r$ succeses in a population of size $N$ when drawing a sample of size $n$. In this population, we have $R$ successes and $N-R$ failures.

We can calculate the probability of obtaining $r$ successes by taking

$$
p(x=r) =
\frac
{
    {R \choose r} {N-R \choose n-r}
}
{
    {N \choose n}
}
$$

# Continous Distributions

## Gamma

The gamma distribution measures the time until $k-th$ subsequent events occur. It has the density function of

$$
p(x;\lambda,\alpha) = \frac{\lambda^{\alpha}x^{\alpha}e^{-\lambda x}}{\Gamma(x)}
$$

The gamma is often used to model non-negative values and is simply the result of $k$ individual exponential distributions. Another way to think about this is that the exponential is a gamma distribution with a rate parameter $\lambda$ of 1.

It has an expected value of $\frac{\alpha}{\lambda}$ and a variance of $\frac{\alpha}{\lambda^2}$.

## Exponential

The exponential distribution measures the time till the first occurence of an event. Since $\Gamma(1) = 1$, we can rewrite our gamma function pdf to give us the pdf of the exponential distribution as

$$
P(x;\theta) = \theta e^{-\theta x}
$$

It has an expected value of $\frac{1}{\theta}$ and a variance of $\frac{1}{\theta^2}$

## Normal Distribution

The Normal distribution has the pdf of

$$
P(x;\mu , \sigma^2 ) = \frac{1}{\sigma\sqrt{2\pi}}exp(-\frac{(x-\mu)^2}{2\sigma^2})
$$

## Chi-Squared

The Chi-Squared distribution is defined as the squared-sum of $n$ samples drawn from a standard normal distribution. The degrees of freedom of a chi-squared distribution is equal to the number of samples involved.
