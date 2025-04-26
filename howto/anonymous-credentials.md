---
description: >-
  This scenario is mainly used to handle the store credentials and verifying
  presentations.
---

# Anonymous Credentials

## Store Credentials

This method is mainly used to save credentials.

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

const storeResult: IStoreCredentialData = await window.mina
    .storePrivateCredential({
        credential: credential,
    })
    .catch((err: any) => err);
```

## Verifying Presentations

This method is mainly used to verify the presentation.

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


const verifyResult: IRequestPresentation = await window.mina
    .requestPresentation({
      presentation: {
        presentationRequest: presentationRequest,
      },
    })
    .catch((err: any) => err);
```

{% hint style="info" %}
The current implementation of Anonymous Credentials is based on [mina-attensions](https://github.com/zksecurity/mina-attestations) v0.5.0
{% endhint %}
