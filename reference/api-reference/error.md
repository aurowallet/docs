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

if return failed info , zkapp can get error code.

```typescript
 * code 4001 The request was rejected by the user
 * code 4300 User disconnect, need connect first
 * code -32005 Have Pending chain action
 * code -32006 Not support chain
 * code -32007 No wallet found
 * code -32008 Verify failed
 * code -32602 The parameters were invalid
 * code -32603 Internal error
 * code -32800 Unspecified error message
 * code -32900 Origin dismatch
```
