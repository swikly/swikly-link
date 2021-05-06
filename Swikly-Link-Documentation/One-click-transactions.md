# One Click Transactions

Depending on your business case, you may need to allow recurring customers to go through Swikly's checkout without re-entering their credit card information.

When this option is activated, an existing customer will land directly on Swikly's Checkout page. The credit card used during the last transaction will be displayed with most digits obfuscated. The customer will then have the following choices :
- Use the recorded card
- Change the card and use another one

If the recorded card doesn't work anymore (lost, expired, etc.) the user will then have to enter new credit card information. 

In order to activate this option you need to contact Swikly's support line : +33 4 20 88 00 48

Once this option activated by Swikly's Support team, at each transaction you will receive the `enduserId` parameter as an additional value in your **[Callback URL and Redirect URL parameters](/Swikly-Link-Documentation/Callback-URL-and-Redirect-URL-parameters)**.

The `enduserId` parameter has to be stored on your side and sent to Swikly when one of your recurring customers initiates a new transaction. The **[link authentication](/Swikly-Link-Documentation/Link-Authentication)** has to be updated accordingly.
