---
description: This method is used to switch chain to the wallet by chainId
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

|        |                             |                                                |
| ------ | --------------------------- | ---------------------------------------------- |
| 4001   | user reject transaction     |                                                |
| -32602 | The parameters were invalid | may cause by address, amount,fee type dismatch |
| -32900 | Origin dismatch             |                                                |

## Example

### Request

```typescript

await window.mina?.switchChain({ chainId: "mainnet" }).catch((err: any) => err);

```

### Result

```
// success
{
  "chainId": "mainnet",
  "name": "testchain"
}

// user reject 
{
  "code": 4001,
  "message": "User rejected the request."
}
// params check error. there check :addres ,amount , fee
{
  "code": -32602,
  "message": "Invalid method parameter(s)."
}
```

