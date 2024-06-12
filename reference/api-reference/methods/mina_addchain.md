---
description: This method is used to add a custom chain to Auro Wallet.
---

# mina\_addChain

{% hint style="success" %}
if you want to switch by URL , you can use this method . if URL is added to wallet , will call switch\_chain auto.
{% endhint %}

### Params

```typescript
type AddChainArgs = {
    // the GraphQL URL that need add.
    readonly url: string
    // custom name.
    readonly name: string
}
```

### Result

```typescript
type ChainInfoArgs ={
    // current networkID, now will return mina:mainnet, mina:testnet, mina:berkeley
    networkID:string,
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

|       |                                            |                                                    |
| ----- | ------------------------------------------ | -------------------------------------------------- |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account.                     |
| 1002  | The request was rejected by the user.      |                                                    |
| 20003 | The parameters were invalid.               | Please check GraphQL URL and name.                 |
| 20004 | Not support chain.                         | Please use support chain.                          |
| 20005 | Request already pending. Please wait.      | Chain action current support one at the same time. |
| 23001 | Origin dismatch                            | Check origin safe.                                 |

## Example

### Request

```typescript
const addInfo = {
    url: encodeURIComponent("GraphQL URL"),
    name: "networkName",
}

await window.mina?.addChain(addInfo).catch((err: any) => err);
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
  "message": "User rejected the request. "
}

// params check error. there check GraphQL URL.
{
  "code": 20003,
  "message": "Invalid method parameter(s). "
}

// have pending chain action.
{
  "code": 20005,
  "message": "Request already pending. Please wait. "
}
```

