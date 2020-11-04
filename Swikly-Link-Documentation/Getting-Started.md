## The Basics

A Swikly Transaction Link is a specific URL created to redirect an end-user to a web form where he has to enter his credit card details to complete a transaction. This specific URL must include: 
- Swikly's checkout root URL according to the **[environment](/Swikly-Link-Documentation/Environments)** (Sandbox or Production) you are working in
- a Swikly account `userId` [parameter](/Swikly-Link-Documentation/Standard-Parameters) based on the **[environment](/Swikly-Link-Documentation/Environments)** (Sandbox or Production) you are working in
- a `ctrlKey` [parameter](/Swikly-Link-Documentation/Standard-Parameters) to **[authenticate](/Swikly-Link-Documentation/Link-Authentication)** the link
- **[Standard Parameters](/Swikly-Link-Documentation/Standard-Parameters)**

##Link Transaction Flow

1. A transaction link must be provided to the end-user (by email, in a website button, etc. depending on your application). 

2. When the end-user clicks on the link, he is redirected to Swikly's checkout process. First on the *Overview Page*, where he has to fill in additional information, and then on the *Checkout Page* where he has to complete the transaction by entering his credit card details in the provided form.
Please note that the *Overview Page* step can be skipped in certain conditions described in the `overviewDisplay` [Standard Parameter](/Swikly-Link-Documentation/Standard-Parameters).

3. Once the transaction completed, the end-user is automatically redirected either to Swikly's *Thank You* page or to a page you have set with the `redirectURL` [Standard Parameter](/Swikly-Link-Documentation/Standard-Parameters).

4. If you have set the `callBackURL` [Standard Parameter](/Swikly-Link-Documentation/Standard-Parameters), your system will receive a POST notification of the successfull transaction as described in **[Callback URL and Redirect URL parameters](/Swikly-Link-Documentation/Callback-URL-and-Redirect-URL-parameters)**.

##Definitions

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Definition  |
|---|---|
|End-User | In Swikly's context, the *End-User* defines the user who ultimately accepts any combination of a deposit, down payment or payment request by entering a valid credit card details in the form provided on Swikly's checkout page. In your business context, the end-user is probably your customer.|
|Overview page | The *Overview Page* is the first page of the checkout process provided by Swikly where the end-user has to enter personal information details such as first name, last name, email address, phone number. Other information related to the city tax and check-in and check out time can also be requested on that page. |
|Checkout page | The *Checkout Page* is the second page of the checkout process provided by Swikly where the end-user enters valid credit card information to complete a transaction. |