# XSIP-5: Staked Indexer Committee

**WIP**

## Abstract



## Motivation

The parsing of inscription protocols like BRC20 is plagued by significant obstacles, making the effective interpretation and use of these protocols complex:

1. **Centralization and Complexity**: The majority of parsing realized under the current design is considerably centralized, leading to unnecessary costs and complications in maintaining data consistency, which necessitates frequent reconciliation checks.

2. **Difficulty in Achieving Consensus**: Inscription protocols at the core are agreements of off-chain consensus. The task of incentivizing off-chain entities to achieve such consensus is challenging. Thus, a deterministic approach to reach consensus is indispensable.

3. **Limitations on Protocol Evolving**: When initiating or updating inscription protocols, issuers tend to either independently craft complex parsing service codes or lean heavily on alliances with current parsing entities. This leads to protocol upgrades requiring extensive communication between parsing entities to reach consensus.

That is to say, a mechanism dedicated to facilitating consensus among off-chain parsing entities is extremely necessary. Therefore, this XSIP proposes the establishment of the Staked Indexer Committee, a committee established depend on XSIP-2 decentralized indexing for achieving decentralized off-chain consensus.

## Specification

### Committee

Committee is comprised of multiple parsing entities, whether using same code base for generating inscription chain or not, they should reach consensus along the main chain.

As XSIP-2 already implemented the software to generating the inscription chain blocks.
What committee member need to do, is just keep the block producer running and the software should report to each other about their latest status.

The software also would vote for slash if it deem one member is mal-operation.   

As you may imagine, to join the committee, certain amount of staked funds is necessary, and would be slashed when mal-operation for a period of time. Also, incentive should be generated for every success block generated.

### Operations

#### Report


```js
{
  'p': 'xchs',
  'op': 'report',
  'tick': 'xchs'
}
```

#### Vote


```js
{
  'p': 'xchs',
  'op': 'vote',
  'tick': 'xchs'
}
```

### Incentive

The detail of incentive is out of scope of this proposal, and subject to change according to circumstance at that time.

But to make the incentive to work, a special token would be issued that support unlimited minting, while only allow minting when a block successful generated and included in the chain.

## Rationale


## Security Considerations
