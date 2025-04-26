---
description: This method is used to store private credentials.
---

# mina\_storePrivateCredential

{% hint style="info" %}
Support from Auro-Wallet-extension v2.3.2.
{% endhint %}

## Params

```typescript
type JSONValue =
    | string
    | number
    | boolean
    | null
    | JSONValue[]
    | { [key: string]: JSONValue };


type Credential<Data = unknown> = { owner: string; data: Data };
type StoredCredential<Data = unknown, Witness = unknown> = {
    version: 'v0';
    witness: Witness;
    metadata: JSONValue | undefined;
    credential: Credential<Data>;
};

type StoredCredentialArgs = {
    credential:StoredCredential
}
```

## Result

```typescript
type IStoreCredentialData = {
    credential: string;
};
```

## Errors

|       |                                            |                                |
| ----- | ------------------------------------------ | ------------------------------ |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account. |
| 1002  | The request was rejected by the user.      |                                |
| 20003 | The parameters were invalid.               | Please check address, fee.     |
| 23001 | Origin dismatch.                           | Check origin safe.             |

## Example

### Request

```typescript
const credential = {"version":"v0","witness":{"type":"native","issuer":{"_type":"PublicKey","value":"B62qp6y93m7HztH5jvn12gHJphzAZrZq3daD792hi8a6WSivDS62M6y"},"issuerSignature":{"_type":"Signature","value":{"r":"20488774605787391652280562339538477966865965211091577050649120180217379031673","s":"16708818945490883015829890483065574022023217519234257567358763357703611506560"}}},"credential":{"owner":{"_type":"PublicKey","value":"B62qpjxUpgdjzwQfd8q2gzxi99wN7SCgmofpvw27MBkfNHfHoY2VH32"},"data":{"nationality":"KR","name":"zvCICx","birthDate":{"_type":"Int64","value":{"magnitude":"215913411073","sgn":"Negative"}},"id":{"_type":"Bytes","size":16,"value":"2a4dc0212e4c68fff1ae6ffbb2c194fb"},"expiresAt":{"_type":"UInt64","value":"1777182333186"}}}}

await window.mina.storePrivateCredential({
    credential: credential,
})
.catch((err: any) => err);

```

### Result

```typescript
// successful result.
{
    credential:"{\"version\":\"v0\",\"witness\":{\"type\":..."
}
```
