# How It Works

- Only standard XCH addresses are valid receiving addresses. If you send to other types of addresses, they will not be recognized and will ultimately lead to losses.
- XCHS may not be compatible with current trading infrastructure, please use with caution.
- Although XCH is also based on the UTXO model like Bitcoin, there are some differences in detail. I won't go into detail here, but please note that the working methods with BRC-20 will be somewhat different.
- XCHS does not need to specially `mint` a one-time-use transfer inscription like in BRC-20, you can directly send fund with an inscription to the target address.
- Only the first deployed ticker is effective, subsequent tickers with the same name will be ignored. Note that tickers are case insensitive, but you can write in your preferred style when deploying. The indexer can display this original name as needed.
- If by chance two `deploy` inscriptions appear in the same block, the first one will be taken as effective.
- The validity of `mint` is determined in the same way as deployment, first come first served.
- Only `mint` and `transfer` will change the balance, while Deploy will not.
- The user who exceeds the maximum value at the first `mint` can get the remaining amount. Any `mint` that exceeds the maximum value afterwards will be invalid.
- XCHS can be completely independent of XCH, that is, an account may not have any XCH but have a balance of XCHS. Furthermore, in wallets that support gasless, you can directly pay gas with XCHS to complete transactions.
- The maximum supply should not exceed the maximum value: 9007199254740991
- When `transfer` your token in XCHS protocol, be sure to inscibe in the coin with correct sender address. Some wallet client might not properly select the correct coin. Nevertheless, even if the wrong sender address is used, your funds will not be lost; but the operation might be ineffective.