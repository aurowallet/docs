---
description: >-
  This scenario is mainly used to handle common methods, such as send payment
  and stake delegation.
---

# Send Transaction

## Send Payment

This method is used to send MINA.

```typescript
// success data
type SendTransactionResult = {
    hash: string;
};
// failed data
interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

let data: SendTransactionResult|ProviderError = await window.mina
    ?.sendPayment({
        amount: amount,
        to: receiveAddress,
        fee: fee, // option
        memo: memo, // option
    })
    .catch((err: any) => err);
```

## Stake Delegation

This method is used to call stake delegation.

```typescript
let data: SendTransactionResult|ProviderError = await window.mina
    ?.sendStakeDelegation({
        to: vaildatorAddress,
        fee: fee, // option
        memo: memo, // option
    }).catch((err: any) => err);
```
