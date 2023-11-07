---
description: Mainly used to create nullifiers
---

# mina\_createNullifier

### Params

```typescript
type CreateNullifierArgs = {
  readonly message: bigint[]
}
```

### Result

```typescript
type Group = {
  x: bigint;
  y: bigint;
};

export type Nullifier = {
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
  message: string; // error message
  code: number; // error code 
  data?: unknown;// error body 
}

Promise<Nullifier | ProviderError>
```

### Errors

|        |                                     |                               |
| ------ | ----------------------------------- | ----------------------------- |
| 1002   | user reject transaction             |                               |
| 1001   | User disconnect, need connect first | can not get connected account |
| 23001 | Origin dismatch                     |                               |

## Example

### Request

```typescript
const signContent = [1,2,3]
await window.mina.createNullifier({ message: signContent }).catch((err: any) => err);
```

### Result

```typescript
// success result
{
  "publicKey": {
    "x": "5248528914034818597164419364515906783046550751002313167808067803822526836450",
    "y": "8499673205188463960219287503467053771967554971086609841768360242543765381807"
  },
  "private": {
    "c": "9902185640563099798552538703361718566830920909287274415375718449173766417439",
    "g_r": {
      "x": "23709477331717770451048134593130727683043593683401466930366147533380855637145",
      "y": "18760208553553506432939082676972461624515683232329707805004444151147449487796"
    },
    "h_m_pk_r": {
      "x": "15858225469987785242406457588027706230191637416882043355002940613645441083323",
      "y": "25708145549986256124255195010233858317380687279717405739951366139000324110011"
    }
  },
  "public": {
    "nullifier": {
      "x": "3361150403274954664604230770379378491388033780248903656881561776735665100150",
      "y": "13198964082679393929618472402851291476272996295959277116839569765356779886575"
    },
    "s": "15386289247285176606445846857509398164434569113204850486864311070500369459309"
  },
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

