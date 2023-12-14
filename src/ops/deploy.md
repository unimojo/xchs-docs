# Deploy

In our documentation, we've chosen to use $PAWS as our example token. This is purely for demonstration purposes. However, the principles apply just the same to your chosen token. Just replace $PAWS with your token's name and you're good to go!

```js
{
  'p': 'xchs',
  'op': 'deploy',
  'tick': 'xchs',
  'max': '21000000',
  'lim': '1000'
}
```

| Key  | Required? | Description                                                      |
| ---- | --------- | ---------------------------------------------------------------- |
| p    | Yes       | Protocol: Helps other systems identify and process XCHS events.  |
| op   | Yes       | Operation: Type of event (Deploy, Mint, Transfer).               |
| tick | Yes       | Ticker: 4 letter identifier of the XCHS.                         |
| max  | Yes       | Max supply: set max supply of the XCHS.                          |
| lim  | No        | Mint limit: If letting users mint to themsleves, limit per mint. |
