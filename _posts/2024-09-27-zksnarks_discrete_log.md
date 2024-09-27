---
layout: post
title: Zero Knowledge Proofs Series Part 3
subtitle: The Discrete Logarithm Problem
tags: zk, cryptography
---

# Intro
This blog post takes a step into what I believe is now the interesting part of cryptography and what makes it such a fascinating subject. For this blog post, I expect readers to be able to have a fundemental grasp of Group Theory (or at least notation).

We will be focusing today on the following problem (this is specifically the **multiplicative** discrete logarithm problem).

Given a large prime $$p$$, and two distinct elements $$a, b \in \mathbb{F}_p$$. Find an element $$x \in \mathbb{Z}$$ such that:
\\
$$a^x = b \mod p$$
\\
Equivalently, find an element $$x$$ such that $$\log_a b = x$$

## Intuition
When working with our more traditional numbers, "normal" logarithms are very easy to compute. Modern computer architectures use a variety of methods such as Taylor's Theorem where we break down the logarithm into a polynomial. However, when it comes to working with Finite Fields such as $$\mathbb{F}_p$$, logarithms do not behave so nicely. For example, consider calculating $$x = \log_5 18$$ as you usually would. 

We know that $$5^1 < 18 < 5^2$$ so by the "montonicity" of the logarithm, we know that $$1 \leq x \leq 2$$. We can further narrow down $$x$$ by calculating $$5^{1.5} < 18 < 5^{1.8}$$ which gives us an even narrower bound for $$x$$. This can be repeated to produce $$x$$ to a very high accuracy relatively quickly.

Now consider $$x = \log_5 18$$ over $$\mathbb{F}_{23}$$.
Calculating a few powers of $$5$$, we get: 
\\
$$5^2 = 25 = 2 \mod 23$$
\\
$$5^3 = 125 = 10 \mod 23$$
\\
$$5^4 = 4 \mod 23$$
\\
There is no obvious pattern for how the result of $$a^x$$ behaves when working over a prime field. This makes deriving "nice" algorithms to calculate a discrete logarithm much harder. Naturally, the difficulty of this calculation depends a huge amount of your choice of $$p$$. For small values of $$p$$, modern computers can very quickly bruteforce solutions by calculating $$5^1, 5^2, 5^3, ...$$ and comparing each result to the desired value.

For very large values of $$p$$, brute forcing is not feasible and a few algorithms have been proposed to offer better alternatives. The different algorithms vary in efficiency depending on the properties of $$p$$. However in general, the time complexity is $$\mathcal{O}(\sqrt{p})$$. 

Some readers may stop for a second and ask what's wrong with a time complexity of $$\mathcal{O}(\sqrt{p})$$. In a lot of applications, people would be delighted to produce such fast algorithms. This is what I believe is so interesting about the Discrete Logarithm problem (and simliar problems in cryptography).

It turns out that calculating the exponent in a Finite Field can be done very efficiently using [exponentation by squaring](https://en.wikipedia.org/wiki/Exponentiation_by_squaring) which at takes most $$\lceil \log_2 x \rceil$$ operations where $$x$$ is the exponent in $$a^x$$.

Therefore, in comparison, it is much easier to calculate an exponent then a discrete logarithm even if both can be quite efficient. This difference is crucial in the security of the Discrete Logarithm problem. The Discrete Logarithm problem is a perfect example of a "trapdoor" function, a function where it is very easy to calculate one way, but much more difficult to calculate the inverse.

## How do I know the Discrete Logarithm stays secure?
There is no proof that the Discrete Logarithm problem is difficult, we only say it is difficult because we have not found an algorithm which has a time complexity of $$\mathcal{O}(\log n)$$. It is entirely possible that someone will figure out a very efficient method of calculating the discete logarithm and break much of modern cryptography. However, that day has not come quite yet, and people are willing to bet that the Discrete Logarithm problem will stay "difficult" enough to be used in cryptography (in the pre-quantum era).

## Next Time
In my next blog, I will take a first look at a class of zero knowledge proof - Sigma protocols and what properties define a "Zero-Knowledge proof". Stay tuned!  



