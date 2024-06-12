---
description: This method is used to switch chain of Auro Wallet by chainId.
---

# mina\_switchChain

### Params

```typescript
type SwitchChainArgs = {
    // Target networkID. now will return mina:mainnet, mina:testnet, mina:berkeley
    readonly networkID: string
}
```

### Result

```typescript
type ChainInfoArgs ={
    // current networkID, now will return mina:mainnet, mina:testnet, mina:berkeley
    networkID:string
}

interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body. 
}

Promise<ChainInfoArgs | ProviderError>
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

|       |                                       |                                                    |
| ----- | ------------------------------------- | -------------------------------------------------- |
| 1002  | The request was rejected by the user. |                                                    |
| 20005 | Request already pending. Please wait. | Chain action current support one at the same time. |
| 23001 | Origin dismatch.                      | Check origin safe.                                 |

## Example

### Request

```typescript
await window.mina?.switchChain({ networkID: "mina:mainnet" }).catch((err: any) => err);
```

### Result

```typescript
// successful result.
{
  "networkID": "mina:mainnet"
}

// user reject.
{
  "code": 1002,
  "message": "User rejected the request."
}

// have pending chain action.
{
  "code": 20005,
  "message": "Request already pending. Please wait."
}
```
