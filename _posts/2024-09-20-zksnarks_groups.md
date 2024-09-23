---
layout: post
title: Zero Knowledge Proofs Series Part 2
subtitle: A mathematical primer into cryptography
tags: zk, cryptography, modular arithmetic
---

# Intro
Some readers may be familiar with the term of groups, fields and modular arithmetic. If $$\forall x \in \mathbb{Z}_p: x^{p-1} \equiv 1 \mod p$$ makes sense to you, then you can skip this blog and move onto the next one.

Otherwise, I will be providing a quick overview into what groups and fields are. To note, this will only cover the fundementals which will be enough to understand the content of the next few blogs. However, group theory and abstract algebra are both very deep and expansive topics in the world of mathematics so I would highly recommend that the reader do some [extra research](https://www.math.uci.edu/~ndonalds/math120a/notes.pdf) if they are so interested.

## Definitions
Before we get into what groups and fields are, I'll detour a bit into their motivation. Mathmaticians like to abstract and generalise the common tools we work with and derive interesting properties from these mathematical objects.

For example, take the integers : $$\mathbb{Z} = \{..., -3, -2, -1, 0, 1, 2, 3, ...\}$$. We can add integers and multiply them together to produce other integers  however if we divide certain integers than we will get rationals instead such as $$\frac{1}{2}$$ which doesn't belong to our set of integers!

So how do we formalise such properties such as addition and multiplication on different sets? We first look at common mathematical objects in our lives and the operations which can be used on them. We then generalise the information and define groups, fields, etc...

### Groups
A group is defined as so:

take a set of elements $$A$$ and a binary "addition" operation which satisfies the following properties:
1. $$\forall x,y \in A \ x + y \in A$$ the addition of two elements in A is another element in A
2. $$\exists 0 \in A \ \forall x \in A \ x + 0 = 0 + x = x$$ there exists a 0 element in A which does nothing to the element it is added to
3. $$\forall x \in A \ \exists y \in A \ x + y = 0$$ every element in A has an inverse whose addition gives you $$0$$
4. $$\forall x,y,z \in A \ (x + y) + z = x + (y + z)$$ you can add elements in different orders and you will get the same result

Be careful of not falling into the common trap that group elements satisfy the property $$x + y = y + x$$ (known as commutativity).
This is not always the case and is the **main** way that the definition of groups differs to the properties of integers.

If you don't want to remember all the rules for a group, a quick way to derive them is by thinking of groups to be simliar to integers without commutativity.


### Fields
Fields are extensions to groups which introduces another "multiplication" operation along with the property of commutativity

Therefore, we add on a few more rules that we established for a group
1. $$\forall x,y \in A \ x + y = y + x$$ commutativity for addition
2. $$\exists 1 \in A \ 0 \neq 1, \forall x \in A \ 1 \times x = x \times 1 = x$$ you have an "identity" for multiplication
3. $$\forall x,y \in A \ x \times y = y \times x$$ commutativity for multiplication
4. $$\forall x,y \in A \ x \times y \in A$$ multiple of two elements is another element in A
5. $$\forall x,y,z \in A \ x \times (y \times z) = (x \times y) \times z$$ order of multiplication does not matter
6. $$\forall x,y,z \in A \ x \times (y + z) = (x \times y) + (x \times z)$$ you can "expand" out elements in brackets when multiplied
7. $$\forall x \in A \ \exists y \in A \ x \times y = y \times x = 1$$ you can always find an inverse for an element in A which multiplies out to $$1$$

If this is the first time you are seeing these definitions, I would not recommend forcing yourself to remembering them. Instead, the Rational numbers is a perfect example for a field and can be used to derive most of the rules.

# Modular Arithmetic
Now that we have defined what a group and a field is, it begs the question of why should you care about any of this? 
It turns out that you can have some very interesting mathematics when you work over different fields, most notably modular arithmetic.

Take a look at the modular arithmetic challenges [here](https://cryptohack.org/challenges/general/) if you want to practice your knowledge on modular arithmetic.

One way to look at modular arithmetic is that you choose a positive number $$p$$ as a "base" and when you add or multiply numbers you divide the result by $$p$$ to find the remainder.

E.g. let $$p = 5$$

$$1 + 6 = 7 = 2 \mod 5$$
\\
$$3 * 33 = 99 = 4 \mod 5$$
\\
$$-1 = -5 + 4 = 4 \mod 5$$

On the other hand, we can see modular arithmetic as operations on a field. If we are to translate the example above, we would use the field $$\mathbb{F}_5$$ 
which is compromised of the set $$\{0, 1, 2, 3, 4\}$$ and supports the operations shown above.

Other examples of fields which represent modular arithmetic but with a different "base" look like this:
$$\mathbb{F}_3 = \{0, 1, 2\}$$
\\
$$\mathbb{F}_6 = \{0, 1, 5\}$$
\\
$$\mathbb{F}_p = \{0, 1, 2, 3, ..., p - 1\}$$ where $$p$$ is a prime number

You may notice that $$\mathbb{F}_6$$ does not follow the pattern for $$\mathbb{F}_5$$ and $$\mathbb{F}_3$$. This is because the number $$6$$ shares factors with numbers which are smaller than it, namely $$2$$ and $$4$$. If you try to apply rule 7 of a Field to $$2$$, you will find out that there does not exist a number which produces $$1$$ when multiplied by $$2$$ modulo $$6$$.

## Operations matter
It is very important to note that the operations which are using will drastically change how a set of elements will look. For example, consider the "integers modulo 6" which is usually symbolised as $$\mathbb{Z}_6$$. This is not a field but instead a special type of group known as an Abelian group (a group which supports commutativity). This means that you can only apply addition on the elements but in turn allows you to include numbers below $$6$$: $$\{0, 1, 2, 3, 4, 5\}$$

# Next time
In the next blog we will take a look at the Discrete Logarithm Problem applied to large groups and its importance to cryptography!





