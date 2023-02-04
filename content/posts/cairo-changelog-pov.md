+++
title = "StarkNet & Cairo significant changes developer opinionated view"
date = "2023-02-03T19:00:03+01:00"
tags = ["starknet", "cairo"]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++


# What's new in Cairo?
 There have been a lot of changes since the Cairo language has been released. This is a developer opinionated list of the major changes since the first release, 0.6.2 (Dec 2021).

StarkWareLtd last release CairoLang v0.10.3 (Dec 5, 2022) also named Cairo 1.0.

Useful links:
 - [CairoLang releases](https://github.com/starkware-libs/cairo-lang/releases)

# v0.10 (Cairo 1.0)
(breaking changes version)
**Aug. 29 2022** v0.10.0-pre Pre-release

Starknet has its core language modified, it's now a Rusty lang, Starknet foresaw the future of Rust based smart-contract ecosystem ([Luna developers](https://news.coincu.com/90055-fall-of-terra/) and Solana)
 - End statements with ;
   - Note that new lines are still part of the language at this point, and you cannot put more than one instruction per line. This will change in Cairo1.0.
 - Use { … } for code blocks (instead of : and end)
 - Add () around the condition of if statements
 - Remove the member keyword in structs
 - Change comment to use // instead of #
 - Use ..., ap++ instead of ...; ap++ in low level Cairo code

 - New transaction version
     - Nonce are enforced as part of the transaction (bye bye UTXO model)
     - Invoke execution object with [**\_\_validate__**](https://github.com/OpenZeppelin/cairo-contracts/blob/d12abf335f5c778fd19d6f99e91c099b40865deb/src/openzeppelin/account/presets/EthAccount.cairo#L81) and [**\_\_execute__**](https://github.com/OpenZeppelin/cairo-contracts/blob/d12abf335f5c778fd19d6f99e91c099b40865deb/src/openzeppelin/account/presets/EthAccount.cairo#L127) to differentiate between validation of the transaction (wether or not execution works (TODO: wild guess)) and execution that his pickup by another part of the process in the decentralized system(TODO: confirm)
     - Declare function to send implementation code for registration
 - Bridge Layer1 to Layer2
     - New **fee** field in [LogMessageToL2 event](https://github.com/starkware-libs/cairo-lang/blob/54d7e92a703b3b5a1e07e9389608178129946efc/src/starkware/starknet/solidity/IStarknetMessagingEvents.sol#L9) when executing L2 contract from L1
 - Tx simulation and fee estimation
 - Support the EC-op builtin. to allows to verify ECDSA signatures
 - API: Remove entry_point_type field from transaction information

# v0.9.x

Fees are now enforced on StarkNet, no more free candy!

Contracts must be declared first and then instanciated through the new [deploy syscall](https://starknet.io/docs/hello_starknet/deploying_from_contracts.html#the-deploy-system-call) forcing 2 manual transactions for contracts deployed by EOA.

# v0.8.1

Fees are in now! What's up with that [code](https://github.com/starkware-libs/cairo-lang/blob/4e233516f52477ad158bc81a86ec2760471c1b65/src/starkware/starknet/business_logic/transaction_fee.py) ? See more [here](https://starknet.io/documentation/fee-mechanism/#Introduction).
![](https://i.imgur.com/G2ZidCf.png)

 - charge_fee ![](https://i.imgur.com/GnKEkFI.png)
 - calculate_tx_fee_by_cairo_usage ![](https://i.imgur.com/wYIohf7.png)


- [L1 -> L2 message cancellation](https://github.com/starkware-libs/cairo-lang/blob/master/src/starkware/starknet/eth/StarknetMessaging.sol)
![](https://i.imgur.com/P4UB8Wm.png)

- `version` and `max_fee` are part of the transaction structure now

- `__execute__` is now required mandatory entry point for account contract,  see more [here](https://github.com/OpenZeppelin/cairo-contracts/blob/main/docs/Account.md#accounts)
![](https://i.imgur.com/gIcuAdK.png)

 - Added the cryptographic hash function [blake2s](https://en.wikipedia.org/wiki/BLAKE_(hash_function)) to the standard library
 
## Cairo
 - Meaningful error messaging(v0.7.0) including local variables and arguments
![](https://i.imgur.com/AwjYaIV.png)
 - High level memory allocation with the `new` keyword in execution memory segment (whereas `alloc` allocates a new memory segment)
 ![](https://i.imgur.com/gFPTHzw.png)

 - Tuples and type aliases, will increase the pythonic vibes of Cairo even further
 ![](https://i.imgur.com/Ya3bPcE.png)
 
 - Fix for python 3.9

# v0.7.x

- [Added a nonce for L1 to L2 message](https://github.com/starkware-libs/cairo-lang/blob/4e233516f52477ad158bc81a86ec2760471c1b65/src/starkware/starknet/services/api/messages.py#L80) this prevents sending the same message twice from the EVM world, e.g: calling a function.
![](https://i.imgur.com/3SPa5Fz.png)

# Addition of EVM compatibilities
 - events are here !
 
![](https://i.imgur.com/rXdCLNc.png)
![](https://i.imgur.com/uOzGLmA.png)

(editor's note: TheGraph but for StarkNet please.)

 - delegate calls
 prepend delegate_ to external contract function name or `l1_handler`
 - The `__default__` entry point is introduced, it is similar to the Solidity fallback method as it is executed after missing on the function selector.
 - The `__l1_default__` entry point same as `__default__` but for in-protocol message from the L1.

## New syscalls
 - get_block_timestamp()
 Returns a random number that sometimes appears to grow over time, currently around since 1970-01-01.
Notice of deprecation for get_tx_signature(), get_tx_info() is now preferred.
