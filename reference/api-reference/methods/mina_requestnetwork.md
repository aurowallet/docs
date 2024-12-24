---
description: This method is used to request the chain info of the Auro wallet.
---

# mina\_requestNetwork

### Params

null

### Result

```typescript
type ChainInfoArgs ={
    // current networkID, now will return mina:mainnet, mina:devnet, zeko:testnet
    networkID:string
}

Promise<ChainInfoArgs>
```

{% hint style="danger" %}
```markdown
** Please update as soon as possible. **
`ChainInfoArgs` params have updated from App 2.0.2 & extension 2.2.17.
Only `networkID` is returned, no longer supports returning `chainId` and `name`. 

// @deprecated from App 2.0.2 & extension 2.2.17.
type ChainInfoArgs ={ 
    chainId:string,
    name:string
}
```
{% endhint %}

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
  "networkID": "mina:mainnet"
}
```
