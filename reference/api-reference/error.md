---
description: Here is the error message returned by the provider
---

# Error

Now we just use error message show the error detail , website can show the error to user . We reserve the code field, which will be activated later if necessary

```typescript
/**error type*/
interface ProviderError extends Error {
  message: string;
  code: number;
  data?: unknown;
}
```

## Error code information

if return failed info , zkApp can get error code.

```typescript
 * code 1001 User disconnect, need connect first
 * code 1002 The request was rejected by the user
 * code 20001 No wallet found
 * code 20002 Verify failed
 * code 20003 The parameters were invalid
 * code 20004 Not support chain
 * code 20005 Have Pending chain action
 * code 21001 Internal error
 * code 22001 Unspecified error message
 * code 23001 Origin dismatch
```
