
---
title: A Rough Guide to Stochastic Calculus for Option Pricing
description: Presenting the main ideas, with derivations removed.
pubDate: 2026-09-24
draft: false
tags:
  - maths
  - finance
---

# 1. Brownian Motion and Diffusion Process

We present Brownian Motion as the limit of scaled random walk. 

Consider an infinite coin tossing space $(\Omega, \mathcal{F}, \mathbb{P}),$ where $\Omega=\{ \omega_{1}\omega_{2}\dots \}$. The initial position of a traveller is $M(0) = 0.$ For each coin toss $\omega_{i}$, if it is head, the traveller moves forward by 1 unit, otherwise, he moves backward by 1 unit. We find the Random Walk $M(t)$ as his position st time t. 

There are 2 mental models to understand this. First, we look "across" $\Omega$.  Imagine conducting one experiment, which produces a coin tossing result $\omega$ known to us. This leads to a fixed $W(t)$ path along $t$. A different coin tossing result leads to a different path $M(t)$. This mental models say: we take an infinite coin toss first, which produces a fixed path, which the traveller is stuck on, among infinite possible paths he may travel. Second interpretation is to "decide-as-it-goes". At time 1, we flip a coin first, which tell us where to go, then at time 2, we flip a coin again, and so on. In this interpretation, $M(t)$ is a random variable depending on outcomes $\omega_{1}\dots\omega_{t}$ up to time $t$. $M(t)$ is a discrete time stochastic process. 

As an analogy, imagine you are navigating from 1 place to another. The first model says: your navigator shows many possible routes, you pick one random route and travel according to it. The second model says: at each cross-road, you use a coin-flip to decide whether go left or right. 

The Scaled Random Walk is:
$$
W^{n}(t) = \frac{1}{\sqrt{ n }} M_{nt}.
$$
Once $M(t)$ is determined, $W^n(t)$ is determined. Thus, $W^n(t)$ can also understood in the previous sense. Now, every $\frac{1}{n}$ unit time, the total distance travelled is $\frac{1}{\sqrt{ n }}$. During each $\frac{1}{n}$ unit time, we travel at a constant speed, thus, for $t$ such that $nt$ not an integer, we use interpolation. 

We take $n \to \infty$ for the scaled random walk, the limit is a Brownian Motion $W(t)$. The precise requirements of a Brownian Motion are:
(a) $W(0)=0$ for all $\omega$;
(b) For non-overlapping increments of time $t_{1}<t_{2}\leq t_{3}<t_{4}$, $W(t_{4})-W(t_{3})$ is independent of $W(t_{2})-W(t_{1})$;
(c) $W(t)-W(s) \sim N(0, t-s)$ for any $t>s$. 

We use Brownian Motion to define the diffusion process (also understood in the mental models described):
$$
X(t+\Delta t) - X(t)=\mu(t, X_{t})\Delta t+\sigma(t, X_{t})\Delta W(t).
$$
At time $t$, the instant change of $X$ is decided by:
(a) a velocity $\mu$ depending on time and location;
(b) a volatility $\sigma$ that scales newly added noise $\Delta W_{t}$.

Fix a certain $\omega$ decided path, we can divide by $\Delta t$ on both sides, and get:
$$
\frac{d}{dt}X(t) = \mu(t, X(t)) + \sigma(t, X_{t}) \frac{d}{dt} W(t).
$$
Now $X(t)$ and $W(t)$ are just fixed curves on a plot. If $W(t)$ is differentiable, we can directly solve for $X(t)$ by integrating the terms, and aligning the starting position $X(0)$. But, unfortunately, $W(t)$ is not differentiable because it looks like a "spike" everywhere, which we know is not differentiable from a simple example $f(x)=|x|$. 

Rewrite the diffusion process as:
$$dX(t)=\mu(t, X(t))dt + \sigma(t, X(t))dW(t),$$
we want to be able to integrate:
$$
X(t) = X(0) + \int_{0}^{t}\mu(s, X(s))ds + \int_{0}^{t}\sigma(s, X(s))dW(s). 
$$
The middle term on right hand side is ordinary calculus. We want to find the last term. 

# 2. Ito's Integral

Imagine a simple case, where inside any gap of time partition $0=t_{0}<t_{1}<\dots<t_{n}=t,$ the process $g(t)$ is a constant. Then the integral can be defined as $\int_{0}^{t} g(s)dW(s)=\sum_{i=0}^{n-1}g(t_{i})(W(t_{i+1}-W(t_{i}))).$ Imagine that $g(t)$ is the share of stocks we hold. $W(t)$ reflects the price of a stock. The summation is the total payoff we make from the investment strategy $g$. If $g$ is not simple, use simple ones to approximate it, and then take the limit. 

We treated the case where we take integral w.r.t to a Brownian Motion. We also want to take integral w.r.t a diffusion process. To find $\int_{0}^{t} g(s)dX(s)$, replace $dX(s)$ by the equation:
$$dX(t)=\mu(t, X(t))dt + \sigma(t, X(t))dW(t),$$
and it reduces to adding an ordinary integral with an Ito's Integral.

# 3. Ito-Doeblin's Formula
Imagine that $X(t)$ is the portfolio value at time $t$. We are interested in the discounted value $f(t, X(t))=e^{-rt}X(t)$. How does the discounted value progress through time? More generally, if we have a transformation of $X(t)$ by $f(t, X(t))$, how does this transformed process progress according to time?

The Ito-Doeblin's Formula says: if needed derivatives of $f$ are well-defined and continuous, then:
$$
\begin{aligned}
df(t,X_t)
&=\left(
\frac{\partial f}{\partial t}(t,X_t)
+\mu(t,X_t)\frac{\partial f}{\partial x}(t,X_t)
+\frac12\sigma^2(t,X_t)\frac{\partial^2 f}{\partial x^2}(t,X_t)
\right)dt \\
&\qquad
+\sigma(t,X_t)\frac{\partial f}{\partial x}(t,X_t)\,dW_t.
\end{aligned}
$$
Notice that $f(t, X_{t})$ is still a diffusion progress, whose progression is transformed by derivatives of $f$.

Compare this to the ordinary calculus, where we have non-random $f(\cdot)$ and $g(\cdot)$. Then, the transformed "progression" have derivation $\frac{d}{dx}f(g(x))=f'(g(x))g'(x)$. 

# 4. Stock, Wealth, and Their Discounts

Consider a stock, or an underlying asset our option is pegged to, that moves in the following diffusion process:
$$
dS(t) = \alpha S(t)dt + \sigma S(t)dW(t).
$$
An investor holds $\Delta(t)$ shares of stock at time $t$. The total money he put into the stock at time $t$ is $\Delta(t)S(t)$, and the remaining $X(t)-\Delta(t)S(t)$ are put in the money market. His wealth will progress as:
$$
dX(t) = \Delta(t)dS(t) + r(X(t)-\Delta(t)S(t))dt.
$$
$\Delta(t)dS(t)$ is just $\Delta(t)(S(t+dt)-S(t)),$ the growth in stock price times our position. For continuous interest rate, over any time, we have $M(t+\Delta t)=M(t)e^{r{\Delta t}}$, where $M(t)$ is amount in money market. Thus, 
$$
\frac{{M(t+\Delta t)-M(t)}}{\Delta t} = M(t)\lim_{ \Delta t \to 0 }  \frac{e^{r \Delta t}-1}{\Delta t} = M(t)\lim_{ \Delta t \to 0 } \frac{re^{r\Delta t}-0}{1}=rM(t).
$$
Thus, the instantaneous contribution from money market is $rM(t)dt$. 

We can substitute $dS(t)$ specified into the about progression of $X(t),$ and get:
$$
dX(t) = rX(t)dt + (\alpha-r)\Delta(t)S(t)dt + \sigma\Delta(t)S(t)dW(t),
$$
which includes 3 driving forces for progression in $X(t):$ (1) the safe interest rate; (2) the risk premium over the holding of risky asset; (3) the noise amplified by $\sigma$ over our risky asset.

We are interested in discounted values. Take $f(t, x) = e^{-rt}x$, using Ito-Doeblin's Formula, we can get:
$$d(e^{-rt}S(t)) = e^{-rt}(\alpha - r)S(t) dt + e^{-rt}\sigma S(t) dW(t)$$
and 
$$
d(e^{-rt}X(t)) = \Delta(t)d(e^{-rt}S(t)).
$$
We see a very nice connection between the discounted value. The progression in wealth is just out position times the progression in discounted stock value. 

# 5. Options

The value of an option should depend on time $t$ and the price of underlying stock. Suppose $c(t,x)$ is the price of an option when time is $t$, stock price is $x$. We just need to find this deterministic function and then substitute $x$ with $S(t)$, then we get the actual option value. 

Ito-Doeblin's formula suggests:
$$
dc(t, S(t)) = \left[ c_t(t, S(t)) + \alpha S(t) c_x(t, S(t)) + \frac{1}{2} \sigma^2 S^2(t) c_{xx}(t, S(t)) \right] dt
+ \sigma S(t) c_x(t, S(t)) \, dW(t). 
$$
Use Ito-Doeblin's formula again for the discounted option value:
$$

d(e^{-rt}c(t, S(t)))= e^{-rt} \left[ -rc(t, S(t)) + c_t(t, S(t)) + \alpha S(t)c_x(t, S(t)) + \frac{1}{2}\sigma^2 S^2(t)c_{xx}(t, S(t)) \right] dt + e^{-rt}\sigma S(t)c_x(t, S(t))dW(t). 
$$

# 6. Hedging 
To find $c(t,x)$, consider shorting a unit of European Call Option. The goal is to create a portfolio, such that at each time $t \in[0,T]$, $X(t)=c(t, S(t)).$ Equivalently, we want the discounted wealth to equate the discounted options value. It seems unnecessary, because we can already equate $X$ and $c$ directly by using there progression. But if one works through the tedious algebra, he realises that by using discounted price, the drift $\alpha$ is eliminated, thus making the task ahead easier.

To make sure equality holds everywhere, we make sure at each time $t \in[0,T)$ before expiration, they evolve at the same pace beginning from a common start:
$$
d(e^{-rt}c(t, S(t))) = d(e^{-rt}X(t)), \text{ for all } t \in[0,T),
$$
$$
c(0,S(0)) = X(0).
$$
after some tedious algebra, we settle down on a goal to solve for 
$$
c_t(t, x) + rxc_x(t, x) + \frac{1}{2}\sigma^2 x^2 c_{xx}(t, x) = rc(t, x) \quad \text{for all } t \in [0, T), \ x \geq 0
$$
with terminal condition:
$$
c(T, x) = (x -K)^+.
$$
# 7. Solution

To solve this form of PDE, we need boundary conditions when $x=0$ and $x=\infty$. 

If $x=0,$ just ignore all the maths for now. The intuition is: if the underlying asset you are pegged to is worth nothing, why should the option worth anything at all? We should have $c(t,0) = 0$.

If $x \to \infty$, at any time $t,$ the holder should definitely exercise the option, since the chance for the stock price to suddenly drop of $\infty$ to $K$ is so low. Thus, our option is essentially the same as a forward contract guaranteeing a strike price of $K$ at $T$. This means:
$$
\lim_{ x \to \infty } [c(t, x) - (x - Ke^{r(T-t)})]=0.
$$

The final solution is:
$$
c(t, x) = xN(d_+(T - t, x)) - Ke^{-r(T-t)}N(d_-(T - t, x)), \quad 0 \leq t < T, \ x > 0,
$$
where
$$
\\
d_{\pm}(\tau, x) = \frac{1}{\sigma\sqrt{\tau}} \left[ \log \frac{x}{K} + \left( r \pm \frac{\sigma^2}{2} \right) \tau \right], 
$$
$$

N(y) = \frac{1}{\sqrt{2\pi}} \int_{-\infty}^{y} e^{-\frac{z^2}{2}} dz = \frac{1}{\sqrt{2\pi}} \int_{-y}^{\infty} e^{-\frac{z^2}{2}} dz. 

$$




