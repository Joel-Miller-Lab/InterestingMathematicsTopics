# Sicherman Dice

Consider two normal dice.  When we roll these dice, a sum of $7$ is much more probable than a sum of $2$ or $12$.  In fact, we can work out the probabilities of each sum using a simple table:
 

|           | <span class="die-face">⚀</span> | <span class="die-face">⚁</span> | <span class="die-face">⚂</span> | <span class="die-face">⚃</span> | <span class="die-face">⚄</span> | <span class="die-face">⚅</span> |
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:| 
| <span class="die-face">⚀</span> | <span class="sum-2">2</span> | <span class="sum-3">3</span> | <span class="sum-4">4</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> |
| <span class="die-face">⚁</span> | <span class="sum-3">3</span> | <span class="sum-4">4</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | 
| <span class="die-face">⚂</span> | <span class="sum-4">4</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> |
| <span class="die-face">⚃</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> | <span class="sum-10">10</span>|
| <span class="die-face">⚄</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> | <span class="sum-10">10</span>| <span class="sum-11">11</span>|
| <span class="die-face">⚅</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> | <span class="sum-10">10</span>| <span class="sum-11">11</span>| <span class="sum-12">12</span>|

Let $S$ be the value of the sum of the two dice.  The probability that $S=2$ is $P[S=2]=1/36$.  The probability of a sum of $7$ is $P[S=7]=6/36=1/6$. 

Remarkably, there is another pair of $6$-sided dice with positive integer values which yield the same sums with the same probabilities.  The two dice in the pair are numbered differently:

|           | <span class="die-face">⚀</span> | <span class="die-face">⚁</span> | <span class="die-face">⚁</span> | <span class="die-face">⚂</span> | <span class="die-face">⚂</span> | <span class="die-face">⚃</span> |
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|
| <span class="die-face">⚀</span> | <span class="sum-2">2</span> | <span class="sum-3">3</span> | <span class="sum-3">3</span> | <span class="sum-4">4</span> | <span class="sum-4">4</span> | <span class="sum-5">5</span> |
| <span class="die-face">⚂</span>| <span class="sum-4">4</span> | <span class="sum-5">5</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> |
| <span class="die-face">⚃</span> | <span class="sum-5">5</span> | <span class="sum-6">6</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> |
| <span class="die-face">⚄</span> | <span class="sum-6">6</span> | <span class="sum-7">7</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> |
| <span class="die-face">⚅</span> | <span class="sum-7">7</span> | <span class="sum-8">8</span> | <span class="sum-8">8</span> | <span class="sum-9">9</span> | <span class="sum-9">9</span> | <span class="sum-10">10</span>|
| ![Die showing eight](die-8.png) | <span class="sum-9">9</span> | <span class="sum-10">10</span>| <span class="sum-10">10</span>| <span class="sum-11">11</span>| <span class="sum-11">11</span>| <span class="sum-12">12</span>|

It will turn out that there is only one such pair of dice that matches the normal pair.  This pair is known as "Sicherman Dice".  We will learn an efficient way to find that pair and show that it is the only such pair.  The methods we learn are used in applications as varied as infectious disease modelling, statistical physics, and the calculation of some infinite sums.

## A warmup problem

Before we find the Sicherman Dice, we'll look at a warmup problem.  It won't be obvious until later why this is relevant to this question.

Consider the number $900=2^2 \cdot 3^2 \cdot 5^2$.

Find all pairs of even numbers that multiply together to give $900$.  You should be able to use the prime factorization to do this efficiently.
## Probability Generating Functions

```{prf:definition}
Given a probability distribution for the non-negative integers, so that the probability of the integer $k$ is $p_k$, a **Probability Generating Function** (PGF) is the function

$$
f(x) = \sum_k  p_k x^k
$$
```

You should verify that all the coefficients must be non-negative, that $f(1)=1$, and $f(0) = p_0$.

In the case of a single normal die 

$$
f_{\text{normal die}}(x) - \frac{x+x^2+x^3+x^4+x^5+x^6}{6}
$$

### Product of PGFs
We can use a tabular form to calculate the value of $(f_{\text{normal die}}(x))^2$:

|           | $x/6$ | $x^2/6$ | $x^3/6$ | $x^4/6$ | $x^5/6$ | $x^6/6$|
|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:|:---------:| 
| $x/6$ | <span class="sum-2">$x^2/36$</span> | <span class="sum-3">$x^3/36$</span> | <span class="sum-4">$x^4/36$</span> | <span class="sum-5">$x^5/36$</span> | <span class="sum-6">$x^6/36$</span> | <span class="sum-7">$x^7/36$</span> |
|$x^2/6$ | <span class="sum-3">$x^3/36$</span> | <span class="sum-4">$x^4/36$</span> | <span class="sum-5">$x^5/36$</span> | <span class="sum-6">$x^6/36$</span> | <span class="sum-7">$x^7/36$</span> | <span class="sum-8">$x^8/36$</span> | 
| $x^3/6$ | <span class="sum-4">$x^4/36$</span> | <span class="sum-5">$x^5/36$</span> | <span class="sum-6">$x^6/36$</span> | <span class="sum-7">$x^7/36$</span> | <span class="sum-8">$x^8/36$</span> | <span class="sum-9">$x^9/36$</span> |
| $x^4/6$ | <span class="sum-5">$x^5/36$</span> | <span class="sum-6">$x^6/36$</span> | <span class="sum-7">$x^7/36$</span> | <span class="sum-8">$x^8/36$</span> | <span class="sum-9">$x^9/36$</span> | <span class="sum-10">$x^{10}/36$</span>|
| $x^5/6$ | <span class="sum-6">$x^6/36$</span> | <span class="sum-7">$x^7/36$</span> | <span class="sum-8">$x^8/36$</span> | <span class="sum-9">$x^9/36$</span> | <span class="sum-10">$x^{10}/36$</span>| <span class="sum-11">$x^{11}/36$</span>|
| $x^6/6$| <span class="sum-7">$x^7/36$</span> | <span class="sum-8">$x^8/36$</span> | <span class="sum-9">$x^9/36$</span> | <span class="sum-10">$x^{10}/36$</span>| <span class="sum-11">$x^{11}/36$</span>| <span class="sum-12">$x^{12}/36$</span>|

There is a clear similarity between this table and the table used to calculate the probabilities of a sum of a pair of normal dice.  You should be able to see that the coefficient of $x^k$ in the product is found in the same way as the probabability that the sum of two normal dice is $k$: $P[S=k]$.  This reasoning can be extended to the product of any two PGFs.

```{prf:theorem} Product of two PGFs
Given two PGFs, their product is a PGF which corresponds to the PGF of the process of choosing one number from each of the distributions and adding them together.
```

You should be able to explain why this theorem is true.  It will help to consider two distributions.  Here is an outline of how to do it:
- Let $p_k$ be the probability of a $k$ from the first distribution and $q_k$ be the probability of $k$ from the second distribution.
- Use summations ($\sum$) to write down the PGF $f(x)$ and $g(x)$ of each distribution.  
- let $s$ be a fixed (but unknown) non-negative integer.  Using summations ($\sum$), express the probability of getting a sum of $s$ by choosing one number $k_1$ from one distribution and $k_2$ from the other and adding them together.
- Similarly, look at how the coefficient of $x^s$ is determined from $f(x)g(x)$.  Show that the expression for the coefficient is the same as the expression for the probability of a sum of $s$.

## Finding the Sicherman dice
We let $f(x)$ be the PGF for a normal die, with $(f(x))^2$ being the PGF for the sum from two normal dice.  

Assume that there is some pair of dice, each with positive integer values, that give the same sums with the same probabilities.

- Let $h(x)$ and $g(x)$ be the PGFs for the two dice.
- Explain why $h(x)g(x)=(f(x))^2$.
- Fully factor $(f(x))^2$ using real coefficients.  It may help to review the factorization of $x^k+y^k$ where $k$ is an odd integer (specifically for $k=3$).
- Use the Fundamental Theorem of Algebra (taught in ``journeyman level'') and possibly the quadratic formula to show that your expression cannot factor any further using real coefficients.
- Determine what $g(0)$ and $h(0)$ must be if all value on the dice are positive integers.
- Determine what $g(1)$ and $h(1)$ must be (since they are both PGFs).
- Using the fact that they correspond to $6$-sided dice, explain why $g(x) = \frac{x^{a_1}+x^{a_2}+ \cdots + x^{a_6}}{6}$ and $h(x) = \frac{x^{b_1}+x^{b_2}+ \cdots + x^{b_6}}{6}$.
- Using your factorization of $(f(x))^2$ and what you know about the $g(0)$, $g(1)$, $h(0)$, and $h(1)$, determine what the values of the dice are.  It may help to revisit the warmup problem of finding all pairs of even numbers that multiply together to give $900$.
- How do you know there are no other such dice pairs?

Now repeat this for tetrahedral (4-sided) dice.

## Presentation guidelines

You should present a derivation of Sicherman Dice, showing that it is the only other pair with the same sum as a regular pair.

Your presentation should be aimed at a student who understands the concept of factorization of polynomials and knows the Fundamental Theorem of Algebra for polynomials with real coefficients.  You can assume that the student understands some basic properties of probabilities (specifically, when you would add or multiply two probabilities).

You will need to explain what a PGF is and justify any properties of PGFs that you use.

