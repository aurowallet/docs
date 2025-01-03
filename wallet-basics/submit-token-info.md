---
description: >-
  Auro Wallet will display the token assets based on the submitted information
  by default.
---

# Submit token info

[**Click here to submit the information.**](https://github.com/aurowallet/launch/tree/master/token)

#### 1. Add token information by updating the `token.json` file (in the corresponding network). Do not change the order.

```typescript
// This is an example submission
{
    "id": "xLpobAxWSYZeyKuiEb4kzHHYQKn6X1vKmFR4Dmz9TCADLrYTD1", // token id
    "address": "B62qmMv99rMLCjnApLERcvof6fP4YD4wqeCXUrFuthHfTNoHbYgmy1i", // token address
    "name": "TEST", // token name
    "symbol": "7UjV6", // token symbol
    "decimal": "6", // token decimal
    "description": "Auro test token in Mainnet", // Optional. token description
    "website":"https://www.aurowallet.com/", // Optional. 
    "fungibleTokenVersion": "1.1.0" // Optional. 
}
```

```md
`fungibleTokenVersion` is an optional field. 
The content should be one of the version fields in https://www.npmjs.com/package/mina-fungible-token

The content is the version of mina-fungible-token currently in use.
Auro Wallet uses the latest version by default.

- If set, Auro Wallet will use the target version of the mina-fungible-token.
- If not set, the latest mina-fungible-token will be used by default.

Custom tokens `do not need` to set fungibleTokenVersion.
```

#### 2. Create a folder with the token ID and add your token icon to `{networkID}/assets/{tokenID}/icon.png`.

* Icon resolution must be 128\*128px.
* The icon file name must be `icon.png`.

#### 3. Send token for testing

You can use the Mainnet or Testnet for this. The purpose is to test whether the token can be send normally before the merge. Send tokens to the following address for testing:

**`B62qpjxUpgdjzwQfd8q2gzxi99wN7SCgmofpvw27MBkfNHfHoY2VH32`**

We will send token to your sending address after the test is completed (return to the original address).

#### 4. Provide the token contract source code (Optional)

We currently use the [fungible token contract](https://github.com/MinaFoundation/mina-fungible-token/releases/tag/v1.0.0). If you modify the contract code, it may cause a mismatch between the token contract and the source code. To prevent this, it is recommended to submit the token contract source code in the PR, so it can be integrated into the build service.

* Example location: `token/{networkID}/assets/xLpobAxWSYZeyKuiEb4kzHHYQKn6X1vKmFR4Dmz9TCADLrYTD1/source`

#### 5. Verify Token Ownership

Add the signature of the `token.json` file submitted or updated in step 1 to the PR comment. This should be signed using the token account. Now can get the signed message in [Auro-Test-zkApp](https://test-zkapp.aurowallet.com/token-submit).

* ```js
  // After signed, submit the result in the comment
  {"field":"10082789485841188200651752083435401189651661935760768844006925598425995295018","scalar":"13559698666955008071097956591497128241909562564253145138590504826423557135826"}
  ```

#### 6. Make a PR

Once all steps are completed, create a PR for review.