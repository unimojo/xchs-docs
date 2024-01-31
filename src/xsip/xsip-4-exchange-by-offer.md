# XSIP-4: Exchange by Offer

**WIP**

## Abstract

This proposal seeks to redefine and fine-tune XCHS with new primitives that enhance both security and operability for inscription trading.
This proposal integrates two existing mechanisms: the Offer mechanism from the Chia Network, which enables direct decentralized trading of assets, and the two-stage 'transfer' mechanism from BRC20.
However, it can lead to irrevocable financial loss if implemented incorrectly, especially when interacted with incompatible wallets.
To address these issues, we propose three primitives: 'Inscribe', 'Transmit', and 'Reclaim'.
'Inscribe' is to bind a certain amount of funds to a created UTXO coin from the sender's balance. Once inscribed, the funds can only be moved using this specific coin.
'Transmit' offers the exclusive method of transmitting inscribed funds out of UTXO.
If improper construction occurs, funds can only be reclaimed through a 'Reclaim' operation.
This XSIP aims to maximize Offer's potential, mitigate the risk of loss, and increase users' control over their funds by providing the ability to rectify mistakes and reclaim lost funds.

## Motivation

Offer is a unique feature provided by Chia, allowing direct asset trades with others in a decentralized manner. For instance, we can put forth an offer inviting someone to trade their Chia for our new token, which then can be accepted by any party.

When it comes to inscription trading within the context of offers, security is achieved by binding a specific amount of inscription tokens to one UTXO coin. In essence, the inscription token can be transferred only when the UTXO coin is spent. This design ethos is reminiscent of the BRC20 protocol. However, the BRC20 protocol reveals a significant shortcoming: if the spending is improperly constructed, such as by an incompatible wallet, the funds may be irretrievably lost.

Therefore, within this XSIP, we propose defining two primitives, reminiscent of BRC20's two-stage transfer. Importantly, we introduce an additional primitive to reclaim funds that may be lost due to incorrectly structured spent coins. In doing so, we aim to not just rectify existing issues but also to introduce new levels of flexibility and security to XCHS.

## Specification

Note: The fields `p`, `op`, `tick` will follow the definitions set by the base protocol and will not be further detailed herein.

### Inscribe

The 'Inscribe' operation entails allocating a specific amount of funds from the sender's balance to a created UTXO coin.
Following inscription, the fund amount will be relocated from a particular account to this UTXO coin, and subsequent operations to transmit these funds can only utilize this coin.

```js
{
  'p': 'xchs',
  'op': 'inscribe',
  'tick': 'xchs',
  'amt': '1000'
}
```

| Key | Required? | Description                                                       |
| --- | --------- | ----------------------------------------------------------------- |
| amt | Yes       | Amount to inscribe: Amount of the XCHS to inscribe to target coin |

### Transmit

'Transmit' signifies the exclusive method to extract funds from the inscribed UTXO coin.
If an inscription instruction is incorrectly constructed and the coin is spent, the `reclaim` operation stands as the sole avenue to retrieve your funds.

```js
{
  'p': 'xchs',
  'op': 'transmit',
  'tick': 'xchs'
}
```

### Reclaim

'Reclaim' operation aids in recovering your funds if the inscribed coin is spent without the correct inscription instruction.
Although this operation is heavy, it ensures the safety of your funds from unsophisticated wallet software execution.

```js
{
  'p': 'xchs',
  'op': 'reclaim',
  'tick': 'xchs',
  'coin': 'fca28aa50c89aaa5f7dc40b7f94e1635d070c9f83be52a2f2be0bf9bf8617285',
  'height': '4700101',
  'idx': '456',
  'path': [
    'e98be068d742b009af509f807d1b6a00a36b73a88aeb074ab40750eb66101aa0',
    '60c20d176b7901447a618e5269c69402a5b5d09e4a7ec7402ff568f2138ee46e',
    '60b9bcaca73d68f3288b9aeec079b165d744bc636e71caa1e8ea1003dbeeee6d',
    '02055edbd965f9d49fd95e1822249a9efdb6d9ff4c1e1c71d428656193577b77',
    '5857bd486c4bdcc437a73f77c2245db81da518197d4d0c2cc5f0965ad22c6635'
  ]
}
```

| Key    | Required? | Description                                                   |
| ------ | --------- | ------------------------------------------------------------- |
| coin   | Yes       | the coin which is spent and still hold inscribed funds        |
| height | Yes       | the block height where the spent coin is located              |
| idx    | Yes       | the index of the spent coin within the merkle tree            |
| path   | Yes       | the path to prove the coin's inclusion within the merkle tree |

## Rationale

### Transfer vs Inscribe

Within the BRC20 protocol, users are required to execute a 'transfer' twice.
Initially, they transfer to their account in preparation, followed by a genuine transfer to a specific recipient.
XCHS circumvents this double-transfer necessity by using the account model, but the downside is that peer-to-peer trading, like Offer mechanism, cannot exclusively guarantee successful trading.
Thus, the two-stage 'transfer' is still a requirement.
However, XCHS has endowed 'transfer' with the notion of a straightforward fund transfer, which is why we've designed this XSIP with a two-stage 'transfer', embodied in the `inscribe` and `transmit` operations.

## Security Considerations

### Offer

Offer is a mechanism provided by the Chia Network, designed to ensure a trade only occurs when both parties requirements are satisfied. To ensure this mechanism's seamless operation with XCHS, under the account model, we propose this XSIP to secure the inscription's binding to a specific coin.

### Funds loss

In BRC20, fund losses occasionally occur, especially when an incompatible wallet is handling these funds.
Users were expected to absorb these losses with no chance to reclaim them.
This vulnerability led to the design of the reclaim operation.
The reclaim operation equips users with a tool to address such situations and guard against unnecessary losses.