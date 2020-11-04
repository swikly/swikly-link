The following table lists the parameters that are:
- Posted as a response by Swikly to the callback URL when the transaction is accepted by the end-user and if the Standard Parameter `callBackURL` is set. The data posted can then be processed for internal business purpose. The script you have set as a `callBackURL` endpoint will have to listen to **POST** request data.
Please note that **if your endpoint is down or not reachable**, Swikly will try to POST the transaction payload again 5 times with a 4 hour interval between each attempt.

- Appended to the redirect URL when the transaction is accepted by the end-user and if the Standard Parameter  `redirectURL` is set. The data appended can then be processed for internal business purpose. The script you have set as a `redirectURL` endpoint will have to listen to **GET** request data.
  
In both cases, a `ctrlKey` is also sent to check that business relevant data has not been tempered with by a third party when you receive the posted data on your side.


| Parameter | Description | Format | Control Key Binding
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
status=OK&userId=[swikly-account-userId]&userFirstname=John&userLastname=Doe&userEmail=john.doe%40emailaddress.com&userPhone=%2B33600000000&language=EN&startDate=2020-10-31&endDate=2020-11-07&linkId=link1&description=Deposit%20for%20your%20vacation%20rental%20in%20Paris&descPayment=solde+%C3%A0+payer%2Fbalance&freeText=&totalPaymentAmount=3460&totalDepositAmount=30000&totalReservationAmount=1000&id=MY_REF&contractId=MY_REF&customId=MY_REF&swiklyDepositToken=369fd7f689adff2dc55c8c3b42ec6157&swiklyReservationToken=e577c228101597c67fcac13fb0b8614e&swiklyPayinToken=04e4ddaa93669cbfec0f3831dc0c43f3&ctrlKey=[computed-control-key]&fingerprint=123456978abc&cityTax=100&totalCityTaxAmount=1400&nights=7&adultsNbr=2&childrenNbr=0&checkInTime=15:00&checkOutTime:11:00
```

Each callback and redirect data will be validated by another control key wich enables you to check that the data sent back to you from Swikly has not been tempered with.

This `ctrlKey` parameter is a **SHA256** hash resulting of the concatenation of several parameter values set in a specific order.

| Parameters in the following order |
|---|
| userId |
| id |
| startDate |
| endDate  |
| totalPaymentAmount |
| totalDepositAmount |
| totalReservationAmount |
| swiklyPayinToken |
| swiklyDepositToken |
| swiklyReservationToken |
| freeText |
| Link Secret |

You can compute the control key on your side with the above parameter values and check that the resulting **SHA256** hash of the string matches the `ctrlKey` parameter.

#Using several callback URLs
For internal business purpose you may need Swikly to POST the callback payload on several endpoints. This can be done via the developer section of your Swikly user account.
- You can add as many URL callbacks as you want.
- Callback URLs added in the developer section will behave exactly as a the `callBackURL` parameter.
- You can use callbacks URLs added in the developer section instead or in addition to the  `callBackURL` parameter.



## Adding a callback URL
In the developer section of your Swikly user account, add the callback URL in the last field of the callback list.

Once the URL has been entered, just click on the validation button located on the left of the URL or press your keyboard enter key.

## Updating a callback URL
Once a URL has been added, if you want to change it, just make your changes in the proper field and click on the validation button located on the left of the URL or press your keyboard enter key.

## Deleting a callback URL
If you want to delete a URL, just press the matching callack URL delete button.