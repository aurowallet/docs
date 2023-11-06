---
description: This method is used to add a custom chain to the wallet
---

# mina\_addChain

###

{% hint style="success" %}
if you want to switch by url , you can use this method . if url is added to wallet , will call switch\_chain auto.
{% endhint %}

### Params

```typescript
type AddChainArgs = {
  // the graphql url that need add 
  readonly url: string
  // custome name 
  readonly name: string
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

|        |                                       |                                                |
| ------ | ------------------------------------- | ---------------------------------------------- |
| 4001   | user reject transaction               |                                                |
| 4300   | User disconnect, please connect first |                                                |
| -32602 | The parameters were invalid           | may cause by address, amount,fee type dismatch |
| -32006 | Not support chain                     |                                                |
| -32900 | Origin dismatch                       |                                                |

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
