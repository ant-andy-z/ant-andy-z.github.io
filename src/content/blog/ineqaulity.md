---
title: Discourse on Inequalities
description: Some useful inequality tools in probability theory
pubDate: 2026-10-27
draft: false
pinned: false
tags:
  - math
  - probability
---
We present some useful inequalities in probability theory. The following notations are used. 

| Notation                     | Meaning                                                                                                               |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| $X$                          | A random variable $X$                                                                                                 |
| $\mathbb{E}\left[ X \right]$ | The expectation of random variable $X$                                                                                |
| $\|X\|_{p}$                  | The $p^{th}$ norm of a random variable $X$, which is defined as $\left(\mathbb{E}\left[ \|X\|^p \right]\right)^{1/p}$ |
# Tail Probability
> **Proposition 1: (*markov*)**
> Let $X$ be an integrable random variable. For any $\epsilon>0,$ we have:
> $$\mathbb{P}\left[ |X| > \epsilon \right] \leq \frac{\mathbb{E}\left[ |X| \right]}{\epsilon}.$$

**Proof**
$$
\begin{align*}
\mathbb{P}\left[ |X| > \epsilon \right] &= \mathbb{E}\left[ \mathbb{1}_{|X|>\epsilon} \right] \\
&= \int_{\Omega}\mathbb{1}_{|X|>\epsilon} \,d\mathbb{P}(\omega) \\
&\leq \frac{1}{\epsilon} \int_{\Omega} \epsilon\mathbb{1}_{|X|>\epsilon} \,d\mathbb{P}(\omega) \\
&\leq \frac{1}{\epsilon} \int_{\Omega} |X| \,d\mathbb{P}(\omega) = \frac{\mathbb{E}\left[ |X| \right]}{\epsilon}. \\
\end{align*}
$$
The last inequality holds because:\
(1) for any $\omega,$ if $|X|(\omega)>\epsilon,$ then $\epsilon \mathbb{1}_{|X|>\epsilon}(\omega) = \epsilon < |X|(\omega);$\
(2) for any $\omega$, if $|X|(\omega)\leq \epsilon,$ then $\epsilon \mathbb{1}_{|X|>\epsilon}(\omega) = 0 \leq |X|(\omega).$
Thus, for any $\omega \in \Omega,$ $\epsilon \mathbb{1}_{|X|>\epsilon}(\omega) \leq |X|(\omega).$ Use monotonicity of integration. 
$\square$

A direct consequence is Chebyshev's Inequality:
> **Corollary** (***chebyshev***)
> Let $X$ be a square-integrable random variable. Then:
> $$\mathbb{P}\left( |X - \mathbb{E}\left[ X \right]|> \epsilon \right) \leq \frac{\mathrm{Var}\left( X \right)}{\epsilon^2}.$$

**Proof**
Square both sides and apply Proposition 1 to $(X-\mathbb{E}[X])^2$:
$$
\begin{align*}
\mathbb{P}\left(|X - \mathbb{E}\left[ X \right]|> \epsilon  \right) &= \mathbb{P}(|X - \mathbb{E}\left[ X \right]|^2> \epsilon^2)\\
&\leq \frac{\mathbb{E}\left[ |X - \mathbb{E}\left[ X \right]|^2 \right]}{\epsilon^2} = \frac{\mathrm{Var}\left( X \right)}{\epsilon^2}.
\end{align*}
$$
$\square$

# Convexity 

> **Proposition 2: (*jensen*)**
> Let $u:\mathbb{R} \to \mathbb{R}$, be a convex function. Suppose $X$ and $u(X)$ are both integrable, then:
> $$ \mathbb{E}\left[ u(X) \right] \geq u(\mathbb{E}\left[ X \right]).$$

**Proof**

We present a proof from Shreve. If $u$ is a convex function, then for any $x,$ $$u(x)=\sup\{\ell(x): \ell(s) \text{ is a linear function } \leq u\}.$$
Then, 
$$
\begin{align*}
\mathbb{E}\left[ u(X) \right] & \geq \mathbb{E}\left[ \ell(X) \right] \\
&= \ell(\mathbb{E}\left[ X \right]) , \text{ for any } \ell \text{ satisfying } \ell\leq u.
\end{align*}
$$
Take the supremum on both sides. We have
$$
 \mathbb{E}\left[ u(X) \right] \geq \sup\{\ell(\mathbb{E}\left[ X \right]): \ell \text{ satisfies } \ell\leq u\}
 = u(\mathbb{E}\left[ X \right]).
$$

$\square$

$\underline{Remark}:$ An immediate consequence is $\mathrm{Var}\left( X \right) = \mathbb{E}\left[ X^2 \right] - \mathbb{E}\left[ X \right]^2 \geq 0,$ due to convexity of $u(x)=x^2$. If one struggles to remember which side is bigger in the original statement, this is a simple example.

$\underline{Remark}:$ Let $u(x)=|x|,$ then $\mathbb{E}\left[ |X| \right]\geq |\mathbb{E}\left[ X \right]|$. 

# Powers and Norms

## Power and Product 

**Proposition 3: (*holder, with two dots on o*)**
> Let $p, q >1,$ such that $\frac{1}{p} + \frac{1}{q} =1$. Let $X, Y$ be random variables such that $\mathbb{E}\left[ |X|^p \right], \mathbb{E}\left[ |Y|^q \right] < \infty$. Then:
> $$\|XY\|_{1} \leq \|X\|_{p}\|Y\|_{q}.$$

**Proof**

If $\|X\|_{p}=0,$ then $\mathbb{E}\left[ |X|^p \right] = 0$. This means $X=0$ almost surely. To see this, use **Proposition 1**:
$$
\mathbb{P}\left[ |X|^p>0 \right] = \mathbb{P}\left( \bigcup_{n = 1}^{\infty} \{ |X|^p> 1/n \} \right) \leq \sum_{n=1}^{\infty}\mathbb{P}\left[|X|^p> \frac{1}{n}\right].
$$
For each $n \in \mathbb{N}$, 
$$
\mathbb{P}\left[|X|^p> \frac{1}{n}\right] \leq \frac{\mathbb{E}\left[ |X|^p \right]}{{\frac{1}{n}}} = 0.
$$
Thus, $\mathbb{P}\left[ |X|^p>0 \right]\leq 0.$ We have $\mathbb{P}\left[ |X|^p>0 \right]=0.$ Since $|X|^p$ is a non-negative random variable, this must mean $|X|^p =0$ almost surely. We know $|X|^p(\omega) = 0 \Leftrightarrow |X|(\omega)=0$ for any $\omega,$ we also know $|X|=0$ almost surely.  
Notice that $\{ \omega:|X|(\omega)=0 \} \subseteq \{ \omega:|XY|(\omega)=0 \}$. By monotonicity of measure, $\mathbb{P}\left[ |X|=0 \right]=1 \leq \mathbb{P}\left[ |XY|=0 \right]$. Since probabilities are at most $1$, $\mathbb{P}\left[ |XY|=0 \right]=1$, so $|XY|=0$ almost surely. Thus $\|XY\|_{1}=0 = \|X\|_{p}\|Y\|_{q}$.

If $\|Y\|_{q}=0,$ we can make the same claim. 

Now, suppose $\|X\|_{p} \neq 0, \|Y\|_{q} \neq 0.$ For any $a, b > 0,$ we can find $s, t,$ such that:
$$
a = \exp\left( \frac{1}{p}s \right), b = \exp\left( \frac{1}{q}t \right).
$$
By convexity of exponential function, 
$$
ab = \exp\left( \frac{1}{p}s + \frac{1}{q}t \right) \leq \frac{1}{p}\exp(s) + \frac{1}{q}\exp(t).
$$
This is:
$$
ab \leq \frac{1}{p}a^p + \frac{1}{q}b^q, \text{ for any }a >0 \text{ and }b>0.
$$
Note that this inequality still holds if $a = 0$ or $b =0$.
Let $a = \frac{|X|}{\|X\|_{p}}\text{ and } b = \frac{|Y|}{\|Y\|_{q}}$, then for any $\omega$:
$$
\frac{|XY(\omega)|}{\|X\|_{p}\|Y\|_{q}} \leq \frac{1}{p}\frac{|X|^p(\omega)}{\|X\|_{p}^p} + \frac{1}{q} \frac{|Y|^q(\omega)}{\|Y\|_{q}^q}
$$
(made possible since $\|X\|_{p} \neq 0, \|Y\|_{q} \neq 0$).
Take expectation on both sides, then by monotonicity of integration:
$$
\mathbb{E}\left[ \frac{|XY|}{\|X\|_{p}\|Y\|_{q}} \right] \leq \frac{1}{p}\mathbb{E}\left[ \frac{|X|^p}{\|X\|_{p}^p}  \right]+ \frac{1}{q}  \mathbb{E}\left[ \frac{|Y|^q}{\|Y\|_{q}^q} \right]=1
$$
(because $\|X\|_{p} = (\mathbb{E}\left[ |X|^p \right])^{1/p},$ is a constant; same for $Y$). 

Then: 
$$\|XY\|_{1} \leq \|X\|_{p}\|Y\|_{q}$$
(because $\|X\|_{p}, \|Y\|_{q}$ are constants.)

$\square$

$\underline{Remark}:$ The intermediate result $ab \leq \frac{1}{p}a^p + \frac{1}{q}b^q, \text{ for any }a >0 \text{ and }b>0$ is called Young's Inequality. 

## Power and Sum
> **Proposition 4: (*minkowski*)**
> Assume $p\geq1$, $X, Y$ are random variables such that $\mathbb{E}\left[ |X|^p \right], \mathbb{E}\left[ |Y|^p \right] < \infty$. Then: $\mathbb{E}\left[ |X+Y|^p \right] < \infty$ and 
> $$\|X+Y\|_{p}\leq\|X\|_{p}+\|Y\|_{p}.$$

**Proof**
We need to check $\mathbb{E}\left[ |X+Y|^p \right] < \infty$ first. For $a,b\geq 0$ and $p\geq 1$, the function $f(x)=x^p$ is convex. Thus:
$$
\begin{align*}
&f\left( \frac{{a+b}}{2} \right) \leq \frac{{f(a)+f(b)}}{2}\\
\implies & \frac{1}{2^p}(a+b)^p \leq \frac{1}{2}(a^p + b ^p)\implies (a+b)^p\leq 2^{p-1}(a^p+b^p).

\end{align*}
$$
Now, for any $\omega$, applying this with $a=|X|(\omega)$ and $b=|Y|(\omega)$ gives:
$$
|X+Y|^p \leq 2^{p-1}(|X|^p+|Y|^p).
$$
By linearity and monotonicity of integration, we have $\mathbb{E}\left[ |X+Y|^p \right]< \infty.$

Next, we show the inequality.

If $p=1,$ then the inequality is just triangle inequality. 

For $p>1$, consider: 
$$
|X+Y|^p = |X+Y||X+Y|^{p-1} \leq |X||X+Y|^{p-1}+|Y||X+Y|^{p-1}.
$$
Now, suppose $\frac{1}{p}+\frac{1}{q}=1$ for some $q >1$. We can write $p-1=\frac{p}{q}.$ Using Holder's, we get:
$$
\begin{align*}
\mathbb{E}\left[ |X||X+Y|^{p-1} \right] &\leq \|X\|_{p}( \||X+Y|^{p/q}\|_{q})\\
&\leq \|X\|_{p} \left( \mathbb{E}\left[  (|X+Y|^{p/q})^q\right]^{1/q} \right)\\
&\leq \|X\|_{p} \left( \mathbb{E}\left[  (|X+Y|^{p})\right]^{1/q} \right)\\
&\leq \|X\|_{p} \left( (\mathbb{E}\left[  (|X+Y|^{p})\right]^{1/p})^{p/q}\right)\\
&\leq \|X\|_{p} \|X+Y\|_{p}^{p-1}.
\end{align*}
$$
Similarly, we have
$$
\mathbb{E}\left[ |Y||X+Y|^{p-1} \right] \leq \|Y\|_{p} \|X+Y\|_{p}^{p-1}.
$$
Now, we have:
$$
\begin{align*}
\mathbb{E}\left[ |X+Y|^p \right]= \|X+Y\|_{p}^p &\leq  \|X\|_{p} \|X+Y\|_{p}^{p-1}  +  \|Y\|_{p} \|X+Y\|_{p}^{p-1} \\
&\leq \left(\|X\|_{p}+\|Y\|_{p}\right) \|X+Y\|_{p}^{p-1}.
\end{align*}
$$
If $\|X+Y\|_{p}=0$, the result is immediate. Otherwise, divide both sides by $\|X+Y\|_{p}^{p-1}$ to obtain:
$$\|X+Y\|_{p}\leq\|X\|_{p}+\|Y\|_{p}.$$


$\square$

$\underline{Remark}:$ Notice that the main difficulty of the proof is that the power in $|X+Y|^p$ is not desirable. When $p=1$, triangular inequality automatically creates a sum. This is the idea in our first step. 

$\underline{Remark}:$ Holder's gives a natural connection between $\mathbb{E}\left[ |X||X+Y|^{p-1} \right]$ and $\|X\|_{p}$. In fact, Holder's can be quite powerful. Because we can pick any $p$ and find an inequality involving $\|X\|_{p}$. We just need to keep track of the complementary term $\|\cdot\|_{q}$. 
