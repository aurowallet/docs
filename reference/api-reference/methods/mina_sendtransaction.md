---
description: This method is used for sign and broadcast zkApp transaction.
---

# mina\_sendTransaction

{% hint style="info" %}
You need to create zk commond in zkApp first, then call Auro Wallet to sign and broadcast.
{% endhint %}

### Params

```typescript
interface SendTransactionArgs  {
    // only sign with auro wallet, auro-extension-wallet support from V2.2.16. 
    readonly onlySign?: boolean; 
    // transaction is zk commond that create by contract.
    readonly transaction: string | object;
    // option. 
    readonly feePayer?: {
        // option. Auro Wallet also provide advance option to change fee.
        readonly fee?: number;
        // option.
        readonly memo?: string;
    };
}
```

### Result

```typescript
type SendTransactionHash = {
    // broadcast hash, you can query tx info by this hash.
    hash: string;
};

type SignedZkappCommand = {
    // results of JSON.stringify( signZkappCommand().data )
    signedData: string; 
};

type SendZkTransactionResult = SendTransactionResult | SignedZkappCommand

interface ProviderError extends Error {
    message: string; // error message.
    code: number; // error code.
    data?: unknown; // error body. 
}

Promise<SendTransactionResult | ProviderError>
```

### Errors

|       |                                            |                                |
| ----- | ------------------------------------------ | ------------------------------ |
| 1001  | User disconnect, need connect Auro Wallet. | Can not get connected account. |
| 1002  | The request was rejected by the user.      |                                |
| 20003 | The parameters were invalid.               | Please check address, fee.     |
| 23001 | Origin dismatch.                           | Check origin safe.             |

## Example

### Request

```typescript
const transactionJSON = {"feePayer":{"body":{"publicKey":"B62qiTKpEPjGTSHZrtM8uXiKgn8So916pLmNJKDhKeyBQL9TDb3nvBG","fee":"0","validUntil":null,"nonce":"0"},"authorization":"7mWxjLYgbJUkZNcGouvhVj5tJ8yu9hoexb9ntvPK8t5LHqzmrL6QJjjKtf5SgmxB4QWkDw7qoMMbbNGtHVpsbJHPyTy2EzRQ"},"accountUpdates":[{"body":{"publicKey":"B62qnwTPcbNqvrpw3pxdsD3NLnbadNJFk5MZnxQLUaX52EiGX7x9TM8","tokenId":"wSHV2S4qX9jFsLjQo8r1BsMLH2ZRKsZx6EJd1sbozGPieEC4Jf","update":{"appState":["33",null,null,null,null,null,null,null],"delegate":null,"verificationKey":null,"permissions":null,"zkappUri":null,"tokenSymbol":null,"timing":null,"votingFor":null},"balanceChange":{"magnitude":"0","sgn":"Positive"},"incrementNonce":false,"events":[],"actions":[],"callData":"9480311477670922688987895225723267062012786366393322319448750791657739847081","callDepth":0,"preconditions":{"network":{"snarkedLedgerHash":null,"blockchainLength":null,"minWindowDensity":null,"totalCurrency":null,"globalSlotSinceGenesis":null,"stakingEpochData":{"ledger":{"hash":null,"totalCurrency":null},"seed":null,"startCheckpoint":null,"lockCheckpoint":null,"epochLength":null},"nextEpochData":{"ledger":{"hash":null,"totalCurrency":null},"seed":null,"startCheckpoint":null,"lockCheckpoint":null,"epochLength":null}},"account":{"balance":null,"nonce":null,"receiptChainHash":null,"delegate":null,"state":["31",null,null,null,null,null,null,null],"actionState":null,"provedState":null,"isNew":null},"validWhile":null},"useFullCommitment":false,"implicitAccountCreationFee":false,"mayUseToken":{"parentsOwnToken":false,"inheritFromParent":false},"authorizationKind":{"isSigned":false,"isProved":true,"verificationKeyHash":"10245640308479032248697049003357984740828440340040477697922362566190589502399"}},"authorization":{"proof":null,"signature":null}}],"memo":"E4YM2vTHhWEg66xpj52JErHUBU4pZ1yageL4TVDDpTTSsv8mK6YaH"}"
const fee = ""
const memo = ""
const onlySign = true;

await window.mina?.sendTransaction({
        onlySign: onlySign,
        transaction: transactionJSON,
        feePayer: {
            fee: fee,
            memo: memo,
        },
    });
```

### Result

```typescript
// successful result.
{
  "hash": "5JuVoDUC2kb3m1dQxG1B9Ar9VhZh4HuABGLgCoYnEJqZVhthk4TV"
}

// can not get connect address.
{
  "code": 1001,
  "message": "User disconnect, please connect first."
}

// user reject.
{
  "code": 1002,
  "message": "User rejected the request."
}

// params check error. there check addres, fee.
{
  "code": 20003,
  "message": "Invalid method parameter(s)."
}

// only sign with auro wallet
{
  "signedData":'{"zkappCommand":{"feePayer":{"body":{"publicKey":"B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD","fee":"10100000","validUntil":null,"nonce":"98"},"authorization":"7mXMsb2cc2RR8qnrubXZ3Wjsx13WhRbuetD9yGbGD7Do58vaph8VanDTb5jZmbX8oUA5koPdAiixvqZ2a2bDyRcjQDDwdiHA"},"accountUpdates":[{"body":{"publicKey":"B62qpSvbc66k2ecSmdryPAUFCPQStHo4Vc8rxYU8K4LSGRSMVwxw6nk","tokenId":"wSHV2S4qX9jFsLjQo8r1BsMLH2ZRKsZx6EJd1sbozGPieEC4Jf","update":{"appState":["63",null,null,null,null,null,null,null],"delegate":null,"verificationKey":null,"permissions":null,"zkappUri":null,"tokenSymbol":null,"timing":null,"votingFor":null},"balanceChange":{"magnitude":"0","sgn":"Positive"},"incrementNonce":false,"events":[],"actions":[],"callData":"21961609069728653483958795532181351452085718952361457203914335723687686999994","callDepth":0,"preconditions":{"network":{"snarkedLedgerHash":null,"blockchainLength":null,"minWindowDensity":null,"totalCurrency":null,"globalSlotSinceGenesis":null,"stakingEpochData":{"ledger":{"hash":null,"totalCurrency":null},"seed":null,"startCheckpoint":null,"lockCheckpoint":null,"epochLength":null},"nextEpochData":{"ledger":{"hash":null,"totalCurrency":null},"seed":null,"startCheckpoint":null,"lockCheckpoint":null,"epochLength":null}},"account":{"balance":null,"nonce":null,"receiptChainHash":null,"delegate":null,"state":[null,null,null,null,null,null,null,null],"actionState":null,"provedState":null,"isNew":null},"validWhile":null},"useFullCommitment":false,"implicitAccountCreationFee":false,"mayUseToken":{"parentsOwnToken":false,"inheritFromParent":false},"authorizationKind":{"isSigned":false,"isProved":true,"verificationKeyHash":"2463176747116618058094797786079315209173315865869177351205687923345657415010"}},"authorization":{"proof":null,"signature":null}}],"memo":"E4YM2vTHhWEg66xpj52JErHUBU4pZ1yageL4TVDDpTTSsv8mK6YaH"},"feePayer":{"feePayer":"B62qr2zNMypNKXmzMYSVotChTBRfXzHRtshvbuEjAQZLq6aEa8RxLyD","fee":"10100000","nonce":"98","memo":"","validUntil":null}}'
}
```
