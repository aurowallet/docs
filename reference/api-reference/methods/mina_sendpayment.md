---
description: >-
  This method is used to call  Auro Wallet send payment (current support send
  MINA ) by zkApp.
---

# mina\_sendPayment

### Params

```typescript
interface SendPaymentArgs  {
    // to is the target address. require base58 address. 
    readonly to: string
    // amount is the send amount, with decimal. e.g. 1.1
    readonly amount: number
    // option. Auro Wallet also provide advance option to change fee.
    readonly fee?: number
    // option.
    readonly memo?:string
}
```

### Result

<pre class="language-typescript"><code class="lang-typescript"><strong>type SendTransactionResult = {
</strong>    // broadcast hash, you can query tx info by this hash.
    hash: string
}

interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body. 
}

Promise&#x3C;SendTransactionResult | ProviderError>
</code></pre>

### Errors

|       |                                            |                                    |
| ----- | ------------------------------------------ | ---------------------------------- |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account.     |
| 1002  | The request was rejected by the user.      |                                    |
| 20003 | The parameters were invalid.               | Please check address, amount, fee. |
| 23001 | Origin dismatch.                           | Check origin safe.                 |

## Example

### Request

```typescript
const amount = 0.1;
const receiveAddress = "B62qpjxUpgdjzwQfd8q2gzxi99wN7SCgmofpvw27MBkfNHfHoY2VH32"
const fee = 0.012
const memo = "Auro Wallet"

await window.mina?.sendPayment({
        amount: amount,
        to: receiveAddress,
        fee: fee,
        memo: memo,
    }).catch((err: any) => err);
```

### Result

```typescript
// successful result.
{
  "hash": "CkpZj7QwDkfzoyPfMiJj9zTC6R41Sbh9fY4yvKsSYM9zjyyTUDwW9"
}

// user reject.
{
  "code": 1002,
  "message": "User rejected the request."
}

// can not get connect address.
{
  "code": 1001,
  "message": "User disconnect, please connect first."
}

// params check error. there check addres, amount and fee.
{
  "code": 20003,
  "message": "Invalid method parameter(s)."
}
```
