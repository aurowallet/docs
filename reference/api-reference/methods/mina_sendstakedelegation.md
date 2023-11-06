---
description: This method is used by zkApp to call wallet stake delegation
---

# mina\_sendStakeDelegation

### Params

```typescript
type SendLegacyStakeDelegationArgs  = {
  // to is the target block Producer address. require base58 address.
  readonly to: string,
  // option. custom fee. auro also provide advance to change fee
  readonly fee?: number,
  // option. custome memo. 
  readonly memo?:string
}

```

### Result

```typescript
type BroadcastTransactionResult = {
  // sendPayment hash , you can query tx info by this hash
  hash: string
}

interface ProviderError extends Error {
  message: string; // error message
  code: number; // error code 
  data?: unknown;// error body 
}

Promise<BroadcastTransactionResult | ProviderError>
```

### Errors

|        |                                     |                                                |
| ------ | ----------------------------------- | ---------------------------------------------- |
| 4001   | user reject transaction             |                                                |
| 4300   | User disconnect, need connect first | can not get connected account                  |
| -32602 | The parameters were invalid         | may cause by address, amount,fee type dismatch |
| -32900 | Origin dismatch                     |                                                |

## Example

### Request

```typescript
const vaildatorAddress = "B62qq3TQ8AP7MFYPVtMx5tZGF3kWLJukfwG1A1RGvaBW1jfTPTkDBW6"
const fee = 0.011
const memo = ""

await window.mina?.sendLegacyStakeDelegation({
    to: vaildatorAddress,
    fee: fee,
    memo: memo,// option , if not use ,can delet this params
})
.catch((err: any) => err);

```

### Result

```typescript
// successful result
{
  "hash": "CkpYTcQv2obKrD78X7QoHF9j3CfmQWNjNb8UFeDaCVRjcGZpUdxUz"
}

// user reject 
{
  "code": 4001,
  "message": "User rejected the request."
}
// can not get connect address
{
  "code": 4300,
  "message": "User disconnect, please connect first"
}
// params check error. there check :addres ,amount , fee
{
  "code": -32602,
  "message": "Invalid method parameter(s)."
}
```