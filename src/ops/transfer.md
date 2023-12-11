# Transfer

Attention, some wallet implementation generate a different address each time. Make sure to send to the address that holds the balance.

```js
{
  'p': 'xchs',
  'op': 'transfer',
  'tick': 'paws',
  'amt': '100'
}
```

| Key  | Required? | Description                                                     |
| ---- | --------- | --------------------------------------------------------------- |
| p    | Yes       | Protocol: Helps other systems identify and process XCHS events. |
| op   | Yes       | Operation: Type of event (Deploy, Mint, Transfer).              |
| tick | Yes       | Ticker: 4 letter identifier of the XCHS.                        |
| amt  | Yes       | Amount to transfer: amount of the XCHS to transfer. \*          |

\*Amount: if the amount is exceeding account balance, then this transfer is invalid.
