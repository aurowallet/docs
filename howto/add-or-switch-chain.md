---
description: Scenarios for interact chain with Auro Wallet.
---

# Add or Switch Chain

## RequestNetwork

During initialization, zkApp can get current chainId and chain name by call `requestNetwork`.

```typescript
const network: ChainInfoArgs = await window.mina?.requestNetwork()
  .catch((err: any) => err);
```

## `SwitchChain`

zkApp can switch chain by this method.

{% hint style="success" %}
current only support these chain Id:

* mainnet
* devnet
* berkeley
* testworld2
{% endhint %}

```typescript
type ChainInfoArgs = {
    chainId: string;
    name: string;
};

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

const switchResult:ChainInfoArgs|ProviderError = await window.mina
    ?.switchChain({
        chainId: chainId.trim(),
    }).catch((err: any) => err);
```

## Add Chain

If want to custom the adding chain or switch chain, can use this method. When the URL has been added, it will request to switch to chain corresponding to the URL.

```typescript
const addInfo = {
  url: encodeURIComponent("graphQLURL"),
  name: "networkName",
}

const addResult:ChainInfoArgs|ProviderError = await window.mina?.addChain(addInfo)
  .catch((err: any) => err);
```

## Chain Event

This method is used to listen chain changes. When the Auro Wallet chain change, the event will be trigger.

```typescript
window.mina?.on("chainChanged",(chainInfo: ChainInfoArgs) => {
  console.log(chainInfo);
});
```
