---
description: This method is used by zkApp to call Auro Wallet stake delegation.
---

# mina\_sendStakeDelegation

### Params

```typescript
type SendStakeDelegationArgs  = {
    // to is the target block Producer address. require base58 address.
    readonly to: string,
    // option. custom fee. Auro Wallet also provide advance to change fee
    readonly fee?: number,
    // option. custome memo. 
    readonly memo?:string
}

```

### Result

```typescript
type SendTransactionResult = {
    // sendPayment hash , you can query tx info by this hash
    hash: string
}

interface ProviderError extends Error {
    message: string; // error message
    code: number; // error code 
    data?: unknown;// error body 
}

Promise<SendTransactionResult | ProviderError>
```

### Errors

|       |                                            |                                |
| ----- | ------------------------------------------ | ------------------------------ |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account. |
| 1002  | user reject transaction.                   |                                |
| 20003 | The parameters were invalid.               | Please check address, fee.     |
| 23001 | Origin dismatch.                           | Check origin safe.             |

## Example

### Request

```typescript
const vaildatorAddress = "B62qq3TQ8AP7MFYPVtMx5tZGF3kWLJukfwG1A1RGvaBW1jfTPTkDBW6"
const fee = 0.011
const memo = ""

await window.mina?.sendStakeDelegation({
    to: vaildatorAddress,
    fee: fee,    // option, if not use ,can delet this params
    memo: memo,    // option, if not use ,can delet this params
}).catch((err: any) => err);
```

### Result

```typescript
// successful result
{
  "hash": "CkpYTcQv2obKrD78X7QoHF9j3CfmQWNjNb8UFeDaCVRjcGZpUdxUz"
}

// user reject 
{
  "code": 1002,
  "message": "User rejected the request."
}
// can not get connect address
{
  "code": 1001,
  "message": "User disconnect, please connect first"
}
// params check error. there check :addres ,amount , fee
{
  "code": 20003,
  "message": "Invalid method parameter(s)."
}
```
