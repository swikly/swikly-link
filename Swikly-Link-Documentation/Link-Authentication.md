# Authentication

Each transaction link you create, or generate within your application, has to be authenticated with a Control Key value set in the `ctrlKey` parameter. This `ctrlKey` is a **SHA256** hash resulting of the concatenation of several parameter values set in a specific order. It allows Swikly to check that important parameter values have not been tempered with.
&nbsp;
| Parameters in the following order | Value  |
|---|---|
| forcedClientFee | Set value or leave it empty if you don't use it |
| amountDeposit  | Set value or 0 if you don't use it |
| amountReservation  | Set value or 0 if you don't use it |
| amountPayment  | Set value or 0 if you don't use it |
| cityTax  | Set value or leave it empty if you don't use it |
| userId  | Swikly's account *userId* found at **My Account** > **Developers** |
| linkId  | linkId provided by Swikly or leave it empty if you don't use it |
| freeText  | Set value or leave it empty if you don't use it |
| Link Secret | Swikly's account *Link Secret* found at **My Account** > **Developers** |
&nbsp;
You must have an active Swikly account, a **Link Secret** and a Swikly **userId** to create a custom Swikly Transaction Link. Create your account in the **[sandbox environment](/Swikly-Link-Documentation/Environments)** for testing or in the **[production environment](/Swikly-Link-Documentation/Environments)** to go live. Once connected to your Swikly account, go to:  **My Account** > **Developers**. You will find your **Link Secret** and account **userId** in this section.

### Sample usage with the following dummy user:
- userId: userId123456789
- Link Secret: mygreatsecret

The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=userId123456789&amountDeposit=10000&ctrlKey=5eec5d8f5cfc236afa3226b9bb3c7c514e6b6b3044bdc9b528b5b2795540be34
```

The `ctrlKey` is computed this way: 

```
String to hash: 1000000userId123456789mygreatsecret
sha256 result: 9fe286c38319818a49898185ae19d459cc9591c01472ec1ac146d4ad508b541d
```