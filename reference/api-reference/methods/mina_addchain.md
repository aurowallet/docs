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
    // the graphql URL that need add.
    readonly url: string
    // custom name.
    readonly name: string
}
```

### Result

```typescript
type ChainInfoArgs ={
    // current chain ID, current support four types: mainnet, devnet, berkeley, testworld2.
    chainId:string,
    // current chain name.
    name:string,
}

interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body. 
}

Promise<ChainInfoArgs | ProviderError>
```

### Errors

|       |                                            |                                                    |
| ----- | ------------------------------------------ | -------------------------------------------------- |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account.                     |
| 1002  | The request was rejected by the user.      |                                                    |
| 20003 | The parameters were invalid.               | Please check graphql-url and name.                 |
| 20004 | Not support chain.                         | Please use support chain.                          |
| 20005 | Request already pending. Please wait.      | Chain action current support one at the same time. |
| 23001 | Origin dismatch                            | Check origin safe.                                 |

## Example

### Request

```typescript
const addInfo = {
    url: encodeURIComponent("graphQLUrl"),
    name: "networkName",
}

await window.mina?.addChain(addInfo).catch((err: any) => err);
```

### Result

```typescript
// successful result.
{
  "chainId": "mainnet",
  "name": "testchain"
}

// user reject.
{
  "code": 1002,
  "message": "User rejected the request. "
}

// params check error. there check graphql-URL.
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
