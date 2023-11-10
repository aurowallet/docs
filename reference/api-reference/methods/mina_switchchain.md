---
description: This method is used to switch chain of Auro Wallet by chainId.
---

# mina\_switchChain

### Params

```typescript
type SwitchChainArgs = {
    // target chain id. current support four types: mainnet , devnet , berkeley , testworld2 , 
    readonly chainId: string
}
```

### Result

```typescript
type ChainInfoArgs ={
    // current chain id , current support four types: mainnet , devnet , berkeley , testworld2 , 
    chainId:string,
    // current chain name
    name:string,
}

interface ProviderError extends Error {
    message: string; // error message
    code: number; // error code 
    data?: unknown;// error body 
}

Promise<ChainInfoArgs | ProviderError>
```

### Errors

|       |                                       |                                                    |
| ----- | ------------------------------------- | -------------------------------------------------- |
| 1002  | The request was rejected by the user. |                                                    |
| 20005 | Request already pending. Please wait. | Chain action current support one at the same time. |
| 23001 | Origin dismatch.                      | Check origin safe.                                 |

## Example

### Request

```typescript
await window.mina?.switchChain({ chainId: "mainnet" }).catch((err: any) => err);
```

### Result

```typescript
// success
{
  "chainId": "mainnet",
  "name": "testchain"
}

// user reject 
{
  "code": 1002,
  "message": "User rejected the request."
}

// have pending chain action
{
  "code": 20005,
  "message": "Request already pending. Please wait."
}
```
