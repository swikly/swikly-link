This is [Swikly](https:/www.swikly.com)'s official documentation on how to generate and implement Swikly's transaction links.  
Swikly enables you to generate a transaction link for any transaction request type:

 - Deposit, down payment or payment.
 - Complex transaction requests of any combination.

# Definitions
| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Definition  |
|---|---|
|End-User | In Swikly's context, the *End-User* defines the user who ultimately accepts any combination of a deposit, down payment or payment request by entering a valid credit card details in the form provided on Swikly's checkout page. |
|Overview page | The *Overview Page* is the first page of the checkout process provided by Swikly where the end-user has to enter personal information details such as first name, last name, email address, phone number. Other information related to the city tax and check-in and check out time can also be requested on that page. |
|Checkout page | The *Checkout Page* is the second page of the checkout process provided by Swikly where the end-user enters valid credit card information to complete a transaction. |

# Sandbox and production environments
- ## Sandbox

The sandbox environment enables you to test your links and application integration. All transactions made and accepted in sandbox mode are for testing purpose only. To complete a  transaction from end to end in sandbox mode, you have to use a **[test credit card](#test-credit-cards)**. 

| Environment  | Url  | Usage |
|---|---| --- |
| Sandbox | [https:/sandbox.swikly.com](https:/sandbox.swikly.com) | Test |

- ## Production 

The production environment enables you to go live with your links and application integration. All transactions made and accepted in production are real transactions. To complete a transaction in production mode, you have to use a **real credit card**. 

| Environment  | Url  | Usage |
|---|---| --- |
| Production | [https:/www.swikly.com](https:/www.swikly.com) | Live |

# Authentication

Each transaction link you generate has to be authenticated with a Control Key value set in the `ctrlKey` parameter. This `ctrlKey` is a **SHA256** hash resulting of the concatenation of several parameter values set in a specific order. It allows Swikly to check that important values have not been tempered with.

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

You must have an active Swikly account, a **secret** and a valid Swikly account **userId** to create a custom Swikly Link. Create your account in the **[sandbox environment](#sandbox)** for testing or in the **[production environment](#production)** environment to go live.

Once connected to your Swikly account, go to:  **My Account** > **Developers**. You will find your **Link Secret** and account **userId** in this section.

### Sample usage with the following user
- userId: userId123456789
- Link Secret: mygreatsecret

The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=userId123456789&amountDeposit=10000&ctrlKey=5eec5d8f5cfc236afa3226b9bb3c7c514e6b6b3044bdc9b528b5b2795540be34
```

The `ctrlKey` is computed this way: 

```
String to hash: 10000000userId123456789mygreatsecret
sha256 result: 5eec5d8f5cfc236afa3226b9bb3c7c514e6b6b3044bdc9b528b5b2795540be34
```

---

# Checkout Root

Swikly's Transaction Link redirects the end-user to Swikly's checkout. Swikly's checkout will then process all the parameters set in the link and display the necessary transaction information to the user.

| Environment  | Url  |   |
|---|---| --- |
| Sandbox Checkout | [https://sandbox.swikly.com/checkout](https://sandbox.swikly.com/checkout)  | Test |
| Production Checkout | [https://www.swikly.com/checkout](https://www.swikly.com/checkout) | Live |

---

# Standard Parameters
The following table lists the *Standard Parameters* of Swikly's Transaction Link. Some of these parameters are required, others are optional. Some of them are interdependent. Most of them can be combined together to easily create complex transaction combinations.

| Parameter | Description |
| ---| --- |
| **[userId](#userid)** | Swikly's sandbox or production userId |
| **[amountDeposit](#amountdeposit)** | Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If not set or set to 0, no deposit will be requested. |
| **[amountReservation](#amountreservation)** | Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If not set or set to 0, no down payment will be requested. |
| **[amountPayment](#amountpayment)** | Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If not set or set to 0, no payment will be requested. |
| **[overviewDisplay](#overviewdisplay)** | If set to 0, bypasses the display of the overview page. However, to bypasss the overview page, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also mandatory and will be used to calculate the tourist tax. |
| **[description](#description)** | Text displayed on the overview page of the form describing the purpose of the request. |
| **[freeText](#freetext)** | Optional text field not displayed to the end-user. The `freeText` value is sent back to yor system via the `callBackURL`.|
| **[firstName](#firstName)** | The end-user's first name. This value is displayed as an editable value in the firstname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. |
| **[lastName](#lastname)** | The end-user's last name. This value is displayed as an editable value in the lastname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. |
| **[email](#email)** | The end-user's email address. This value is displayed as an editable value in the email field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. |
| **[phone](#phone)** | The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. |
| **[startDate](#startdate)** | This date is displayed on the overview page as the start date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the reservation swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the reservation swik +3 months. |
| **[endDate](#enddate)** | This date is displayed on the overview page as the end date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the deposit swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the deposit swik  +3 months. |
| **[relativeEndDate](#relativeenddate)** | Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks. |
| **[id](#id)** | Your custom booking reference or event id. |
| **[language](#language)** | Language in which the overview page is displayed. |
| **[currency](#currency)** | currency of the transaction |
| **[validityCount](#validitycount)** | Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set. |
| **[sendEmail](#sendemail)** | Allows you to decide whether to send an e-mail confirming the transaction to the end user. |
| **[linkId](#linkid)** | Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http:/lelien.swikly.com). |
| **[callBackURL](#callbackurl)** | Callback URL to a script that is called when an end-user completes any type of individual transaction or transaction combination. |
| **[redirectURL](#redirecturl)** | Redirects the end-user to the URL set at the end of the transaction process. |
| **[returnURL](#returnurl)** | Displays a Back to Shop button on the transaction success page. This button is linked to the URL defined in `returnURL`. |
| **[cancelURL](#cancelurl)** | Displays a Cancel button on the transaction **[checkout page](#definitions)**. This button is linked to the URL defined in `cancelURL`. |
| **[ctrlKey](#ctrlkey)** | Control key based on the concatanation and hash of multiple parameter values. (cf. [Authentication](#authentication)) |

## userId
Swikly account userId

Type : *string*  
Control key binding: *yes*  
Required: *yes*

### Sample usage
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&ctrlKey=[computed-control-key]
```
---

## amountDeposit
Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If not set or set to 0, no deposit will be requested.

Type : *int*  
Min. value: 0  
Max. value: 250000  
Control key binding: *yes*  
Required: *no*   

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&ctrlKey=[computed-control-key]
```
---

## amountReservation
Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If not set or set to 0, no down payment will be requested.

Type : *int*  
Min. value: 0  
Max. value: 250000  
Control key binding: *yes*  
Required: *no*

### Sample usage
The following link will request a down payment of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&ctrlKey=[computed-control-key]
```
---
## amountPayment
Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If not set or set to 0, no payment will be requested.

Type : *int*  
Min. value: 0  
Max. value: 250000  
Control key binding: *yes*  
Required: *no*

### Sample usage
The following link will request a payment of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&ctrlKey=[computed-control-key]
```
---

## overviewDisplay
If set to 0, bypasses the display of the **[overview page](#definitions)**. However, to bypasss the **[overview page](#definitions)**, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also required and will be used to calculate the tourist tax.

Type : *int*  
Allowed values: 0 or 1  
Default value : 1  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following links will request a payment of 100 EUR and display the **[overview page](#definitions)** to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&overviewDisplay=1&ctrlKey=[computed-control-key]
```
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&ctrlKey=[computed-control-key]
```

The following link will request a payment of 100 EUR and display the **[checkout page](#definitions)** to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&overviewDisplay=0&firstName=John&lastName=Doe&email=john.doe@emailaddress.com&phone=+33600000000&ctrlKey=[computed-control-key]
```

---

## description
Text displayed on the **[overview page](#definitions)** describing the purpose of the request.

Type : *string*  
Control key binding: *no*  
Required: *no*

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and display the description *Deposit for your vacation rental in Paris* on the overview page:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&description=Deposit%20for%20your%20vacation%20rental%20in%20Paris&ctrlKey=[computed-control-key]
```
---

## freeText
Optional text field not displayed to the end-user. The `freeText` value is sent back to your system via the `callBackURL`

Type : *string*  
Control key binding: *yes*  
Required: *no*

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and send back the freeText *My freeText value* via the callBackURL:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&freeText=My%20freeText%20Value&callBackURL=https%3A%2F%2Fwww.mycalbbackurl.com&ctrlKey=[computed-control-key]
```
---

## firstName
The end-user's first name. This value is displayed as an editable value in the firstname field of the **[overview page](#definitions)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *firstname* field of **[overview page](#definitions)** will be prefilled with *John*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&firstName=John&ctrlKey=[computed-control-key]
``` 
---
## lastName
The end-user's last name. This value is displayed as an editable value in the lastname field of the **[overview page](#definitions)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *lastname* field of **[overview page](#definitions)** will be prefilled with *Doe*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&lastName=Doe&ctrlKey=[computed-control-key]
```
---
## email
The end-user's email address. This value is displayed as an editable value in the email field of the **[overview page](#definitions)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *email* field of **[overview page](#definitions)** will be prefilled with *john.doe@emailaddress.com*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&email=john.doe%40emailaddress.com&ctrlKey=[computed-control-key]
```
---

## phone
The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.   

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *phone* field of **[overview page](#definitions)** will be prefilled with the country flag matching (+33) and 060000000:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&phone=%2B33600000000&ctrlKey=[computed-control-key]
```
---

## startDate
This date is displayed on the overview page as the start date of the service provided. If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the reservation swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the reservation swik +3 months.

Type : *string*  
Format: *YYYY‐MM‐DD*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a down payment of 100 EUR to the end-user and set the expiry date of the service provided to *2020-10-31*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&startDate=2020-10-31&ctrlKey=[computed-control-key]
```
The following link will request a deposit of 600 EUR to the end-user and set the start date of the service provided to *2020-10-31*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&startDate=2020-10-31&ctrlKey=[computed-control-key]
```
---

## endDate
This date is displayed on the **[overview page](#definitions)** as the end date of the service provided. If set, this date defines the expiry date of the deposit transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the deposit swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the deposit swik  +3 months.

Type : *string*  
Format: *YYYY‐MM‐DD*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and set the end date of the service provided to *2020-10-31*:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&endDate=2020-10-31&ctrlKey=[computed-control-key]
```
---

## relativeEndDate
Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks.

Type : *int* 
Min. value: 1   
Max. value: 365  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and set the expiry date of the service provided 30 days after the transaction has been accepted:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&relativeEndDate=30&ctrlKey=[computed-control-key]
```
---

## id
Your cutom booking reference or event ID.

Type : *string*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit with an internal refence *MY_REF* and an amount of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&id=MY_REF&amountDeposit=10000&ctrlKey=[computed-control-key]
```
---

## language
Language in which the overview page is displayed to the end-user.

Type : *string*  
Authorized values : *FR, GB, NL, DE, IT, ES*  
Default value : *FR*  
Format: *ISO 3166-1 alpha-2*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user. All the system and interface messages will be displayed in Spanish:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&language=ES&ctrlKey=[computed-control-key]
```
---

## currency
Currency of the transaction.

Type : *string*  
Authorized values : *EUR*  
Default value : *EUR*  
Format: *ISO 4217*  
Control key binding: *no*  
Required: *no*  


### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&currency=EUR&ctrlKey=[computed-control-key]
```
---

## validityCount
Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set.

Type : *int*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user. This link will be inactive once it has been accepted 5 times:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&validityCount=5&ctrlKey=[computed-control-key]
```
---

## sendEmail
Allows you to decide whether to send an e-mail confirming the transaction success to the end-user. This parameter is particularly useful when you integrate Swikly into your own process and want to manage yourself all the notifications sent to the end-users.

Type : *boolean*  
Authorized values : *true*, *false* 
Default value : *true* 
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user who will not receive a confirmation e-mail once the transaction has been accepted:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&sendEmail=false&ctrlKey=[computed-control-key]
```
---

## linkId
Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http:/lelien.swikly.com).

Type : *string*  
Control key binding: *yes*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&linkId=[provided-link-id]&ctrlKey=[computed-control-key]
```
---

## callBackURL
Callback URL to a script that is called when an end-user completes any type of individual transaction or transaction combination. Swikly **posts** the transaction data as described in the *Callback URL Posted Parameters* section to the URL set as `callBackURL`.

Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user and POST the transaction data to the `callBackURL` defined at the end of the transaction process:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&callBackURL=https%3A%2F%2Fwww.mycalbbackurl.com&ctrlKey=[computed-control-key]
```
---

## redirectURL
Redirects the end-user to the URL set at the end of the transaction process. The default Swikly success page will not be displayed.

Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and redirect the end-user to `redirectURL` at the end of the transaction process:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&redirectURL=https%3A%2F%2Fwww.myredirecturl.com&ctrlKey=[computed-control-key]
```
---

## returnURL
Displays a *Back to Shop* button on the transaction success page. This button is linked to the URL defined in `returnURL`.

Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and display a *Back To Shop* button on the success page at the end of the transaction process:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&returnURL=https%3A%2F%2Fwww.myreturnurl.com&ctrlKey=[computed-control-key]
```
---

## cancelURL
Displays a *Cancel* button on the transaction **[checkout page](#definitions)**. This button is linked to the URL defined in `cancelURL`.

Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and display a *Cancel* button on the **[checkout page](#definitions)**:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cancelURL=https%3A%2F%2Fwww.mycancelurl.com&ctrlKey=[computed-control-key]
```
---

## ctrlKey
Control key based on the concatanation and hash of multiple parameter values. (cf. [Authentication](#authentication))

Type : *string*   
Required: *yes*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&ctrlKey=[computed-control-key]
```

# City Tax Parameters
The following table lists the *City tax Parameters* of Swikly's Transaction Link. These parameters can be combined to the *Standard Parameters* in order to request the payment of the city tax by the end-user.

| Parameter | Description |
| ---| --- |
| **[cityTax](#citytax)** | Amount of the city tax in euro cents per adult and per night.|
| **[adultsNbr](#adultsnbr)** | Number of adults over 18 years of age during the stay. This setting is optional if `overviewDisplay` is set to 1.|
| **[childrenNbr](#childrennbr)** | Number of children under 18 years of age during the stay. This setting is optional if `overviewDisplay` is set to 1.|

## cityTax
Amount of the city tax in euro cents per adult and per night. If set, a payment of the city tax of the corresponding amount will be requested alongside any other payment, deposit or reservation request. If not set or set to 0, no city tax payment will be requested.  
The `startDate` and `endDate` parameters are mandatory when a city tax payment is requested.  
If the `adultsNbr` and `childrenNbr` parameters are not set, the `overviewDisplay` parameter has to be set to 1 - default value - and a select box for each option will be presented to the end-user on the **[overview page](#definitions)**.

Type : *int*  
Min. value: 0  
Control key binding: *yes*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user as well as a the payment of a city tax of 1 EUR per adult per night:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cityTax=100&startDate=2020-12-08&endDate=2020-12-10&ctrlKey=[computed-control-key]
```
---

## adultsNbr
Number of adults over 18 years of age during the stay. This parameter is mandatory if the `overviewDisplay` parameter is set to 0 as the calculation of the city tax is based on the the number of adults per night.

Type : *int*  
Min. value: 1  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a deposit of 100 EUR to the end-user as well as a the payment of a city tax of 1 EUR per adult per night:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cityTax=100&startDate=2020-12-08&endDate=2020-12-10&adultsNbr=2&childrenNbr=2&overviewDisplay=0&ctrlKey=[computed-control-key]
```
---

## childrenNbr
Number of children under 18 years of age during the stay. This parameter is mandatory if the `overviewDisplay` parameter is set to 0.

Type : *int*  
Min. value: 0  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a deposit of 100 EUR to the end-user as well as a the payment of a city tax of 1 EUR per adult per night:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cityTax=100&startDate=2020-12-08&endDate=2020-12-10&adultsNbr=2&childrenNbr=2&overviewDisplay=0&ctrlKey=[computed-control-key]
```

# Callback URL and Redirect URL Parameters
The following table lists the parameters that are:
- Posted as a response by Swikly to the callback URL when the transaction is accepted by the end-user and if  `callBackURL` is set. The data posted can then be processed for internal business purpose. The script you have set as a `callBackURL` endpoint will have to listen to **POST** data.

- Appended to the redirect URL when the transaction is accepted by the end-user and if `redirectURL` is set. The data appended can then be processed for internal business purpose. The script you have set as a `redirectURL` endpoint will have to listen to **GET** data.
  
In both cases, a `ctrlKey` is also sent to check that business relevant data has not been tempered with by a third party when you receive the posted data on your side.


| Parameter | Description | Format | Key Binding
| ---| --- | --- | --- |
|status | Set to OK if the transaction is successful. | String | No |
|userId | Business userId. | String | Yes |
|id | Value of the `id` Standard Parameter. | String | Yes |
|contractId | Value of the `id` Standard Parameter. | String | No |
|customId | Value of the `id` Standard Parameter. | String | No |
|userFirstname | Firstname of the end-user as entered on the overview page. | String | No |
|userLastname | Lastname of the end-user as entered on the overview page. | String | No |
|userEmail | Email address of the end-user as set in the `email` standard parameter or as  entered on the overview page. | String | No |
|userTrueEmail | Email address of the end-user as entered on the overview page. | String | No |
|userPhone | Phone number of the end-user as set in the `phone` standard parameter or as  entered on the overview page. | String | No |
|language | Same value as `language` standard parameter. | String | No |
|startDate | Same value as `startDate` standard parameter. | String | Yes |
|endDate | Same value as `endDate` standard parameter. | String | Yes |
|linkId | Same value as `linkId` standard parameter. | String | No |
|description | Same value as `description` standard parameter. | String | No |
|descPayment | Same value as `descPayment` standard parameter. | String | No |
|totalPaymentAmount | Total amount paid by the end-user in cents. | Int | Yes |
|totalDepositAmount | Total deposit amount in cents. | Int | Yes |
|totalReservationAmount | Total down payment amount in cents. | Int | Yes |
|swiklyPayinToken | Swikly generated Id for the payment transaction. | String | Yes |
|swiklyDepositToken | Swikly generated Id for the deposit transaction. | String | Yes |
|swiklyReservationToken | Swikly generated Id for the down payment transaction. | String | Yes |
|swiklyRef | Swikly generated Id for the group of transactions. | String | No |
|ctrlKey | Control key generated to validate the response data. | String | No |
|freeText | Same value as `freeText` standard parameter. | String | Yes |
|fingerprint | Fingerprint of the credit card used by the end-user. | String | No |
|cityTax | Same value as `cityTax` standard parameter. | Int | No |
|adultsNbr | Same value as `adultsNbr` standard parameter. | Int | No |
|childrenNbr | Same value as `childrenNbr` standard parameter. | Int | No |
|nights | Number of nights computed by Swikly from the `startDate` and `endDate` standard parameters. | Int | No |
|totalCityTaxAmount | Total city tax amount paid by the end-user in cents. | Int | No |
|checkInTime | Check-in time declared by the end-user. *Option available upon request* | String | No |
|checkOutTime | Check out time declared by the end-user. *Option available upon request* | String | No |

## Example of callback data

Swikly will **POST** a data string formatted as follows to the callback URL or append that same data string to the redirect URL:
```
status=OK&userId=[swikly-account-userId]&userFirstname=John&userLastname=Doe&userEmail=john.doe%40emailaddress.com&userPhone=%2B33600000000&language=EN&startDate=2020-10-31&endDate=2020-11-07&linkId=link1&description=Deposit%20for%20your%20vacation%20rental%20in%20Paris&descPayment=solde+%C3%A0+payer%2Fbalance&freeText=&totalPaymentAmount=3460&totalDepositAmount=30000&totalReservationAmount=1000&id=MY_REF&contractId=MY_REF&customId=MY_REF&swiklyDepositToken=369fd7f689adff2dc55c8c3b42ec6157&swiklyReservationToken=e577c228101597c67fcac13fb0b8614e&swiklyPayinToken=04e4ddaa93669cbfec0f3831dc0c43f3&controlKey=[computed-control-key]&fingerprint=123456978abc&cityTax=100&totalCityTaxAmount=1400&nights=7&adultsNbr=2&childrenNbr=0&checkInTime=15:00&checkOutTime:11:00
```

Each callback and redirect data will be validated by another control key wich enables you to check that the data sent back to you from Swikly has not been tempered with.

This `ctrlKey` parameter is a **SHA256** hash resulting of the concatenation of several parameter values set in a specific order.

| Parameters in the following order |
|---|
| userId |
| id |
| endDate  |
| startDate |
| totalPaymentAmount |
| totalDepositAmount |
| totalReservationAmount |
| swiklyPayinToken |
| swiklyDepositToken |
| swiklyReservationToken |
| freeText |
| Link Secret |

You can compute the control key on your side with the above parameter values and check that the resulting **SHA256** hash of the string matches the `ctrlKey` parameter.

---

# Test Credit Cards

These credit cards are to be used in the **[sandbox environment](#sandbox)** for testing purpose only.  
**Important**: Some of these test cards may be down or not responding properly from time to time. In that case, use another test card.

| Card Number | Expiry Date | CVV | 3DS code |
| --- | --- | --- | --- |
|3569990000000132 | Date in the future | 123 | secret3 |
|3569990000000157 | Date in the future | 123 | secret3 |
|4970105715165150 | Date in the future | 123 | FRATEST1 |
|4970105444347681 | Date in the future | 123 | FRATEST2 |
