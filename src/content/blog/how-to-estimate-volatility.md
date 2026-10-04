---
title: How to Estimate Volatility
description: Estimating volatility for a stock 
pubDate: 2026-10-04
draft: false
tags:
  - maths
  - finance
---

The Black-Scholes-Merton formula requires an input of volatility. We want to know how to estimate this value. 

## From Diffusion to Geometric Brownian Motion
We assumed the movement of stock prices follows:
$$
dS(t) = \alpha S(t)dt + \sigma S(t)dW(t). 
$$

Divide $S(t)$ on both sides, we get:
$$
\frac{dS(t)}{S(t)} = \alpha dt + \sigma dW(t).
$$
The left hand side reminds us of $d(\log S(t)).$ However, notice that in Stochastic Calculus, taking differentiation of a stochastic process reaquires Ito-Doeblin's formula, not just chain rule. We consider $f(t, x) = \log x$, then $f_{t}(t, x) = 0,$ $f_{x}(t, x)= \frac{1}{x},$ $f_{x x} (t, x) = -\frac{1}{x^2},$ thus:
$$
\begin{align}
d(\log S(t)) &= 0\cdot dt + \frac{1}{S(t)}dS(t) + \frac{1}{2}\left( -\frac{1}{S(t)^2} \right)dS(t)dS(t) \\ 
& = \frac{1}{S(t)}dS(t) +\frac{1}{2}\left( -\frac{1}{S(t)^2} \right)\sigma^2S(t)^2dW(t)dW(t)) \\
&=\frac{dS(t)}{S(t)} -\frac{1}{2}\sigma^2dt.
\end{align}
$$
Take integral, and we get:
$$
\log S(t) = \log S(0) + \int_{0}^{t} \alpha ds+\int_{0}^{t} \sigma dW(s) - \int_{0}^{t} \frac{1}{2}\sigma^2ds.
$$
The stochastic integral is 
$$
\int_{0}^{t} \sigma dW(s) = \sigma \cdot \left( \sum_{i=0}^{n-1}W(t_{i+1})-W(t_{i}) \right) = \sigma W(t),
$$
by telescoping sum. 
Thus, we have:

$$
\log S(t) = \log S(0) + \alpha t + \sigma W(t) - \frac{1}{2}\sigma^2t.
$$
Then, this gives us the Geometric Brownian Motion that $S(t)$ follows:
$$
S(t) = S(0)\exp\left\{ \left( \alpha - \frac{1}{2}\sigma^2 \right)t + \sigma W(t) \right\}.
$$
## From Geometric Brownian Motion to Volatility

Between any 2 time points $t_{j}, t_{j+1}$ inside a time period $[T_{1}, T_{2}]$, we have:
$$
\log \frac{S(t_{j+1})}{S(t_{j})} = \left( \alpha-\frac{1}{2}\sigma^2 \right)(t_{j+1}-t{j})+ \sigma(W(t_{j+1})-W(t_{j})).
$$
Suppose we take the summation of all time intervals:
$$
\begin{align}
\sum_{j =0}^{m-1}\left( \log \frac{S(t_{j+1})}{S(t_{j})} \right)^2 &= \sigma^2\sum_{}^{}(W(t_{j+1})-W(t_{j}))^2 + \left( \alpha-\frac{1}{2}\sigma^2 \right)^2 \sum_{}^{}(t_{j+1}-t{j})^2 + \sigma(2\alpha-\sigma^2)\sum_{}^{}(t_{j+1}-t_{j})(W(t_{j+1})-W(t_{j})) \\
&= \sigma^2dW(t)dW(t) + \left( \alpha-\frac{1}{2}\sigma^2 \right)^2 dtdt +\sigma(2\alpha-\sigma^2)dtdW(t) \\
&= \sigma^2dt = \sigma^2(T_{2}-T_{1}). 
\end{align}

$$
We have the volatility estimate:
$$
\sigma^2 \approx \frac{1}{(T_{2}-T_{1})}\sum_{j =0}^{m-1}\left( \log \frac{S(t_{j+1})}{S(t_{j})} \right)^2.
$$
