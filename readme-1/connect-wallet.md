---
description: Scenarios for connect wallets and request accounts.
---

# Connect Wallet

{% hint style="info" %}
When using the API, you need to ensure that the browser has successfully obtained the **`window.mina`** object.
{% endhint %}

The presence of the mina provider object, `window.mina`, in a user's browser indicates an Mina Protocol user.

To demonstrate this, verify whether your browser is running Auro Wallet by copying and pasting the following code snippet into your browser's developer console:

```javascript
if (typeof window.mina !== 'undefined') {
  console.log('Auro Wallet is installed!');
}
```

## Request Account

Interactive with Auro Wallet require connect account. This method returns an array when user confirm authorizes, which contains address that authenticated. The current array returns one address at a time. Returns a ProviderError when user reject authorization.

```typescript
const account:string[]|ProviderError = await window.mina.requestAccounts()
    .catch((err: any) => err);

console.log(account)
```

{% hint style="info" %}
**requestAccounts** will show a popup window when Auro Wallet lock or have no connected account, if you want to request account without popup window . you can use\
[getAccounts](../reference/api-reference/methods/#getaccounts)
{% endhint %}

```javascript
let account = await window.mina?.getAccounts();

console.log(account)
```

## Account Event

This method is used to monitor account changes. When the account changes, the monitoring will be triggered.

```javascript
window.mina?.on("accountsChanged", (accounts: string[]) => {
    console.log(accounts);
});
```
