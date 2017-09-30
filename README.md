---
title: "Statistical Inference Part1"
author: "Veronica Vaca"
date: "29 de septiembre de 2017"
output:
  word_document: default
  pdf_document: default
---

## Overview

In this project we are going to investigate the exponential distribution in R and compare it with the Central Limit Theorem. 


```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Simulations

The exponential distribution can be simulated in R with rexp(n, lambda) where lambda is the rate parameter. The mean of exponential distribution is 1/lambda and the standard deviation is also 1/lambda. Set lambda = 0.2 for all of the simulations. You will investigate the distribution of averages of 40 exponentials.

### Show the sample mean and compare it to the theoretical mean of the distribution.

```{r }
# set seed for reproducability
set.seed(31)

# set lambda to 0.2
lambda <- 0.2

# 40 samples
n <- 40

# 1000 simulations
simulations <- 1000

# simulate
simulated_exponentials <- replicate(simulations, rexp(n, lambda))

# calculate mean of exponentials
means_exponentials <- apply(simulated_exponentials, 2, mean)

# distrribution mean
analytical_mean <- mean(means_exponentials)
analytical_mean

# analytical mean
theory_mean <- 1/lambda
theory_mean

```

```{r , echo=FALSE}
# visualization
hist(means_exponentials, xlab = "mean", main = "Exponential Function Simulations")
abline(v = analytical_mean, col = "green")
abline(v = theory_mean, col = "blue")
```
The center of distribution of averages of 40 exponentials is very close to the theoretical center of the distribution.


## Show how variable the sample is and compare it to the theoretical variance of the distribution.

You can also embed plots, for example:


```{r }
# standard deviation of distribution
standard_deviation_dist <- sd(means_exponentials)
standard_deviation_dist

# standard deviation from analytical expression
standard_deviation_theory <- (1/lambda)/sqrt(n)
standard_deviation_theory

# variance of distribution
variance_dist <- standard_deviation_dist^2
variance_dist

# variance from analytical expression
variance_theory <- ((1/lambda)*(1/sqrt(n)))^2
variance_theory

```
The Theoretical variance is 0.625. The actual variance of the distribution is 0.6291041. The distribution is approximately a normal as it is shown in the next plot.

```{r , echo=FALSE}
# visualization
xfit <- seq(min(means_exponentials), max(means_exponentials), length=100)
yfit <- dnorm(xfit, mean=1/lambda, sd=(1/lambda/sqrt(n)))
hist(means_exponentials,breaks=n,prob=T,col="green",xlab = "means",main="Density of means",ylab="density")
lines(xfit, yfit, pch=22, col="blue", lty=5)
```

Aditional we compare the distribution of averages of 40 exponentials to a normal distribution

```{r , echo=FALSE}
qqnorm(means_exponentials)
qqline(means_exponentials, col = 2)

```

The central limit theorem (CLT), says that the distribution of averages of n exponentials is very close to a normal distribution as we have seen.




