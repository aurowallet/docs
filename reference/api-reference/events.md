---
description: >-
  Here are the monitoring events of the provider. There are currently two types
  of events, account update and chain update.
---

# Events

### **accountsChanged**

When user switch account in Auro Wallet, `accountsChanged` will be triggered.

```javascript
window.mina?.on('accountsChanged', handler: (accounts: string[]) => void);
```

```javascript
window.mina?.on('accountsChanged', handler: (accounts: string[]) => {
   console.log('connected accounts', accounts)
});
```

### **chainChanged**

When user switch chain in Auro Wallet, `chainChanged` will be triggered.&#x20;

```javascript
type ChainInfoArgs ={
  chainId:string,
  name:string,
}

window.mina?.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => void);
```

```javascript
window.mina?.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => {
   console.log('current chain id', chainInfo.chainId)
   console.log('current chain name', chainInfo.name)
});
```
