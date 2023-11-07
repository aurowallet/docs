---
description: >-
  This scenario is mainly used to update zk transactions, including create
  zk-contract and update zk-contracts.
---

# Send zk Transaction

## Update zk contract

this method main use sign zk commond.

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
      transaction: transactionJSON,// this is zk commond ,create by o1js
      feePayer: {//option
        fee: fee,
        memo: memo,
      },
    });

console.log(updateResult)
```

{% hint style="info" %}
Here is an demo of update a zk. Creating the contract requires zkapp to sign once using zk-account keys, and then the plug-in signs it twice. The [created demo is here](https://github.com/aurowallet/test-zkapp/blob/feature/zk/ui/src/components/HomeComponents/SignTransactionBox.tsx#L263)
{% endhint %}
