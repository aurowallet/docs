---
description: Scenarios for interact chain with wallets.
---

# Add or Switch Chain

## RequestNetwork

During initialization, zkApp can get current chainId and chain name by call `requestNetwork`

```typescript
const network: ChainInfoArgs = await window.mina?.requestNetwork()
  .catch((err: any) => err);
```

## `SwitchChain`

zkApp can switch chain throw `switchChain`&#x20;

{% hint style="success" %}
current only support these chain Id:&#x20;

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
      })
      .catch((err: any) => err);
```

## Add Chain

If want to customize the adding chain or switch chain, can use this method. When the url has been added, it will request to switch to chain corresponding to the url.

```typescript

const addInfo = {
  url: encodeURIComponent("graphQLUrl"),
  name: "networkName",
}
const addResult:ChainInfoArgs|ProviderError = await window.mina?.addChain(addInfo)
  .catch((err: any) => err);
```

## Chain Event

This method is used to monitor chain changes. When the wallet chain changes, the monitoring will be triggered.

```typescript
window.mina?.on("chainChanged",(chainInfo: ChainInfoArgs) => {
  console.log(chainInfo);
});
```
