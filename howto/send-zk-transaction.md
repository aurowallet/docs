---
description: This scenario is mainly used to create zk-contract or update zk-contracts.
---

# Send zk Transaction

## Update zk contract

This method is use to sign and broadcast zk transaction.

```typescript
type SendTransactionHash = {
  hash: string;
};

type SignedZkappCommand = {
  signedData: string; // results of JSON.stringify( signZkappCommand().data )
};

type SendZkTransactionResult = SendTransactionResult | SignedZkappCommand

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

interface SendTransactionArgs {
    readonly onlySign?: boolean; // auro-extension-wallet support from V2.2.16. 
    readonly nonce?: number; // auro-extension-wallet support from V2.3.0. 
    readonly transaction: string | object;
    readonly feePayer?: {
        readonly fee?: number;
        readonly memo?: string;
    };
}

const updateResult: SendZkTransactionResult| ProviderError= await window.mina?
    .sendTransaction({
      onlySign: onlySign, // only sign zkCommond, not broadcast.
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
