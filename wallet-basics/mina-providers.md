---
description: >-
  Starting from Auro Extension 2.3.0 and Auro App 2.1.0, Auro Wallet introduces
  a new method to use providers, called "Announce Provider," which supports
  multiple providers.
---

# Mina Providers

## 1. Announce Provider (Recommended)

```ts
let auroProvider: any; 
useEffect(() => {
    const handleAnnounceProvider = async (event: any) => {
      if (!auroProvider) {
        if (
          event?.detail?.info?.slug === "aurowallet" ||
          event?.detail?.provider?.isAuro
        ) {
          auroProvider = event?.detail?.provider;
        }
      }
      if (auroProvider) {
        // can excute action in here
      }
    };

    window.addEventListener("mina:announceProvider", handleAnnounceProvider);

    window.dispatchEvent(new Event("mina:requestProvider"));
    setTimeout(() => {
      window.dispatchEvent(new Event("mina:requestProvider"));
    }, 1000);

    return () => {
      window.removeEventListener(
        "mina:announceProvider",
        handleAnnounceProvider
      );
    };
  }, []);
```

## 2. Use window.mina

This method is always available and will not be deprecated.

`window.mina && window.mina.isAuro`
