---
description: This method is used to verify the validity of the signature info.
---

# mina\_verifyMessage

### Params

```typescript
interfaceVerifyMessageArgs{
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
```

### Result

```typescript
interface ProviderError extends Error {
  message: string; // error message
  code: number; // error code 
  data?: unknown;// error body 
}

Promise<boolean | ProviderError>
```

### Errors

|        |                 |   |
| ------ | --------------- | - |
| -32008 | Verify failed   |   |
| -32900 | Origin dismatch |   |

## Example

### Request

```typescript
let verifyMessageBody = {
  "signature": {
    "field": "13468724101429370746602596170094552502200193721398063751467629418902449650534",
    "scalar": "5638584219029837254561020594864591092072844530049610703222272818700774330907"
  },
  "publicKey": "B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD",
  "data": "Click \"Sign\" to sign in. No password needed!\n\nThis request will not trigger a blockchain transaction or cost any gas fees.\n\nI accept the Auro Test zKApp Terms of Service: http://localhost:3000/\n\naddress: \niat: 1699294808439"
};

await window.mina?.verifyMessage(verifyMessageBody).catch((err: any) => err);

```

### Result

```typescript
//successful result
false | true

// verify failed
{
  "message": "Verify failed",
  "code": -32008
}
```
