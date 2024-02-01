# XSIP-3: Flexible Smart Contract

**DRAFT**

## Abstract

TBD

## Motivation

The Account Model presents several advantages over the UTXO Model. Here are some primary ones:

1. **Simpler State Representation**: The account model directly maintains account balances and smart contract states. This is more intuitive and easier to understand compared to UTXO's system of tracking unspent transaction outputs.

2. **Smart Contract Flexibility**: The Account Model, gives much more power and flexibility to developers. Allowing for more complex processes and applications to be created.

3. **Reduced Space Complexity**: Accounts model only needs to keep track of the final state of accounts (each account's balance and associated smart contracts), while UTXO model has to maintain all the unspent transaction outputs across the entire network.

4. **Ease of Transaction Writing**: In the UTXO model, a transaction has to consume all the funds held in a UTXO, and if not all funds are spent, a change address must be specified. Whereas, in the Account Model, funds can be transferred directly from one account to another without the need to consume all the funds all at once.

## Specification

TBD

## Rationale

**Programming Language**

TBD: Lisp with I/O Monad

## Security Considerations

TBD
