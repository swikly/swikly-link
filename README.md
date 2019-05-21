# Swikly Link Documentation
This is [Swikly](https://www.swikly.com)'s official documentation on how to generate and implement Swikly's transaction link.  
Swikly enables you to generate a transaction link for any transaction request type:

 - Deposit, down payment or payment.
 - Complex transactions request of any combination.

## Sandbox and production environments

## Authentication

You must have an active Swikly account and a secret key to create a custom Swikly Link. Create your account at the following Internet address:

| Environment  | Url  |
|---|---|
| Sanbox | [https://sandbox.swikly.com](https://sandbox.swikly.com)  |
| Production  | [https://www.swikly.com](https://www.swikly.com) |

Once your account created, go to:  **My Account** > **Developers**. You will find your secret key in this section.

## Checkout Root

The aim of the Swikly Link is to redirect the user accepting a transaction to Swikly's checkout. Swikly's checkout will then process all the parameters set in the link and display the necessary transaction information to the user.  