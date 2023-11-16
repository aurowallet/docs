---
description: Mainly used to create nullifier.
---

# Create Nullifier

```typescript
type Group = {
    x: bigint;
    y: bigint;
};

type Nullifier = {
    publicKey: Group;
    public: {
        nullifier: Group;
        s: bigint;
    };
    private: {
        c: bigint;
        g_r: Group;
        h_m_pk_r: Group;
    };
};

interface ProviderError extends Error {
    message: string;
    code: number;
    data?: unknown;
}

const signResult: Nullifier|ProviderError = await window.mina
    ?.createNullifier({
        message: "fields",
    }).catch((err: any) => err);
```
