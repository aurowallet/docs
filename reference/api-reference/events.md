---
description: >-
  Here are the monitoring events of the provider. There are currently two types
  of events, account update and chain update.
---

# Events

### **accountsChanged**

accountsChanged will be triggered when user switch connected account in Auro Wallet.

```javascript
window.mina.on('accountsChanged', handler: (accounts: string[]) => void);
```

```javascript
window.mina.on('accountsChanged', handler: (accounts: string[]) => {
   console.log('connected accounts', accounts)
});
```

### **chainChanged**

chainChanged will be triggered when user switch chainId in Auro Wallet.

```javascript

type ChainInfoArgs ={
  chainId:string,
  name:string,
}

window.mina.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => void);
```

```javascript
window.mina.on('chainChanged', handler: (chainInfo: ChainInfoArgs) => {
   console.log('current chain id', chainInfo.chainId)
   console.log('current chain name', chainInfo.name)
});
```
