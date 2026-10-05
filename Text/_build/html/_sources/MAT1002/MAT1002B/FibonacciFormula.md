# The Fibonacci Sequence --- Application of Partial Fractions

## Problem Statement

If $f(x) = \frac{1}{1-x-x^2}$, then

- $f(0.1)= 1.\:1\:2\:3\:5\:9\ldots$
- $f(0.01) = 1.\:01\:02\:03\:05\:08\:13\:21\:34\:55\:9\ldots$
- $f(0.001) = 1.\:001\:002\:003\:005\:008\:013\:021\:034\:055\:089\:144\:233\:377\:610\:988\ldots$

These correspond to the Fibonacci Sequence $1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, \ldots$.

We will find out why this is true, and then find a formula for the $n$th Fibonacci number.

### Essential knowledge

1. Factoring a quadratic polynomial.
2. Expansion of $\frac{K}{1-r}$ as the infinite sum

$$
\frac{K}{1-rx} = K + Krx + Kr^2x^2 + \cdots
$$

3. Partial fractions to convert $\frac{ax+b}{x^2+cx+d}$ into $\frac{A}{x-r_1} + \frac{B}{x-r_2}$ and find $A$ and $B$

4. Ability to reindex a sum:  $\sum_{n=0}^\infty T_{n+1} = \sum_{n=1}^\infty T_n$

## The method
Consider the Fibonacci Sequence:

\begin{align*}
F_0 &=1\\
F_1 &= 1\\
F_2 &= 2\\
F_3 &= 3\\
F_4 &=5\\
\vdots & \quad \vdots\\
F_{n+1} &= F_{n-1}+F_{n-2}\\
\vdots & \quad \vdots
\end{align*}

We have found a formula for $F_n$ previously through matrix algebra and eigenvectors.  Here we will use partial fractions to create an entirely different method to derive the same formula.



### Generating Function
```{prf:definition} Generating Function
Given a sequence of numbers $c_0, c_1, \ldots$, the corresponding **Generating Function** $f(x)$ is the power series whose coefficients are $c_i$:

$$
f(x) = c_0 + c_1 x + c_2 x^2 + \cdots
$$
```

We will define the generating function $f(x)$ for the Fibonacci numbers as the infinite sum:

$$
f(x) = F_0 + F_1 x^1 + F_2 x^2 + F_3 x^3 + \cdots  = \sum_{n=0}^\infty F_n x^n
$$

Our starting point is to find a closed form for $f(x)$.  Notice that

\begin{align*}
f(x) &= \sum_{n=0}^\infty F_n x^n\\
    &= F_0 + F_1 x^1 + \sum_{n=2}^\infty F_n x^n\\
    &= F_0 + F_1 x^1 + \sum_{n=2}^\infty (F_{n-2}+F_{n-1}) x^n\\
    &= F_0 + F_1 x^1 + \sum_{n=2}^\infty F_{n-2}x^n + \sum_{n=2}^\infty F_{n-1} x^n\\
    &= F_0 + F_1 x^1 + x^2\sum_{n=2}^\infty F_{n-2}x^{n-2} + x\sum_{n=2}^\infty F_{n-1} x^n\\
    &= F_0 + F_1x^1 + x^2 \sum_{n=0}^\infty F_n x^n + x \sum_{n=1}^\infty F_n x^n\\
    &= F_0 + F_1x^1 + x^2 f(x) + x (f(x)-F_0)\\
    &= 1 + x -x + (x^2+x) f(x)\\
\Rightarrow f(x) [1-x-x^2] &= 1\\
\Rightarrow f(x) &= \frac{1}{1-x-x^2}
\end{align*}
or

$$
f(x) = \frac{-1}{x^2+x-1}
$$

Now go back to 

$$
f(x) = F_0 + F_1 x^1 + F_2 x^2 + F_3 x^3 + \cdots  = \sum_{n=0}^\infty F_n x^n
$$
and explain why $f(0.1)$ and $f(0.01)$, and in general $f(0.1^k)$ results in sequences of Fibonacci numbers.


### Deriving the Fibonacci formula
Our goal now is to take $f(x) = -1/(x^2+x-1)$ and write it out as a power series whose coefficients we know exactly.  We will do this by writing it as partial fractions, and then expanding each term as a series whose coefficients we know.

We can factor the denominator.  With the quadratic formula we find that the roots of $x^2+x-1=0$ are $-\frac{1\pm\sqrt{5}}{2}$.  We use $\phi$ as a shorthand for $\frac{1+\sqrt{5}}{2}$ (the Golden Ratio) and $\psi$ as a shorthand for $\frac{1-\sqrt{5}}{2}$.  

So $x^2+x-1 = (x+\phi)(x+\psi)$

- Use the fact that $x^2+x-1=(x+\phi)(x+\psi)$ to show that $\phi\psi=-1$.  (you can directly check that the product is $-1$, but you're asked to use a different method)
- Similarly show $\phi+\psi = 1$.

When using partial fractions to help integrate, we would write
\begin{align*}
\frac{-1}{x^2+x-1} &= \frac{-1}{(x+\phi)(x+\psi)}\\
\end{align*}
and solve for $A$ and $B$.  However, the formula we have for expanding a fraction out nicely when the denominator is a linear function is for the form $K/(1-rx)$.  So using $\phi\psi=-1$, we will rewrite this as

\begin{align*}
\frac{-1}{(x+\phi)(x+\psi)} &= \frac{-1}{(x+\phi)(x+\psi)} \frac{-\psi}{-\psi}\frac{-\phi}{-\phi}\\
&= \frac{1}{(1-x\psi)(1-x\phi)}
\end{align*}

So $f(x)$ can be written as

\begin{align*}
\frac{1}{(1-x\phi)(1-x\psi)} &= \frac{A}{1-x\phi} + \frac{B}{1-x\psi}\\
\Rightarrow 1 &= A(1-x\psi) + B(1-x\phi)
\end{align*}
Choosing nice values of $x$, we have
- $x=1/\phi$:  $1 = A(1-\psi/\phi)$
- $x=1/\psi$:  $1 = B(1-\phi/\psi)$

So 
- $ A = 1/(1-\psi/\phi)=\phi/(\phi-\psi)$
- $B = 1/(1-\phi/\psi)=\psi/(\psi-\phi)$

We can easily check that $\phi-\psi = \sqrt{5}$  So we get

\begin{align*}
A &= \frac{1}{\sqrt{5}} \phi\\
B &= -\frac{1}{\sqrt{5}} \psi
\end{align*}
So we finally have

\begin{align*}
f(x) = \frac{\phi}{\sqrt{5}} \frac{1}{1-\phi x} - \frac{\psi}{\sqrt{5}} \frac{1}{1-\psi x}\\
&= \sum_{n=0}^\infty \frac{\phi}{\sqrt{5}} \phi^nx^n +  \sum_{n=0}^\infty -\frac{\psi}{\sqrt{5}} \psi^n x^n\\
&= \sum_{n=0}^\infty \left( \frac{\phi^{n+1}}{\sqrt{5}} - \frac{\psi^{n+1}}{\sqrt{5}}\right)x^n\\
&= \sum_{n=0}^\infty \frac{\phi^{n+1} - \psi^{n+1}}{\sqrt{5}} x^n

\end{align*}

But it also satisfies

$$
f(x) = \sum_{n=0}^\infty F_n x^n
$$

So

$$
F_n = \frac{\phi^{n+1}-\psi^{n+1}}{\sqrt{5}}
$$

## Presentation Guidelines
