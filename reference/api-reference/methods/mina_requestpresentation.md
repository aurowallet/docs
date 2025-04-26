---
description: This method is used to verify presentation.
---

# mina\_requestPresentation

{% hint style="info" %}
Support from Auro-Wallet-extension v2.3.2.
{% endhint %}

## Params

```typescript
type PresentationRequestType = 'no-context' | 'zk-app' | 'https';
type PresentationRequest<
    RequestType extends PresentationRequestType = PresentationRequestType,
    InputContext = any,
> = {
    type: RequestType;
    spec: any;
    claims: any;
    inputContext: InputContext;
    program?: unknown;
    verificationKey?: unknown;
};

type IPresentationRequest = {
    presentationRequest:PresentationRequest
    zkAppAccount?:any // used for type zk-app
}

type PresentationArgs = {
    presentation:IPresentationRequest
}
```

## Result

```typescript
type IRequestPresentation = {
    presentation: string;
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
const presentationRequest = {"type":"https","spec":{"inputs":{"credential":{"type":"credential","credentialType":"native","witness":null,"data":{"_type":"DynamicRecord","maxEntries":20,"knownShape":{"expiresAt":{"_type":"UInt64"}},"_isFactory":true}},"expectedIssuer":{"type":"claim","data":{"_type":"Field"}},"createdAt":{"type":"claim","data":{"_type":"UInt64"}}},"assert":{"type":"and","inputs":[{"type":"equals","left":{"type":"issuer","credentialKey":"credential"},"right":{"type":"property","key":"expectedIssuer","inner":{"type":"root"}}},{"type":"lessThanEq","left":{"type":"property","key":"createdAt","inner":{"type":"root"}},"right":{"type":"property","key":"expiresAt","inner":{"type":"credential","credentialKey":"credential","credentialType":"native"}}}]},"outputClaim":{"type":"constant","data":{"_type":"Undefined","value":null}}},"claims":{"expectedIssuer":{"_type":"Field","value":"16167289078389923610953595615737668731080372316578280370618447557903825457595"},"createdAt":{"_type":"UInt64","value":"1745647048630"}},"inputContext":{"type":"https","serverNonce":{"_type":"Field","value":"817980905302159961768471044132257779624448992114290456026544408364528955972"},"action":"credentials-web-demo-server:anonymous-login"}}

await window.mina.requestPresentation({
    presentation: {
      presentationRequest: presentationRequest,
    },
})
.catch((err: any) => err);
```

### Result

```typescript
// successful result.
{
    presentation:"{\"version\":\"v0\",\"claims\"...}"
}
```
