---
layout: post
title: Hello world!
subtitle: A small post to test the website functionality
tags: [test]
comments: true
---

Here, have some solidity to comfort you
```solidity
pragma solidity 0.8.15;

contract Test {
    function run(bytes32 a) external pure returns (bytes32) {
        return keccak256(a);
    }
}
```
