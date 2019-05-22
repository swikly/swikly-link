This is [Swikly](https://www.swikly.com)'s official documentation on how to generate and implement Swikly's transaction link.  
Swikly enables you to generate a transaction link for any transaction request type:

 - Deposit, down payment or payment.
 - Complex transactions request of any combination.

## Sandbox and production environments

## Authentication

You must have an active Swikly account, a **secret** and a valid Swikly **userId** to create a custom Swikly Link. Create your account at the following Internet address:

| Environment  | Url  |
|---|---|
| Sanbox | [https://sandbox.swikly.com](https://sandbox.swikly.com)  |
| Production  | [https://www.swikly.com](https://www.swikly.com) |

Once your account created, go to:  **My Account** > **Developers**. You will find your **secret** and **userId** in this section.

## Checkout Root

The aim of the Swikly Link is to redirect the user accepting a transaction to Swikly's checkout. Swikly's checkout will then process all the parameters set in the link and display the necessary transaction information to the user.

## Link Parameters

| Parameter  | Description  | Type | Format  | Min Value | Max Value  | Default Value  | Key Dependent | Required |
|---|---|:---:|---|:---:|:---:|:---:|:---:|:---:|
|  userId | Swikly account userId | *string*  |  |  | | | yes  | yes|
| amountDeposit  | Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If absent or set to 0, no deposit will be requested.  | *int*  |   | 0 | 250000  |   | yes  | no
| amountReservation  | Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If absent or set to 0, no down payment will be requested.  | *int*  |   | 0| 250000  |   | yes  | no
| amountPayment | Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If absent or set to 0, no payment will be requested.  | *int*  |   |  |  |   |   | yes  | no
| description  |  Text displayed on the overview page of the form describing the purpose of the request. | *string* |   |   |   |   | no | no
| overviewDisplay  | If set to 0, bypasses the display of the overview page of the form. However, to bypasss the overview page, the following parameter must be set in the link: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also mandatory and will be used to calculate the tourist tax. | *int*  |   | 0  | 1  | 1  | no  | no
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |
|   |   |   |   |   |   |   |   |



