# XSIP-2: Decentralized Indexer

**WIP**

## Abstract

The proposal seeks to establish a decentralized indexing mechanism for inscription data. The aim is to address the issues tied to centralized indexes that can expose a protocol to risk if the singular indexer experience any problems, potential falsely issuing tokens or even leading to overall protocol stagnation. Decentralized indexing brings about improved security, flexibility and efficiency that can, in turn, spur further activity and growth within the ecosystem.

## Motivation

Presently, the structure of most inscription protocols relies heavily on centralized indexes. This concentration often resides with a single indexer or less commonly, a handful, proving inadequate for optimal performance and security. With data handled in off-chain servers, they make the protocol susceptible to vulnerability, disruption, and even falsification. The proposal to transition towards a decentralized indexing system stems from a need to strengthen security, boost operational efficiency, eliminate reliance on single entities, and foster organic growth within the ecosystem.

## Specification

The implementation of the decentralized indexing mechanism will utilize the XCHS indexer, which is structured in the form of a blockchain, and we call it Inscription Chain. Dependence on Chia Network as the mainchain, consensus, security, and final confirmation will be provided by mainchain to the Inscription Chain. The XCHS indexer will act like Layer 2, but with a unique features that Chia is difficult to provide. Unlike typical Layer 2 implementation, all transactions are directly submitted to the mainchain instead of being aggregated by Layer 2. With this model, sometimes referred to as Layer 1.5, offers heightened security superior to Layer 2, and flexibility superior to Layer 1.

The Inscription Chain will incorporate an account model as its intrinsic ledger model. Such an implementation offers Chia a unique bolstering effect, laying the groundwork for versatile and feature-rich smart contracts.

![](./xsip-2-chain.drawio.svg)

From a technical view, the Inscription Chain will utilize Chia's Reward Chain to generate blocks. Each block is structured according to the following table:

| Field               | Data Type | Description                                                                             |
| ------------------- | --------- | --------------------------------------------------------------------------------------- |
| Version             | UInt16    | Version information pertaining to the block generation rules.                           |
| PrevBlockHash       | UInt256   | Hash of the previous block in Inscription Chain                                         |
| InfusionBlockHash   | UInt256   | Reference to the hash of the Chia reward chain block hash.                              |
| InfusionBlockHeight | UInt64    | Indication of the height of the Chia reward chain from the genesis block.               |
| WorldStateRoot      | UInt256   | Hash representing the state of the blockchain after applying transactions in the block. |
| TransactionRoot     | UInt256   | Root hash of the tree containing all transactions included in the block.                |
| CoinRoot            | UInt256   | Root hash of the tree containing all spent coins included in the block.                 |

- WorldStateRoot: Patricia Merkle Tree (hex tree) Root with SHA256 Hash
- TransactionRoot: Merkle Tree (binary tree) Root with SHA256 Hash
- CoinRoot: Merkle Tree (binary tree) Root with SHA256 Hash

## Rationale

Various models for indexing are currently being utilized - centralized and open-sourced, multiple central providers with cross-verification. The inherent issues tied to these prior solutions necessitate a shift towards a truly decentralized indexing model. This model ensures data consistency and security, agility in protocol upgrades, and eases the indexing setup for ecosystem developers. Furthermore, this deters potential collusion among a few indexers. These considerations guide the design and adoption of a comprehensive decentralized indexing system.

In considering the techniques to implement decentralized indexing, inspiration comes from the inherent breakthrough that blockchain technology has offered. Constructing a sidechain could lay the groundwork for achieving decentralized indexing in a secure and expedient manner. This approach would allow the inscription data to be auditable and even reach consensus within the decentralized network, ultimately providing final confirmation ability. This notable feature leans into the primary advantage that blockchain provides — transparency and auditability, thereby heightening trust in the overall system.

## Security Considerations

Adopting a decentralized indexing system improves security considerations in the following ways:

1. It dispels the potential for concentrated collusion that can jeopardize data integrity.
2. It encourages diverse participation, thereby diluting the risk pool.
3. It's equipped with a standardized and open-source code that makes for straightforward checks and calibration, and low chance of bugs and vulnerabilities.

However, transitioning to this new model should be undertaken with care, ensuring meticulous testing and verification and observing potential unforeseen threats and risks. Any implementation must maintain a strong focus on preserving data security in all stages of the indexing process.
