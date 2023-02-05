+++
title = "Support cours Ethereum Virtual Machine"
date = "2022-03-17T21:50:00+01:00"
cover = "/img/posts/support-evm/cover.jpg"
showCover = false
tags = ["teaching", "french", "esilv", "evm", "ethereum"]
keywords = ["teaching", "french", "esilv", "evm", "ethereum"]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

Ceci est un support de cours sur l'EVM (Ethereum Virtual Machine) pour le cours de l'Ecole Supérieure d'Ingénieurs Léonard de Vinci (ESILV).

Il comprend du matériel de cours, des illustrations et des liens vers des ressources.

La durée du cours est de 3h, séparé en une lesson de 1h15 et des travaux dirigés de 1h15.
La première partie est une introduction à la machine de Turing et sa correspondance aux processeurs de nos jours (rappel des connaissances),
la seconde partie est une introduction à l'EVM et sa correspondance avec la machine de Turing.

Les travaux pratiques consistent à observer le fonctionnement de l'EVM ainsi que la lecture des [opcodes](https://www.evm.codes/) au travers du debugger [Remix](https://remix.ethereum.org/) et à implémenter des opcodes directement dans un second temps.

NB: Tenderly peut-être utilisé pour une meilleure observervation du fonctionnement de l'EVM sur la blockchain Ethereum mais un peu plus long à mettre en place.

# Machine de Turing

Machine de Turing
![](/img/posts/support-evm/mThs6b2.jpg)
https://www.youtube.com/watch?v=L5O04P2ASRc&t=647s

# Ethereum Virtual Machine (EVM)

![](/img/posts/support-evm/ysIsVUG.png)

---

![](/img/posts/support-evm/Xba9Jwb.png)

---

Lexiques
https://github.com/asseth/yellowpaper/blob/7dd3ed26b6fe4b7a1b0394194ef268d01f9955b4/Paper.pdf Page 17
    
---

![](/img/posts/support-evm/Lo0fP89.png)

---

![](/img/posts/support-evm/8cOg89m.png)

---

![](/img/posts/support-evm/vRJgorg.png)

---

![](/img/posts/support-evm/tMgjFeK.png)

---

![](/img/posts/support-evm/cnV0k5f.png)

---

![](/img/posts/support-evm/0J3imfd.png)

---

Dive in http://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf

## Illustration
 - Illustration Turing machine => https://medium.com/creative-automata/classic-turing-machine-with-tape-erasure-e14870ad154e
 - http://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf

## Bibliography
 - :fr: [EIP-150 Yellowpaper](https://github.com/asseth/yellowpaper/blob/7dd3ed26b6fe4b7a1b0394194ef268d01f9955b4/Paper.pdf)
 - :uk: [Updated Yellowpaper](https://ethereum.github.io/yellowpaper/paper.pdf)
 - [Yellowpaper Cheat Sheet](https://github.com/benjaminion/YellowPaper_CheatSheet)
 - [Ethereum EVM Illustrated](http://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf)

 - Execution model Page 56

## Implementation
 - [Implementation allocation](https://github.com/ethereum/go-ethereum/blob/master/core/vm/interpreter.go#L138)

# Travaux dirigés
 - [Remix](https://remix.ethereum.org/)
 - [EVM opcodes](https://www.evm.codes/)

 Solidity sources to analyze:
  - Goal, observe the behavior of the EVM between the differents implementation functions of the same algorithm:
    - Sum of an array of uint.
 ```solidity
// SPDX-License-Identifier: GPL-3.0
pragma solidity >=0.4.16 <0.9.0;

library VectorSum {
// This function is less efficient because the optimizer currently fails to
// remove the bounds checks in array access.
function sumSolidity(uint[] memory data) public pure returns (uint sum) {
    for (uint i = 0; i < data.length; ++i)
        sum += data[i];
}

// We know that we only access the array in bounds, so we can avoid the check.
// 0x20 needs to be added to an array because the first slot contains the
// array length.
function sumAsm(uint[] memory data) public pure returns (uint sum) {
    for (uint i = 0; i < data.length; ++i) {
        assembly {
            sum := add(sum, mload(add(add(data, 0x20), mul(i, 0x20))))
        }
    }
}

// Same as above, but accomplish the entire code within inline assembly.
function sumPureAsm(uint[] memory data) public pure returns (uint sum) {
    assembly {
        // Load the length (first 32 bytes)
        let len := mload(data)

        // Skip over the length field.
        //
        // Keep temporary variable so it can be incremented in place.
        //
        // NOTE: incrementing data would result in an unusable
        //       data variable after this assembly block
        let dataElementLocation := add(data, 0x20)

        // Iterate until the bound is not met.
        for
            { let end := add(dataElementLocation, mul(len, 0x20)) }
            lt(dataElementLocation, end)
            { data := add(dataElementLocation, 0x20) }
        {
            sum := add(sum, mload(dataElementLocation))
        }
    }
}
}
```

# Contact

 - [@magicking_](https://twitter.com/magicking_)
 - [s@6120.eu](mailto:s@6120.eu)
 - [https://6120.eu](https://6120.eu)