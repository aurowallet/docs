---
description: This method is used to sign the field
---

# mina\_signFields

{% hint style="info" %}
The output of numbers and string type numbers is the same in sign fields&#x20;
{% endhint %}

### Params

```typescript
type SignFieldsArguments = {
  readonly message: (string|number)[],
}
```

### Result

```typescript
type SignedFieldsData  = {
  // sign data
  data: (string|number)[],
  // signature
  signature:string
}


interface ProviderError extends Error {
  message: string; // error message
  code: number; // error code 
  data?: unknown;// error body 
}

Promise<SignedFieldsData | ProviderError>
```

### Error

|        |                                     |                               |
| ------ | ----------------------------------- | ----------------------------- |
| 1002   | user reject transaction             |                               |
| 1001   | User disconnect, need connect first | can not get connected account |
| 23001 | Origin dismatch                     |                               |

## Example

### Request

```typescript
await window.mina?.signFields({ message: [1,2,3] }).catch((err: any) => err);
```

### Result

```typescript
// success 
{
  "signature": "7mX4QDZBoq3eTfLhvoWzBBQnUhxBfVCUcXwnPsDoEqcpiGacuoeYq3i9HpMfFUvvTz5qG4C2zqCDDBoB5KPamAko15m4wMiS",
  "publicKey": "B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD",
  "data": [
    1,
    2,
    3
  ]
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
