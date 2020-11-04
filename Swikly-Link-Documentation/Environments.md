# Sandbox and production environments

Swikly's Transaction Link redirects the end-user to Swikly's checkout. Swikly's checkout will then process all the GET request parameters set in the link and display the necessary transaction information to the end-user as well as the credit card form for him to complete the transaction.

- ## Sandbox

The sandbox environment enables you to test your links and application integration. All transactions made and accepted in sandbox mode are for testing purpose only. To complete a  transaction from end to end in sandbox mode, you have to use a **[test credit card](/Swikly-Link-Documentation/Test-Credit-Cards)**.

| Environment  | URL  | Usage |
|---|---| --- |
| Sandbox | [https://sandbox.swikly.com](https://sandbox.swikly.com) | Test |
| Sandbox Checkout Root | [https://sandbox.swikly.com/checkout](https://sandbox.swikly.com/checkout)  | Test |

- ## Production 

The production environment enables you to go live with your links and application integration. All transactions made and accepted in production are real transactions. To complete a transaction in production mode, you have to use a **real credit card**. 

| Environment  | URL | Usage |
|---|---| --- |
| Production | [https://www.swikly.com](https://www.swikly.com) | Live |
| Production Checkout Root | [https://www.swikly.com/checkout](https://www.swikly.com/checkout) | Live |