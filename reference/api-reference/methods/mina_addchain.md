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

|       |                                       |                                                |
| ----- | ------------------------------------- | ---------------------------------------------- |
| 1002  | user reject transaction               |                                                |
| 1001  | User disconnect, please connect first |                                                |
| 20003 | The parameters were invalid           | may cause by address, amount,fee type dismatch |
| 20004 | Not support chain                     |                                                |
| 20005 | Request already pending. Please wait. | chain action now support one at the same time. |
| 23001 | Origin dismatch                       |                                                |

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
  "code": 1002,
  "message": "User rejected the request."
}
// params check error. there check :addres ,amount , fee
{
  "code": 20003,
  "message": "Invalid method parameter(s)."
}
// have pending chain action
{
  "code": 20005,
  "message": "Request already pending. Please wait."
}
```
