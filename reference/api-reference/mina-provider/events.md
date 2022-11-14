# Events

### accountsChanged

accountsChanged wiil be triggered when user switch connected account in auro wallet

```
window.mina.on('accountsChanged', handler: (accounts: string[]) => void);
```

```
window.mina.on('accountsChanged', handler: (accounts: string[]) => {
   console.log('connected accounts', accounts)
});

```
