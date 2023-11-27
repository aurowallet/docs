---
description: >-
  This scenario mainly explains how the server-side verify the result of the
  signMessage.
---

# VerifyMessage in server-side

{% hint style="info" %}
The features is implemented through [mina-signer](https://www.npmjs.com/package/mina-signer).

**mina-signer** is the NodeJS SDK provided by **MinaProtocol** for sign, verify signatures, etc.
{% endhint %}

## Verify Message

1. Add **mina-signer** to `package.json`.

```json
"dependencies": {
    "mina-signer": "2.1.1"
}
```

2. Import and init **mina-signer**.

```typescript
var Client = require("mina-signer");

// type Network = 'mainnet' | 'testnet'
var signerClient = new Client({ network: "mainnet" });
```

{% hint style="info" %}
There are two types of initialization supported here. The main network type is **mainnet**, and the type of other network are **testnet**. [See original definition.](https://github.com/o1-labs/o1js/blob/main/src/mina-signer/src/TSTypes.ts#L12)
{% endhint %}

3. Implement code.

```javascript
const publicKey = 'B62qj6z7oseWTr37SQTn53mF8ebHn45cmSfRC58Sy52wG6KcaPZNWjw'

const verifyMessage = `Click "Sign" to sign in. No password needed!

  This request will not trigger a blockchain transaction or cost any gas fees.
  
  I accept the Auro Test zkApp Terms of Service: https://test-zkapp.aurowallet.com
  
  address: B62qj6z7oseWTr37SQTn53mF8ebHn45cmSfRC58Sy52wG6KcaPZNWjw
  iat: 1701069403643`;

const signature = {
    field: '25087624681052481871246375076085075176624243458008290192358519021588472251513',
    scalar: '17285357755862735391605884635523872951699156489623612197745807470058903167470'
}

const verifyBody = {
    data: verifyMessage, // Signature content that needs to be verified.
    publicKey: publicKey, // Public key that needs to be verified.
    signature: signature, // Signature results that need to be verified.
};

// When verifyResult is true, the verification is successful.
const verifyResult = signerClient.verifyMessage(verifyBody);
```

{% hint style="success" %}
This is an [example of server-side](https://github.com/aurowallet/mina-signer-verify-example) verification of signature. You can refer to the implementation or run it locally.
{% endhint %}
