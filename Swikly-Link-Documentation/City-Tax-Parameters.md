The following table lists the **City tax Parameters** of Swikly's Transaction Link. These parameters can be combined to the **Standard Parameters** in order to request the payment of the city tax by the end-user.

| Parameter | Description |
| ---| --- |
| **[cityTax](#citytax)** | Amount of the city tax in euro cents per adult and per night.|
| **[adultsNbr](#adultsnbr)** | Number of adults over 18 years of age during the stay. This setting is optional if `overviewDisplay` is set to 1.|
| **[childrenNbr](#childrennbr)** | Number of children under 18 years of age during the stay. This setting is optional if `overviewDisplay` is set to 1.|

## cityTax
Amount of the city tax in euro cents per adult and per night. If set, a payment of the city tax of the corresponding amount will be requested alongside any other payment, deposit or reservation request. If not set or set to 0, no city tax payment will be requested.  
The `startDate` and `endDate` parameters are mandatory when a city tax payment is requested.  
If the `adultsNbr` and `childrenNbr` parameters are not set, the `overviewDisplay` parameter has to be set to 1 - default value - and a select box for each option will be presented to the end-user on the **[overview page](/Swikly-Link-Documentation)**.

>Type : *int*  
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

>Type : *int*  
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

>Type : *int*  
Min. value: 0  
Control key binding: *no*  
Required: *yes* if `overviewDisplay` is set to 0.

### Sample usage
The following link will request a deposit of 100 EUR to the end-user as well as a the payment of a city tax of 1 EUR per adult per night:
```
https:/sandbox.swikly.com/checkout/?userId=[swikly-account-userId]&amountDeposit=10000&cityTax=100&startDate=2020-12-08&endDate=2020-12-10&adultsNbr=2&childrenNbr=2&overviewDisplay=0&ctrlKey=[computed-control-key]
```
