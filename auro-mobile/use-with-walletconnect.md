---
description: >-
  Auro Mobile supports WalletConnect, allowing seamless integration of zkApp
  with Auro Mobile with QR code scanning or deep linking.
---

# Use with WalletConnect

{% hint style="info" %}
The Auro Wallet in-app browser does not support building zkApps (due to [SharedArrayBuffer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/SharedArrayBuffer) limitations). Therefore, you need to build the zkApp in the Chrome mobile browser on Android and interact with Auro Wallet via deeplink.\
\
This feature is available in **Auro Mobile v2.1.2 or later**. Please update to the latest version to use this feature.
{% endhint %}

## Step

1. Get projectId from [Reown](https://cloud.reown.com/).
2. Init client.

```ts
const client = await SignClient.init({
  projectId: process.env.NEXT_PUBLIC_WALLET_CONNECT_PROJECY_ID,
  metadata: {
    name: "Auro Wallet Demo",
    description: "A Mina Protocol dApp with WalletConnect",
    url: window.location.origin,
    icons: ["https://www.aurowallet.com/imgs/auro.png"],
  },
  logger: "warn",
});
```

3. Request connect wallet.

```ts
const connectParams = {
  requiredNamespaces: {
    mina: {
      chains: ["mina:mainnet", "mina:devnet", "zeko:testnet"], // Chains currently supported by the zkApp, requiring Auro Wallet support.
      methods: [
        // The current zkApp requires the following methods, consistent with other methods supported by Auro Wallet. 
        // The supported methods are listed below:
        // List only the required methods:
        "mina_sendPayment",
        "mina_sendStakeDelegation",
        "mina_sendTransaction",
        "mina_signMessage",
        "mina_sign_JsonMessage",
        "mina_signFields",
        "mina_createNullifier",
        "mina_verifyMessage",
        "mina_verify_JsonMessage",
        "mina_verifyFields",
        "wallet_info",
      ],
      events: ["accountsChanged", "chainChanged"],
    },
  },
};
```

4. Set Up Event Listener (Optional).\
   If the app requires authorization or signing, you can configure it to trigger the app for operations upon a successful callback, or prompt the user in the zkApp to manually switch to Auro Wallet.

```ts
client.on("session_request_sent", (event: any) => {
  console.log("Session request sent:", event);
  if (
    [
      "mina_sendPayment",
      "mina_sendStakeDelegation",
      "mina_sendTransaction",
      "mina_signMessage",
      "mina_sign_JsonMessage",
      "mina_signFields",
      "mina_createNullifier",
    ].includes(event?.request?.method)
  ) {
    const deepLink = `aurowallet://`;
    console.log("Auro Wallet Deep Link for request:", deepLink);
    const isMobile = /iPhone|iPad|iPod|Android/i.test(navigator.userAgent);
    if (isMobile) {
      openDeepLink(deepLink);
    }
  }
});
```

5. UI Interaction.

```ts
const handleSendZkTransaction = async () => {
  if (!client || !session || !account) {
    setError("Please connect wallet first");
    return;
  }
  const zkTransaction = await getZkBuildBody(selectedChain, account);
  const zkRequest = {
    topic: session.topic,
    chainId: selectedChain,
    request: {
      method: "mina_sendTransaction",
      params: {
        // Optional: Specifies the current browser's scheme. 
        // If set, the app automatically returns to the provided scheme's browser; 
        // otherwise, the app only displays a pop-up prompting the user to return.
        scheme: chromeScheme, 
        from: account,
        transaction: zkTransaction,
        feePayer: {
          fee: "0.01", // Optional
          memo: "test zkApp", // Optional
        },
      },
    },
  };
  const result = await client.request(zkRequest);
};
```

#### Reference Links

**Test Website**\
[Visit Test Website](https://test-zkapp.aurowallet.com/wallet-connect)

**Core Code Examples**

* [UI Code](https://github.com/aurowallet/test-zkapp/blob/master/ui/src/pages/wallet-connect.page.tsx)
* [Initialization Code](https://github.com/aurowallet/test-zkapp/blob/master/ui/src/utils/walletConnect.ts)

**WalletConnect Integration Documentation**

* [WalletConnect Sign Client](https://docs.reown.com/advanced/api/sign/overview)
* [Reown AppKit](https://docs.reown.com/appkit-overview)
