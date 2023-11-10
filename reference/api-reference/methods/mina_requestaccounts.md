---
description: >-
  This method is used to request the current connect account. If there is a
  connected account, the connected account will be returned. If not, a popup
  window will show to request a connection.
---

# mina\_requestAccounts

### Params

null

### Result

```typescript
interface ProviderError extends Error {
    message: string; // error message
    code: number; // error code 
    data?: unknown;// error body 
}

// string[] will contain the connected account address
Promise<string[] | ProviderError>
```

### Error

<table><thead><tr><th></th><th width="332.3333333333333"></th><th></th></tr></thead><tbody><tr><td>1002</td><td>The request was rejected by the user.</td><td></td></tr><tr><td>20001</td><td>No account found.</td><td>Need create or restore account in Auro Wallet first.</td></tr><tr><td>23001</td><td>Origin dismatch.</td><td>Check origin safe.</td></tr></tbody></table>

## Example

### Request

```typescript
await window.mina.requestAccounts().catch((err: any) => err);
```

### Result

```typescript
// user reject
{
  "code": 1002,
  "message": "User rejected the request."
}

// success result
[
  "B62qpjxUpgdjzwQfd8q2gzxi99wN7SCgmofpvw27MBkfNHfHoY2VH32"
]
```
