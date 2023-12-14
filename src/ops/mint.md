# Mint

If you're using an inscription service, be cautious. Some tools might inscribe the token to their own address first, then forward it to you, the customer. This means that the balance initially lands with the inscription service's address.

```js
{
  'p': 'xchs',
  'op': 'mint',
  'tick': 'xchs',
  'amt': '1000'
}
```

| Key  | Required? | Description                                                     |
| ---- | --------- | --------------------------------------------------------------- |
| p    | Yes       | Protocol: Helps other systems identify and process XCHS events. |
| op   | Yes       | Operation: Type of event (Deploy, Mint, Transfer).              |
| tick | Yes       | Ticker: 4 letter identifier of the XCHS.                        |
| amt  | Yes       | Amount to mint: Amount of the XCHS to mint. \*                  |

\*Amount: Has to be less than 'lim' if stated during the deployment.
