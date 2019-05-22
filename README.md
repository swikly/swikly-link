This is [Swikly](https://www.swikly.com)'s official documentation on how to generate and implement Swikly's transaction link.  
Swikly enables you to generate a transaction link for any transaction request type:

 - Deposit, down payment or payment.
 - Complex transactions request of any combination.

# Definitions
- ## # Overview page
- ## # Checkout page 
- ## # End-User

# Sandbox and production environments
- ## # Sandbox
- ## # Production 

# Authentication

You must have an active Swikly account, a **secret** and a valid Swikly **userId** to create a custom Swikly Link. Create your account at the following Internet address:

| Environment  | Url  |
|---|---|
| Sanbox | [https://sandbox.swikly.com](https://sandbox.swikly.com)  |
| Production  | [https://www.swikly.com](https://www.swikly.com) |

Once your account created, go to:  **My Account** > **Developers**. You will find your **secret** and **userId** in this section.

# Checkout Root

The aim of the Swikly Link is to redirect the user accepting a transaction to Swikly's checkout. Swikly's checkout will then process all the parameters set in the link and display the necessary transaction information to the user.

# Parameters

| Parameter         | Description                                                                                                                                                                                                                                                                                                                                                                                                                              |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| userId            | Swikly account userId                                                                                                                                                                                                                                                                                                                                                                                                                    |
| amountDeposit     | Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If absent or set to 0, no deposit will be requested.                                                                                                                                                                                                                                                                   |
| amountReservation | Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If absent or set to 0, no down payment will be requested.                                                                                                                                                                                                                                                    |
| amountPayment     | Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If absent or set to 0, no payment will be requested.                                                                                                                                                                                                                                                                   |
| overviewDisplay   | If set to 0, bypasses the display of the overview page of the form. However, to bypasss the overview page, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also mandatory and will be used to calculate the tourist tax.                                                                                           |
| description       | Text displayed on the overview page of the form describing the purpose of the request.                                                                                                                                                                                                                                                                                                                                                   |
| **[firstName](#firstname)** | The end-user's first name. This value is displayed as an editable value in the firstname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.                                                                                                                                                                                                                    |
| lastName          | The end-user's last name. This value is displayed as an editable value in the lastname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.                                                                                                                                                                                                                      |
| email             | The end-user's email address. This value is displayed as an editable value in the email field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.                                                                                                                                                                                                                     |
| phone             | The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.                                                                                                                                                                                                                      |
| startDate         | This date is displayed on the overview page as the start date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the reservation swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the reservation swik +3 months. |
| endDate           | This date is displayed on the overview page as the end date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the deposit swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the deposit swik  +3 months.          |
| relativeEndDate   | Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks.                                                                      |
| id                | Your cutom booking reference or event ID.                                                                                                                                                                                                                                                                                                                                                                                                |
| language          | Language in which the overview page is displayed.                                                                                                                                                                                                                                                                                                                                                                                        |
| currency          | currency of the transaction                                                                                                                                                                                                                                                                                                                                                                                                              |
| validityCount     | Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set.                                                                                                                                                                                                                                                                                                                  |
| linkId            | Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http://lelien.swikly.com).                                                                                                                                                                                                                                                                                     |
|                   |                                                                                                                                                                                                                                                                                                                                                                                                                                          |

##  userId
Swikly account userId

Type : *string*  
Control key binding: *yes*  
Required: *yes*  
## amountDeposit
Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If absent or set to 0, no deposit will be requested.

Type : *int*
Min. value: 0
Max. value: 250000
Control key binding: *yes*
Required: *no*

## amountReservation
Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If absent or set to 0, no down payment will be requested.

Type : *int*
Min. value: 0
Max. value: 250000
Control key binding: *yes*
Required: *no*

## amountPayment
Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If absent or set to 0, no payment will be requested.

Type : *int*
Min. value: 0
Max. value: 250000
Control key binding: *yes*
Required: *no*

## overviewDisplay
If set to 0, bypasses the display of the overview page of the form. However, to bypasss the overview page, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also mandatory and will be used to calculate the tourist tax.

Type : *int*
Allowed values: 0 or 1
Default value : 1
Control key binding: *no*
Required: *no*

## description
Text displayed on the overview page of the form describing the purpose of the request.

Type : *string*
Control key binding: *no*
Required: *no*

## firstName
The end-user's first name. This value is displayed as an editable value in the firstname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*
Control key binding: *no*
Required: *yes* if `overviewDisplay` is set to 0.

## lastName
The end-user's last name. This value is displayed as an editable value in the lastname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*
Control key binding: *no*
Required: *yes* if `overviewDisplay` is set to 0.

## email
The end-user's email address. This value is displayed as an editable value in the email field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*
Control key binding: *no*
Required: *yes* if `overviewDisplay` is set to 0.

## phone
The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*
Control key binding: *no*
Required: *yes* if `overviewDisplay` is set to 0.

## startDate
This date is displayed on the overview page as the start date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the reservation swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the reservation swik +3 months.

Type : *string*
Format: *YYYY‐MM‐DD*
Control key binding: *no*
Required: *no*

## endDate
This date is displayed on the overview page as the end date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the deposit swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the deposit swik  +3 months.

Type : *string*
Format: *YYYY‐MM‐DD*
Control key binding: *no*
Required: *no*

## relativeEndDate
Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks.

Type : *int*
Min. value: 1
Max. value: 365
Control key binding: *no*
Required: *no*

## id
Your cutom booking reference or event ID.

Type : *string*
Control key binding: *no*
Required: *no*

## language
Language in which the overview page is displayed to the end-user.

Type : *string*
Authorized values : *FR, GB, NL, DE, IT, ES*
Default value : *FR*
Format: *ISO 3166-1 alpha-2*
Control key binding: *no*
Required: *no*

## currency
Currency of the transaction.

Type : *string*
Authorized values : *EUR*
Default value : *EUR*
Format: *ISO 4217*
Control key binding: *no*
Required: *no*

## validityCount
Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set.

Type : *int*
Control key binding: *no*
Required: *no*

## linkId
Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http://lelien.swikly.com).

Type : *string*
Control key binding: *yes*
Required: *no*