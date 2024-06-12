---
description: Scenarios for interact chain with Auro Wallet.
---

# Add or Switch Chain

## RequestNetwork

During initialization, zkApp can get current networkID by call `requestNetwork`.

```typescript
const network: ChainInfoArgs = await window.mina?.requestNetwork()
  .catch((err: any) => err);
```

## `SwitchChain`

zkApp can switch chain by this method.&#x20;

The following are the networkID that Auro supports by default. If you want to use other networkID, need to add network first, then use the target networkID as a parameter to switch.

> Current support these networkID (default):
>
> * mina:mainnet
> * mina:testnet
> * mina:berkeley

```typescript
type ChainInfoArgs = {
    networkID: string;
};

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

const switchResult:ChainInfoArgs|ProviderError = await window.mina
    ?.switchChain({
        networkID: networkID.trim(),
    }).catch((err: any) => err);
```

{% hint style="danger" %}
```markdown
** Please update as soon as possible. **
`ChainInfoArgs` params have updated from App 2.0.2 & extension 2.2.17.
Only `networkID` is returned, no longer supports returning `chainId` and `name`. 

// @deprecated from App 2.0.2 & extension 2.2.17.
type ChainInfoArgs ={ 
    chainId:string,
    name:string
}
```
{% endhint %}

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
