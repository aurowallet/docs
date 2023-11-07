---
description: >-
  This method is used by zkApp to call wallet sendPayment.(current supports main
  coin send.)
---

# mina\_sendPayment

### Params

```typescript
interface SendLegacyPaymentArgs  {
  // to is the target address. require base58 address. 
  readonly to: string
  // amount is the send amount , with decimal. like 1.1 MINA
  readonly amount: number
  // option. custom fee. auro also provide advance to change fee
  readonly fee?: number
  // option. custome memo. 
  readonly memo?:string
}

```

### Result

<pre class="language-typescript"><code class="lang-typescript"><strong>type BroadcastTransactionResult = {
</strong>  // sendPayment hash , you can query tx info by this hash
  hash: string
}

interface ProviderError extends Error {
  message: string; // error message
  code: number; // error code 
  data?: unknown;// error body 
}

Promise&#x3C;BroadcastTransactionResult | ProviderError>
</code></pre>

### Errors

|        |                                     |                                                |
| ------ | ----------------------------------- | ---------------------------------------------- |
| 1002   | user reject transaction             |                                                |
| 1001   | User disconnect, need connect first | can not get connected account                  |
| 20003 | The parameters were invalid         | may cause by address, amount,fee type dismatch |
| 23001 | Origin dismatch                     |                                                |

## Example

### Request

```typescript
const amount = 0.1;
const receiveAddress = "B62qpjxUpgdjzwQfd8q2gzxi99wN7SCgmofpvw27MBkfNHfHoY2VH32"
const fee = 0.012
const memo = "auro wallet"

await window.mina?.sendLegacyPayment({
        amount: amount,
        to: receiveAddress,
        fee: fee,
        memo: memo,
      })
      .catch((err: any) => err);
```

### Result

```typescript
// successful result
{
  "hash": "CkpZj7QwDkfzoyPfMiJj9zTC6R41Sbh9fY4yvKsSYM9zjyyTUDwW9"
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
