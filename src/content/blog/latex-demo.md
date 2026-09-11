---
title: Rendering LaTeX with KaTeX
description: Inline math, a display equation, and a short derivation to prove the pipeline.
pubDate: 2026-09-12
tags:
  - math
  - latex
---

Markdown posts on this site run through `remark-math` and `rehype-katex`, so ordinary `$…$` and `$$…$$` delimiters work.

Inline: the Gaussian density is $p(x) = (2\pi\sigma^2)^{-1/2}\exp\bigl(-(x-\mu)^2/(2\sigma^2)\bigr)$.

A display equation — the Euler–Lagrange condition for $L(q,\dot q,t)$:

$$
\frac{d}{dt}\frac{\partial L}{\partial \dot q} = \frac{\partial L}{\partial q}.
$$

A short derivation. Start from the quadratic $f(x) = ax^2 + bx + c$ with $a \neq 0$. Completing the square:

$$
\begin{aligned}
f(x)
&= a\left(x^2 + \frac{b}{a}x\right) + c \\
&= a\left(x + \frac{b}{2a}\right)^2 - \frac{b^2}{4a} + c.
\end{aligned}
$$

The vertex is therefore at $x = -b/(2a)$, and the discriminant $b^2 - 4ac$ is the usual $4a$ times that constant term with a sign flip.
