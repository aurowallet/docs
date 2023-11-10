---
description: This scenario is mainly used to create zk-contract or update zk-contracts.
---

# Send zk Transaction

## Update zk contract

This method is use to sign and broadcast zk transaction.

```typescript
type SendTransactionResult = {
    hash: string;
};

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

interface SendTransactionArgs {
    readonly transaction: any;
    readonly feePayer?: {
        readonly fee?: number;
        readonly memo?: string;
    };
}

const updateResult:SendTransactionResult| ProviderError= await window.mina?
    .sendTransaction({
      transaction: transactionJSON, // this is zk commond, create by zkApp.
      feePayer: { // option.
        fee: fee,
        memo: memo
      },
    });

console.log(updateResult);
```

{% hint style="info" %}
Here is an demo of update a zk contract. To create a zkApp contract, you need to use [o1js](https://www.npmjs.com/package/o1js) to sign first, then use Auro Wallet to sign the result of o1js signed. The created zkApp contract demo is [here](https://github.com/aurowallet/test-zkapp/blob/feature/zk/ui/src/components/HomeComponents/SignTransactionBox.tsx#L263).
{% endhint %}
