---
title: Put Call Parity
description: How to price an European put option with forward and call option
pubDate: 2026-10-04
draft: false
tags:
  - maths
  - finance
---

A forward contract obliges its holder to pay $K$ for the underlying stock at maturity time $T$. Unlike an European option, its holder can not decide not to do so. At time $t,$ with stock price $x$, what is the price of a forward contract $f(t, x)$? 

Consider a *static-hedge* strategy. I am selling a forward contract with strike price $K$ and maturity time $T$. At time $0$, I should receive $f(0,S(0))$ amount of money. This income should be used to buy 1 share of stock, because we must sell the stock to the contract holder at time $T$. We need $S(0)$ dollars to buy 1 share of stock. However, we don't need exactly $S(0)$ at time 0. $S(0) - e^{-rT}K$ would suffice. We can borrow $e^{-rT}K$ dollars at time 0, to afford 1 share of stock at $S(0)$. The borrowed sum can be repaid at time $T$ by the income of $K$ dollars guaranteed by the forward contract. We have:
$$
f(t, x) = x - e^{-r(T-t)}K.
$$
Now, if we want to decide on a proper strike price $K$, what should we pick? If we'd like to be profitable, we can estimate $S(T)$ and make $K$ larger than it. However, this comes with a risk of loss, due to $S(T)>K$. At time $t$, we can guarantee a completely safe $K$. Take $K = xe^{r(T-t)}$, we make $f(t,x) = 0.$ Notice that such $K$ can be found based on current knowledge. This is the *forward price* of a forward contract. We write:
$$
\text{For}(t,x) = xe^{r(T-t)}.
$$
At time $0$, suppose we set $K = S(0)e^{rT}$. At time $0$, we have a forward worth $0$ dollars. However, at $t$ proceeds, the value of the forward contract changes. 
$$
f(t, S(t)) = S(t) - e^{-r(T-t)}K = S(t) - e^{-r(T-t)}S(0)e^{rT}= S(t)-S(0)e^{rt}.
$$
This is the progression of the value of forward contract. 

At time $T$, if we hold 1 piece of forward contract, notice that the payoff from forward contract is exactly the payoff of a European call option minus that of a put option:
$$
x - K = (x - K)^+ - (K - x)^-.
$$
Thus, 
$$
f(T, S(T)) = c(T, S(T)) - p(T, S(T)).
$$

Suppose at time $t\leq T$, the equality does not hold. Let's say 
$$
f(t, S(t)) > c(t, S(t)) - p(t, S(t)).
$$
Then, at time $t$, we can short 1 piece of forward contract and a put option (borrow and then sell them), then long 1 piece of call option (use the money gained from shorting to buy), which gives us a net profit of $f(t, S(t))+ p(t, S(t)) - c(t, S(t))>0 .$ At time $T$, we need to repay the worth of forward + put option, which is $f(T, S(T)) + p(T, S(T))$. This can be paid by selling our call option that is worth $c(T, S(T)) = f(T, S(T))  + p(T, S(T))$. Notice that we have arbitrage at time $t$.

The previous argument requires 
$$
f(t, S(t)) = c(t, S(t)) - p(t, S(t)), \text{ for all } 0\leq t \leq T.
$$
Since we already have $c(t, S(t))$ by Black-Scholes-Merton formula, and $f(t, S(t)) = S(t)-S(0)e^{rt}$, we can write the value of a put option as:
$$
p(t, S(t)) = c(t, S(t)) - f(t, S(t)),
$$
by plugging in formulas. 
