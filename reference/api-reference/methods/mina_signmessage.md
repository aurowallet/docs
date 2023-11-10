---
description: This method is used to sign message.
---

# mina\_signMessage

### Params

```typescript
type SignMessageArgs = {
    // need sign Message
    readonly message: string
}
```

### Result

```typescript

interface SignedData {
    // sign account address
    publicKey: string;
    // sign message
    data: string;
    // sign result
    signature: {
        field: string;
        scalar: string;
    }
}

interface ProviderError extends Error {
    message: string; // error message
    code: number; // error code 
    data?: unknown;// error body 
}


Promise<SignedData | ProviderError> 
```

### Errors

|       |                                            |                                |
| ----- | ------------------------------------------ | ------------------------------ |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account. |
| 1002  | The request was rejected by the user.      |                                |
| 23001 | Origin dismatch.                           | Check origin safe.             |

## Example

### Request

```typescript
const content = `Click "Sign" to sign in. No password needed!

This request will not trigger a blockchain transaction or cost any gas fees.

I accept the Auro Test zkApp Terms of Service: ${window.location.href}

address: ${currentAccount}
iat: ${new Date().getTime()}`;

await window.mina?.signMessage({ message: content }).catch((err: any) => err);
```

### Result

```typescript
// success result
{
  "signature": {
    "field": "13468724101429370746602596170094552502200193721398063751467629418902449650534",
    "scalar": "5638584219029837254561020594864591092072844530049610703222272818700774330907"
  },
  "publicKey": "B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD",
  "data": "Click \"Sign\" to sign in. No password needed!\n\nThis request will not trigger a blockchain transaction or cost any gas fees.\n\nI accept the Auro Test zkApp Terms of Service: http://localhost:3000/\n\naddress: \niat: 1699294808439"
}

// can not get connect address
{
  "code": 1001,
  "message": "User disconnect, please connect first"
}

// user reject 
{
  "code": 1002,
  "message": "User rejected the request."
}
```
