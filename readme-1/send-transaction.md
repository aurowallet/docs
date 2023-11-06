---
description: >-
  This scenario is mainly used to handle common methods, such as send payment
  and delegation.
---

# Send Transaction

## Send Payment

this method is used to call send token.

```typescript
// success data
type BroadcastTransactionResult = {
    hash: string;
};
// failed data
interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

let data:BroadcastTransactionResult|ProviderError = await window.mina
      ?.sendLegacyPayment({
        amount: amount,
        to: receiveAddress,
        fee: fee,
        memo: memo,
      })
      .catch((err: any) => err);
```

## Stake Delegation

this method is used to call stake delegation.

```typescript
let data: BroadcastTransactionResult|ProviderError = await window.mina
    ?.sendLegacyStakeDelegation({
      to: vaildatorAddress,
      fee: fee,
      memo: memo,
    })
    .catch((err: any) => err);
```
