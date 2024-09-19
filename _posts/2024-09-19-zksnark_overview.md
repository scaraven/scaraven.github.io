---
layout: post
title: Zero Knowledge Proofs Series Part 1
subtitle: A qualitative overview into ZK proofs
tags: zk, cryptography
---

# Intro 
Although I complained in the last blog about qualitative explanations of zero knowledge proofs. Such explanations are not without their merits. Explaining the mathematics behind a concept is very difficult to understand when you do not understand what you are trying to build to begin with.

# What is Zero Knowledge
Zero Knowledge proofs traditionally occur between two people, a Prover and a Verifier who are both focusing on a common "problem".

In this setup, the Prover has a solution and needs to *prove* to the Verifier that they indeed know the solution. Traditionally, the Verifier will ask questions about the solution which the Prover needs to answer. If the Prover answers enough questions correctly, the Verifier can be certain that there is a negligible (not quite zero) probability that the Prover knows the solution.

The beauty of these proofs, is that the Verifier does not learn anything about the solution itself (or anything which might hint to a possible solution). Now, you might ask, how is it possible that the Verifier ask questions, receives and verifies answers without every learning about the solution?

That we will look over the next few blog posts.

## Where's Waldo Analogy
If the previous explanation is still difficult to wrap your head around. There exists a famous analogy which I like to tell friends and family when trying to illustrate ZK proofs. Another similiar retelling can be found [here](https://www.galaxy.com/insights/perspectives/zero-knowledge-proofs-the-magic-key-to-identity-privacy/)


Imagine you have a "Where's Waldo" book which is a children's comic book where each page is filled with a massive amount of [zany characters and scenarios](https://miro.medium.com/v2/resize:fit:5656/1*7v_75ZGg1CTmWAw1rEgMHQ.jpeg). Your task is to find "Waldo".

Assume that I am the Prover and have gone through the effort to find Waldo but I do not want anyone else to profit off my hard work. I can take a massive piece of cardboard, many times size of the book, and cut a small hole the size of Waldo's face. I then place the small hole over Waldo's face.

I have now proven I know where Waldo is, but a Verifier will not be able to figure out where the book is in respect to the hole and therefore cannot derive Waldo's exact or approximate location (lets say the book is perfectly flat so you cannot see the edges under the cardboard).

Although this is not exactly how Zero Knowledge proofs work, it aptly illustrates that it is possible to prove knowledge of a solution without every giving away that solution.


# Why should I care?

An obvious application is in privacy. Using ZK Proofs, you would be able to prove to your local tax authority that you earn below a certain threshold and so are not liable to pay a certain tax percentage.

Other, less obvious applications, occur when there is a large computational power difference between the Prover and the Verifier. It is possible that verifying a zero knowledge proof is a lot faster than verifying the solution to a problem itself and in applications (smart contracts on the Ethereum blockchain) where computations are very expensive, ZK proofs may be preferrable.

# That's it for today folks
For my next blog, I will dive into the more mathematical nature of ZK proofs and start with the fundementals: Groups, Fields and Rings!

