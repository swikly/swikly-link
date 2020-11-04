The following table lists the **Standard Parameters** of Swikly's Transaction Link. Some of these parameters are required, others are optional. Some of them are interdependent. Most of them can be combined together to easily create complex transaction combinations. These parameters have to be appended to the **[checkout URL](/Swikly-Link-Documentation/Environments)** as **GET request parameters**.

| Parameter | Description |Type | Required |
| ---| --- | --- | --- |
| **[userId](#userid)** | Swikly's sandbox or production userId | string | yes |
| **[amountDeposit](#amountdeposit)** | Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If not set or set to 0, no deposit will be requested. | int | no
| **[amountReservation](#amountreservation)** | Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If not set or set to 0, no down payment will be requested. | int | no |
| **[amountPayment](#amountpayment)** | Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If not set or set to 0, no payment will be requested. | int | no
| **[overviewDisplay](#overviewdisplay)** | If set to 0, bypasses the display of the overview page. However, to bypasss the overview page, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also mandatory and will be used to calculate the tourist tax. | int | no |
| **[description](#description)** | Text displayed on the overview page of the form describing the purpose of the request. | string | no |
| **[freeText](#freetext)** | Optional text field not displayed to the end-user. The `freeText` value is sent back to your system via the `callBackURL`.| string | no |
| **[firstName](#firstName)** | The end-user's first name. This value is displayed as an editable value in the firstname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. | string | no |
| **[lastName](#lastname)** | The end-user's last name. This value is displayed as an editable value in the lastname field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. | string | no |
| **[email](#email)** | The end-user's email address. This value is displayed as an editable value in the email field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. | string | no |
| **[phone](#phone)** | The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty. | string | no |
| **[startDate](#startdate)** | If set, this date defines the start of the rental. If not set, we will use the acceptation date as the start of the rental. This value is not used for a reservation swik nor for any calculation. The start date is used for information only and statistical purpose. | string | no |
| **[endDate](#enddate)** | If set, this date defines the expiry date of the reservation transaction. If not set, the `relativeEndDate` parameter is used to define the validity period of the deposit swik. If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set at the date of acceptation of the deposit swik  +3 months. | string | no |
| **[relativeEndDate](#relativeenddate)** | Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks added to the reclaim delay | int | no |
| **[id](#id)** | Your custom booking reference or event id. | string | no |
| **[language](#language)** | Language in which the overview page is displayed. | string | no |
| **[currency](#currency)** | currency of the transaction | string | no |
| **[validityCount](#validitycount)** | Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set. | int | no |
| **[sendEmail](#sendemail)** | Allows you to decide whether to send an e-mail confirming the transaction to the end user. | boolean | no |
| **[linkId](#linkid)** | Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http:/lelien.swikly.com). | string | no |
| **[callBackURL](#callbackurl)** | Callback URL to a script that is called when an end-user completes any type of individual transaction or transaction combination. | string | no |
| **[redirectURL](#redirecturl)** | Redirects the end-user to the URL set at the end of the transaction process. | string | no |
| **[returnURL](#returnurl)** | Displays a Back to Shop button on the transaction success page. This button is linked to the URL defined in `returnURL`. | string | no |
| **[cancelURL](#cancelurl)** | Displays a Cancel button on the transaction **[checkout page](/Swikly-Link-Documentation)**. This button is linked to the URL defined in `cancelURL`. | string | no |
| **[ctrlKey](#ctrlkey)** | Control key based on the concatanation and hash of multiple parameter values. (cf. [Authentication](/Swikly-Link-Documentation/Link-Authentication)) | string | yes |

## userId
Swikly account userId

>Type : *string*  
Control key binding: *yes*  
Required: *yes*

### Sample usage
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&ctrlKey=[computed-control-key]
```
---

## amountDeposit
Amount of the deposit transaction in euro cents. If set, a deposit of the corresponding amount will be requested. If not set or set to 0, no deposit will be requested.

>Type : *int*  
Min. value: 0  
Max. value: 250000  
Control key binding: *yes*  
Required: *no*   

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&ctrlKey=[computed-control-key]
```
---

## amountReservation
Amount of the down payment transaction in euro cents. If set, a down payment of the corresponding amount will be requested. If not set or set to 0, no down payment will be requested.

>Type : *int*  
Min. value: 0  
Max. value: 250000  
Control key binding: *yes*  
Required: *no*

### Sample usage
The following link will request a down payment of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&ctrlKey=[computed-control-key]
```
---
## amountPayment
Amount of the payment transaction in euro cents. If set, a payment of the corresponding amount will be requested. If not set or set to 0, no payment will be requested.

>Type : *int*  
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
If set to 0, bypasses the display of the **[overview page](/Swikly-Link-Documentation)**. However, to bypasss the **[overview page](/Swikly-Link-Documentation)**, the following parameters are required: `firstName`, `lastName`, `email`, `phone`. If the `cityTax` parameter is set, the `adultsNbr` and `childrenNbr` parameters are also required and will be used to calculate the tourist tax.

>Type : *int*  
Allowed values: 0 or 1  
Default value : 1  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following links will request a payment of 100 EUR and display the **[overview page](/Swikly-Link-Documentation)** to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&overviewDisplay=1&ctrlKey=[computed-control-key]
```
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&ctrlKey=[computed-control-key]
```

The following link will request a payment of 100 EUR and display the **[checkout page](/Swikly-Link-Documentation)** to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountPayment=10000&overviewDisplay=0&firstName=John&lastName=Doe&email=john.doe@emailaddress.com&phone=+33600000000&ctrlKey=[computed-control-key]
```

---

## description
Text displayed on the **[overview page](/Swikly-Link-Documentation)** describing the purpose of the request.

>Type : *string*  
Control key binding: *no*  
Required: *no*

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and display the description *Deposit for your vacation rental in Paris* on the overview page:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&description=Deposit%20for%20your%20vacation%20rental%20in%20Paris&ctrlKey=[computed-control-key]
```
---

## freeText
Optional text field not displayed to the end-user. The `freeText` value is sent back to your system via the `callBackURL`

>Type : *string*  
Control key binding: *yes*  
Required: *no*

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and send back the freeText *My freeText value* via the callBackURL:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&freeText=My%20freeText%20Value&callBackURL=https%3A%2F%2Fwww.mycalbbackurl.com&ctrlKey=[computed-control-key]
```
---

## firstName
The end-user's first name. This value is displayed as an editable value in the firstname field of the **[overview page](/Swikly-Link-Documentation)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

>Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *firstname* field of **[overview page](/Swikly-Link-Documentation)** will be prefilled with *John*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&firstName=John&ctrlKey=[computed-control-key]
``` 
---
## lastName
The end-user's last name. This value is displayed as an editable value in the lastname field of the **[overview page](/Swikly-Link-Documentation)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

>Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *lastname* field of **[overview page](/Swikly-Link-Documentation)** will be prefilled with *Doe*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&lastName=Doe&ctrlKey=[computed-control-key]
```
---
## email
The end-user's email address. This value is displayed as an editable value in the email field of the **[overview page](/Swikly-Link-Documentation)**. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

>Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *email* field of **[overview page](/Swikly-Link-Documentation)** will be prefilled with *john.doe@emailaddress.com*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&email=john.doe%40emailaddress.com&ctrlKey=[computed-control-key]
```
---

## phone
The end-user's phone number. This value is displayed as an editable value in the phone field of the overview page. If the `overviewDisplay` parameter is set at  0, this parameter is required and cannot be empty.

>Type : *string*  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.   

### Sample usage
The following link will request a down payment of 100 EUR to the end-user. The *phone* field of **[overview page](/Swikly-Link-Documentation)** will be prefilled with the country flag matching (+33) and 060000000:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&phone=%2B33600000000&ctrlKey=[computed-control-key]
```
---
## Date definition and swik expiration 

The acceptation date (`acceptationDate`) is the date where your customer accept the swik and secure is deposit in Swikly.

The reclaim delay (`reclaimDelay`) is an internal parameter set to 20 days by default and can be modified only by the Swikly support team upon request.

The expiry date (`expiryDate`) is defined as the date from where it will not be possible to request a reclaim anymore. Expiry date is linked to the end date since as followed : `expiryDate = endDate + reclaimDelay`

End date is the end of a rental for security deposit and is the appointment date for a swik no-show.

## startDate
If set, this date defines the start of the rental. If not set, we will use the acceptation date as the start of the rental. This value is not used for a reservation swik nor for any calculation. The start date is used for information only and statistical purpose.

>Type : *string*  
Format: *YYYY‐MM‐DD*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a down payment of 100 EUR to the end-user and set the expiry date of the service provided to *2020-10-31*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountReservation=10000&startDate=2020-10-31&ctrlKey=[computed-control-key]
```
The following link will request a deposit of 600 EUR to the end-user and set the start date of the service provided to *2020-10-31*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&startDate=2020-10-31&ctrlKey=[computed-control-key]
```
---

## endDate
If set, this date defines the end of the rental for a security deposit or the appointment date for a reservation swik. This value defines the expiry date of the swik as follow : 

`expiryDate = endDate + reclaimDelay`

if not set, the `relativeEndDate` delay parameter is used to define the validity period of the swik as follow : 

`expiryDate = acceptationDate + relativeEndDate + reclaimDelay`

The reclaim delay (`reclaimDelay`) is an internal parameter set to 20 days by default and can be modified only by the Swikly support team upon request.

If the `relativeEndDate` parameter is not defined either, the expiry date is automatically set as follow : 
`expiryDate = acceptationDate + 90 days + reclaimDelay`

>Type : *string*  
Format: *YYYY‐MM‐DD*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and set the end date of the service provided to *2020-10-31*:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&endDate=2020-10-31&ctrlKey=[computed-control-key]
```
---

## relativeEndDate
Number of days of validity of a deposit or reservation swik from the validation of the swik by the end-user aka the acceptation date. The `startDate` and `endDate` parameters are taken into account first and foremost when defining the expiry date. If none of these 3 parameters is defined, the expiration of the swiks is set at + 3 months from the date of validation of the swiks and added to the reclaim delay.

>Type : *int* 
Min. value: 1   
Max. value: 365  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 600 EUR to the end-user and set the expiry date of the service provided 30 days after the transaction has been accepted:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=60000&relativeEndDate=30&ctrlKey=[computed-control-key]
```
---

## id
Your cutom booking reference or event ID.

>Type : *string*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit with an internal refence *MY_REF* and an amount of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&id=MY_REF&amountDeposit=10000&ctrlKey=[computed-control-key]
```
---

## language
Language in which the overview page is displayed to the end-user.

>Type : *string*  
Authorized values : *FR, EN, NL, DE, IT, ES*  
Default value : *FR*  
Format: *ISO 3166-1 alpha-2*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user. All the system and interface messages will be displayed in Spanish:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&language=ES&ctrlKey=[computed-control-key]
```
---

## currency
Currency of the transaction.

>Type : *string*  
Authorized values : *EUR*  
Default value : *EUR*  
Format: *ISO 4217*  
Control key binding: *no*  
Required: *no*  


### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&currency=EUR&ctrlKey=[computed-control-key]
```
---

## validityCount
Allows you to limit the number of times the link is used. This parameter can only be used if the `id` parameter is set.

>Type : *int*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user. This link will be inactive once it has been accepted 5 times:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&validityCount=5&ctrlKey=[computed-control-key]
```
---

## sendEmail
Allows you to decide whether to send an e-mail confirming the transaction success to the end-user. This parameter is particularly useful when you integrate Swikly into your own process and want to manage yourself all the notifications sent to the end-users.

>Type : *boolean*  
Authorized values : *true*, *false* 
Default value : *true* 
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user who will not receive a confirmation e-mail once the transaction has been accepted:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&sendEmail=false&ctrlKey=[computed-control-key]
```
---

## linkId
Id of the link. Defines the fee and the configuration of the request (Id provided by Swikly following a request made from http:/lelien.swikly.com).

>Type : *string*  
Control key binding: *yes*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&linkId=[provided-link-id]&ctrlKey=[computed-control-key]
```
---

## callBackURL
Callback URL to a script that is called when an end-user completes any type of individual transaction or transaction combination. Swikly **posts** the transaction data as described in the *Callback URL Posted Parameters* section to the URL set as `callBackURL`.

>Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user and POST the transaction data to the `callBackURL` defined at the end of the transaction process:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&callBackURL=https%3A%2F%2Fwww.mycalbbackurl.com&ctrlKey=[computed-control-key]
```
---

## redirectURL
Redirects the end-user to the URL set at the end of the transaction process. The default Swikly success page will not be displayed.

>Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and redirect the end-user to `redirectURL` at the end of the transaction process:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&redirectURL=https%3A%2F%2Fwww.myredirecturl.com&ctrlKey=[computed-control-key]
```
---

## returnURL
Displays a *Back to Shop* button on the transaction success page. This button is linked to the URL defined in `returnURL`.

>Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and display a *Back To Shop* button on the success page at the end of the transaction process:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&returnURL=https%3A%2F%2Fwww.myreturnurl.com&ctrlKey=[computed-control-key]
```
---

## cancelURL
Displays a *Cancel* button on the transaction **[checkout page](https://dev.azure.com/swikly/swikly-link/_wiki/wikis/swikly-link-documentation.wiki/23/Definitions)**. This button is linked to the URL defined in `cancelURL`.

>Type : *string*  
Format: *Valid URL*  
Control key binding: *no*  
Required: *no*  

### Sample usage
The following link will request a deposit of 100 EUR and display a *Cancel* button on the **[checkout page](https://dev.azure.com/swikly/swikly-link/_wiki/wikis/swikly-link-documentation.wiki/23/Definitions)**:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cancelURL=https%3A%2F%2Fwww.mycancelurl.com&ctrlKey=[computed-control-key]
```
---

## ctrlKey
Control key based on the concatanation and hash of multiple parameter values. (cf. [Authentication](/Swikly-Link-Documentation/Link-Authentication))

>Type : *string*   
Required: *yes*  

### Sample usage
The following link will request a deposit of 100 EUR to the end-user:
```
https://sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&ctrlKey=[computed-control-key]
```
