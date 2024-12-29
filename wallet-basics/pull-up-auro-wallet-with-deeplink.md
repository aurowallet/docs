---
description: >-
  This document describes how to use a deep link to open the Auro Mobile Wallet
  and launch a zkApp within the App. This feature is supported starting from
  Auro Mobile Wallet version 2.1.0.
---

# ​Pull Up Auro Wallet with DeepLink

## **Pull Up the wallet to** launch **zkApp**

```javascript
let targetURL = ""; // Required, the target URL, e.g., https://www.aurowallet.com/
let paramsURL = encodeURIComponent(targetURL);

let targetNetworkId = ""; // Optional, the target network ID, e.g., mina:mainnet. You can retrieve this from the daemon node. If not provided, the App will use its current network by default.
let networkId = encodeURIComponent(targetNetworkId);

const endURL = `https://aurowallet.com/applinks?action=openurl&networkid=${networkId}&url=${paramsURL}`;
window.location.href = endURL;

```

Currently, there are 3 parameters supported:

*   **`action`** (Required)

    The action that the App will excute. Currently, only `openurl` is supported.
*   **`networkid`** (Optional)

    The ID of the target network. You can get this value from a GraphQL endpoint. If supported, the App will switch to the target network. If not supported, no changes will be made. If not set, the App will default to its current network.

```graphql
## Example GraphQL query:
query myQuery {
    networkID
}
```

*   **`url`** (Required)

    The URL the App will open. It is recommended to include this at the end of the deep link URL.

{% hint style="info" %}
**Note**: This method is limited to pulling up the Auro Wallet via the mobile phone's system browser.
{% endhint %}
