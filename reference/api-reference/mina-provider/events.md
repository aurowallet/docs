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


chainChanged will be triggered when user switch chainType in Auro Wallet.

```javascript
window.mina.on('chainChanged', handler: (chainType: string) => void);
```

```javascript
window.mina.on('chainChanged', handler: (chainType: string) => {
   console.log('current chain', chainType)
});
```
