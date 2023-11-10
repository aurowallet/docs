---
description: >-
  This method is used to request the current connect account . It is a silent
  request. If there is a connected account, it will return the connected
  account. If not, it will return an empty array.
---

# mina\_accounts

### Params

null

### Result

string\[]

### Errors

null

### Example

#### Request

```typescript
await window.mina?.getAccounts();
```

#### Result

```typescript
// have connect account
["address"]
// if not 
[] 
```
