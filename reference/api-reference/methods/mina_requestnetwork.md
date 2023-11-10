---
description: This method is used to request the chain info of the Auro wallet.
---

# mina\_requestNetwork

### Params

null

### Result

```typescript
type ChainInfoArgs ={
    // current chain id, now will return mainnet, devnet, berkeley, testworld2.
    chainId:string,
    // current chain name. The default node name is fixed, 
    // and the custom added ones are user-defined.
    name:string,
}

Promise<ChainInfoArgs>
```

### Errors

null

## Example

### Request

```typescript
await window.mina?.requestNetwork().catch((err: any) => err);
```

### Result

```typescript
{
  "chainId": "mainnet",
  "name": "Mainnet"
}
```
