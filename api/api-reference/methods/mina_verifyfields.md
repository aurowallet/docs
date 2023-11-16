---
description: This method is used to verify the signature results of fields.
---

# mina\_verifyFields

### Params

```typescript
interface VerifyFieldsArguments {
    // sign publicKey.
    publicKey: string,
    // sign fields.
    data: (string|number)[],
    signature:string
}
```

### Result

```typescript
interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body.
}

Promise<boolean | ProviderError> 
```

### Error

|       |                                |                                                                                           |
| ----- | ------------------------------ | ----------------------------------------------------------------------------------------- |
| 20002 | Signature verification failed. | This error is returned because an exception was thrown, please check the signature format |
| 23001 | Origin dismatch.               | Check origin safe.                                                                        |

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
// successful result.
false | true

// verify failed.
{
  "message": "Verify failed",
  "code": 20002
}
```
