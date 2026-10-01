---
title: Changing Measure to Make Non-standard Normal Distribution Standard Normal
description: Helps one understand the construction of changing measures
pubDate: 2026-10-01
draft: false
tags:
  - maths
  - probability
---


On Volume II of Shreve's *Stochastic Calculus for Finance*, he presented the following question:
Let $X \sim N(0,1)$ and let $Y = X + \theta.$ We want to change the measure from $\mathbb{P}\left( \cdot \right)$ to $\tilde{\mathbb{P}}(\cdot)$, such that $Y$ follows a standard normal under $\tilde{\mathbb{P}}(\cdot)$. Shreve presented a Radon-Nikodym derivative 
$$
Z(\omega) = \exp\left\{ -\theta X(\omega) - \frac{\theta^2}{2} \right\},
$$
but this construction was given without any justifications. I try to show why this constructions works. 

The goal is to make $\tilde{\mathbb{P}}(Y\leq b)$ a C.D.F of a standard normal variable. We already know that $X$ is distributed as a standard normal variable. We can use that directly:
$$
\tilde{\mathbb{P}}(Y\leq b) = \mathbb{P}\left( X\leq b \right).
$$

Since the Radon-Nikodym derivative have the nice property that connects expectations under different measures:
$$
\tilde{\mathbb{E}}[X]=E[XZ],
$$
it is natural to think that we need to turn the probability equation into an equation of expectations:
$$
\tilde{\mathbb{E}}[\mathbb{1}_{X+\theta\leq b}]=E[\mathbb{1}_{X\leq b}],
$$
where the left hand side can be transformed using Radon-Nikodym derivative:

$$
\tilde{\mathbb{E}}[\mathbb{1}_{X+\theta\leq b}] =\mathbb{E}[Z \cdot \mathbb{1}_{X+\theta\leq b}] =\mathbb{E}[\mathbb{1}_{X\leq b}].
$$
Now, our goal is to find $Z$ such that $\mathbb{E}[Z \cdot \mathbb{1}_{X+\theta\leq b}] =\mathbb{E}[\mathbb{1}_{X\leq b}]$ holds.

It is easier to write things out in the integral form:

$$
\frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b-\theta}Z e^{-x^2/2} dx = \frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b} e^{-x^2/2} dx.
$$
Let $x'=x-\theta,$ then transform the integration on the right hand side:

$$
\begin{align*}
\frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b} e^{-x^2/2} dx &= \frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b-\theta} e^{-(x'+\theta)^2/2} dx'\\
&= \frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b-\theta} e^{-x'^2/2}e^{-\theta x'+1/2\theta^2} dx'.
\end{align*}
$$

Equating, we get:
$$
\frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b-\theta}Z e^{-x^2/2} dx = \frac{1}{\sqrt{ 2\pi } }\int_{-\infty}^{b-\theta} e^{-x'^2/2}e^{-\theta x'-1/2\theta^2} dx'.
$$
Thus, $Z = e^{-\theta X-1/2\theta^2}$ to match the terms. (Note that integrating to $x$ and $x'$ is just a matter of notation. We can just treat $x'$ as $x$ in the last step and find $Z$.)

By definition we can let:
$$
\tilde{\mathbb{P}}(A) = \int_{A}Z(\omega)d\mathbb{P}(\omega).
$$
The verification of this probability measure is given in the textbook, thus we won't discuss it here.



