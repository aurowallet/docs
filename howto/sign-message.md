---
description: >-
  This scenario is mainly used to sign information. that can be used for login
  verification.
---

# Sign Message

## Sign Message

This method is used for sign message.

```typescript
interface SignedData {
    publicKey: string;
    data: string;
    signature: {
        field: string;
        scalar: string;
    };
}

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}
type SignMessageArgs = {
    message:string
}

const content = `Click "Sign" to sign in. No password needed!

This request will not trigger a blockchain transaction or cost any gas fees.

I accept the Auro Test zkApp Terms of Service: ${window.location.href}

address: ${currentAccount}
iat: ${new Date().getTime()}`;

const signContent:SignMessageArgs = {
    message:content
}

const signResult: SignedData|ProviderError = await window.mina?
     .signMessage(signContent)
     .catch((err: any) => err);

console.log(signResult)
```

## Sign Json Message

This method is used for sign JSON data , Auro Wallet will format message.

```typescript
type JsonMessageData  = {
    label:string
    value:string
}

type SignJsonMessageArgs = {
    readonly message: Array<JsonMessageData>
}

const msgParams = [
    { label: "Label:", value: "Sign Confirm" },
    {
      label: "Message:",
      value: "Click to sign in and accept the Terms of Service",
    },
    {
      label: "URI:",
      value: window.location.href,
    },
    {
      label: "networkID:",
      value: network.networkID,
    },
    {
      label: "Chain Name:",
      value: network.name,
    },
    {
      label: "Issued At:",
      value: new Date().getTime(),
    },
    {
      label: "Resources:",
      value: "https://docs.aurowallet.com/",
    },
    ];
  
const signResult:SignedData|ProviderError = await window.mina
    ?.signJsonMessage({
        message: msgParams
    })
    .catch((err: any) => err);

console.log(signResult);
```

## Verify Message

This methods is used for verify signed Message.

```typescript
let verifyResult:boolean|ProviderError = await window.mina
    ?.verifyMessage(verifyMessageBody)
    .catch((err: any) => err);
  
console.log(verifyResult); // If the result is successful, it will return true.
```
