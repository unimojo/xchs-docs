# XSIP-5: Staked Indexer Committee

**DRAFT**

## Abstract



## Motivation

The parsing of inscription protocols like BRC20 is plagued by significant obstacles, making the effective interpretation and use of these protocols complex:

1. **Centralization and Complexity**: The majority of parsing realized under the current design is considerably centralized, leading to unnecessary costs and complications in maintaining data consistency, which necessitates frequent reconciliation checks.

2. **Difficulty in Achieving Consensus**: Inscription protocols at the core are agreements of off-chain consensus. The task of incentivizing off-chain entities to achieve such consensus is challenging. Thus, a deterministic approach to reach consensus is indispensable.

3. **Limitations on Protocol Evolving**: When initiating or updating inscription protocols, issuers tend to either independently craft complex parsing service codes or lean heavily on alliances with current parsing entities. This leads to protocol upgrades requiring extensive communication between parsing entities to reach consensus.

That is to say, a mechanism dedicated to facilitating consensus among off-chain parsing entities is extremely necessary. Therefore, this XSIP proposes the establishment of the Staked Indexer Committee, a committee established depend on XSIP-2 decentralized indexing for achieving decentralized off-chain consensus.

## Specification

### Committee

The Committee is comprised of multiple parsing entities. Whether or not they use the same codebase for generating the inscription chain, they should reach consensus along the main chain.

With XSIP-2 already implementing the software for generating inscription chain blocks, what Committee members need to do is to keep the block producer running. The software should then report each member's latest status to each other.

Moreover, if the software deems a member is in mal-operation, it would vote for a slash of that member.

As one may imagine, to join the committee, a certain amount of staked funds is required, which would be slashed if mal-operation continues for a period of time. Also, incentives should be provided for every successfully generated block.

### Operations

We designed the operation protocol with universality in mind.
Where we place the operations can be determined later, with considerations being found in the Rationale section.

#### Join

Ask to join the block producer network with certain amount to stake and its public key registered.

```js
{
  'p': 'xchs',
  'op': 'join',
  'amt': '1000000',
  'pubkey': 'b976ead8b3fe50d6813d6073cc161fc020f399fc7789e55c0da944ad8b5d04da418159e5dc40e492258baf2ca5123278'
}
```

| Key | Required? | Description                                                       |
| --- | --------- | ----------------------------------------------------------------- |
| amt | Yes       |  |
| pubkey | Yes       | BLS public key |

#### Report

Report the hash at specific height by the block producer.

```js
{
  'p': 'xchs',
  'op': 'report',
  'height': '4800000',
  'hash': '02055edbd965f9d49fd95e1822249a9efdb6d9ff4c1e1c71d428656193577b77'
}
```

| Key | Required? | Description                                                       |
| --- | --------- | ----------------------------------------------------------------- |
| height | Yes       | report height  |
| hash | Yes       | report hash of specific height |

#### Vote-Slash

Vote to slash certain block producer with public key in ripemd160 encoding, accuse it mal-behavior at specific height, with signature from block producer.

```js
{
  'p': 'xchs',
  'op': 'slash',
  'height': '4801234',
  'pubkey': 'ec206ed55d2c47843d2defaba41e869a8572897e',
  'sig': '998899f4edfef5a4a44874c862bd841ce7bd60c97b741a3c0d8243e95a05479e319a94a8fe65b7e3f9384e06b135192f14db7a03bb78929db3105482b54551025b592f81cb7d2535c7ce5e6b1a442feaf7e0da197c829cc34bdb2655af65b32a'
}
```

| Key | Required? | Description                                                       |
| --- | --------- | ----------------------------------------------------------------- |
| height | Yes       | height that is mal-behavior  |
| pubkey | Yes       | the pubkey in ripemd160 encoding which is mal-behavior |
| sig | Yes       | the signature provided who is accusing other is mal-behavior |

### Incentive

The specifics of incentives are beyond the scope of this proposal and are subject to change according to the circumstances that prevail at that time.

However, to make the incentive system work, a special token would be issued. This token would support unlimited minting, but only allow minting when a block is successfully generated and included in the chain.

## Rationale

### Operations: Main Chain vs Inscription Chain vs Off-chain

## Security Considerations
