---
description: This method is used to verify the validity of the signature info.
---

# mina\_verifyFields

### Params

```typescript
interface VerifyFieldsArguments {
  // sign publicKey
  publicKey: string,
  // sign fields
  data: (string|number)[],
  signature:string
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

### Error

|        |                 |   |
| ------ | --------------- | - |
| -32008 | Verify failed   |   |
| -32900 | Origin dismatch |   |

## Example

### Request

```typescript
const verifyMessageBody = {
      publicKey: "B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD",
      signature: "7mX4QDZBoq3eTfLhvoWzBBQnUhxBfVCUcXwnPsDoEqcpiGacuoeYq3i9HpMfFUvvTz5qG4C2zqCDDBoB5KPamAko15m4wMiS",
      data:  [1,2,3]
      
    };

await window.mina?.verifyFields(verifyMessageBody).catch((err: any) => err);
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

