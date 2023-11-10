---
description: This method is used to sign Json message.
---

# mina\_sign\_JsonMessage

### Params

```typescript
type JsonMessageData  = {
    // show title.
    label:string
    // show value.
    value:string
}

export type SignJsonMessageArgs = {
    readonly message: Array<JsonMessageData>
}
```

### Result

```typescript
interface SignedData {
    // sign account address.
    publicKey: string;
    // sign message.
    data: string;
    // sign result.
    signature: {
        field: string;
        scalar: string;
    }
}

interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body.
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
const msgParams = [
    { label: "Label:", value: "Sign Confirm" },
    {
      label: "Message:",
      value: "Click to sign in and accept the Terms of Service",
    },
    {
      label: "URI:",
      value: "window.location.href",
    },
    {
      label: "Chain ID:",
      value: network.chainId,
    },
    {
      label: "Chain Name:",
      value: network.name,
    },
    {
      label: "Issued At:",
      value: new Date().getTime(),
    },
    {
      label: "Resources:",
      value: "https://docs.aurowallet.com/",
    },
];

await window.mina?.signJsonMessage({ message: msgParams }).catch((err: any) => err);
```

### Result

```typescript
// successful result.
{
  "signature": {
    "field": "15090234057839595695283019772297604801858172950962387359567660702180735659373",
    "scalar": "21947964776036205182010988394099954210017471543964218028225956286142062520626"
  },
  "publicKey": "B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD",
  "data": "[{\"label\":\"Label:\",\"value\":\"Sign Confirm\"},{\"label\":\"Message:\",\"value\":\"Click to sign in and accept the Terms of Service\"},{\"label\":\"URI:\",\"value\":\"window.location.href\"},{\"label\":\"Chain ID:\",\"value\":\"mainnet\"},{\"label\":\"Chain Name:\",\"value\":\"testchain\"},{\"label\":\"Issued At:\",\"value\":1699295213633},{\"label\":\"Resources:\",\"value\":\"https://docs.aurowallet.com/\"}]"
}

// can not get connect address.
{
  "code": 1001,
  "message": "User disconnect, please connect first. "
}

// user reject.
{
  "code": 1002,
  "message": "User rejected the request. "
}
```
