---
description: >-
  Here are the monitoring events of the provider. There are currently two types
  of events, account update and chain update.
---

# Events

### **accountsChanged**

When user switch account in Auro Wallet, `accountsChanged` will be trigger.

```javascript
window.mina?.on('accountsChanged', handler: (accounts: string[]) => void);
```

```javascript
window.mina?.on('accountsChanged', handler: (accounts: string[]) => {
   console.log('connected accounts', accounts)
});
```

{% hint style="success" %}
**NOTE**\
When switching to an unconnected account, an empty array will be returned.
{% endhint %}

### **chainChanged**

When user switch chain in Auro Wallet, `chainChanged` will be trigger.&#x20;

```javascript
type ChainInfoArgs ={
  networkID:string
}

window.mina?.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => void);
```

```javascript
window.mina?.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => {
   console.log('current networkID', chainInfo.networkID)
});
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
