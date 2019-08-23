# Introduction

While shopping on online merchant sites, customers will have the ability to select the Skye payment service during their checkout process. Selecting the Skye payment service, the merchant will first transfer customer information to the Skye system before transferring the customer onto the Skye origination website. Here the customer will enter information necessary to complete the Skye origination process. When the origination process has completed the customer will be transferred back to the merchant checkout page, and if approved, will be able to finalise their online purchase. Upon confirmation of the online purchase the merchant will be credited with the transaction amount. 

The Skye Online product is a revolving line of credit that supports transactions over an agreed minimum amount (usually a few hundred dollars).

## Architecture

The Web Services provided are implemented using the SOAP Web Service standard which is a detailed and well supported standard. To use the Skye Online system a number of Web Services need to be called to setup a transaction and later to check the result of the transaction, and confirm it. 

This process begins by creating an object to hold information about the applicant and the merchant. Once the object has been created on the merchant system, it will be passed to the Skye system to create a new transaction. This process will provide you with a unique identifier for this new transaction. The user is then re-directed to the Skye system to continue their data entry. 

Once the user’s IFOL application has been accepted or rejected, they will be returned to the merchant site and given the option to confirm their choice of the Skye payment method if they have been approved.

Merchants will interact with the Skye system via two components: 

* Skye Web Service 
* Skye Origination website 

## Pre-requisites to integration

Prior to commencing building integration to Skye web services, the following conditions are prefferred:

1. Availability of a test merchant website/environment. Requests for testing integration from a live website will not be entertained.

2.	SSL Certificate for Production Shopping Cart.

3.	SSL certificate for test (preferred). To mimic the production setup as close as possible so that no “new” bugs are  introduced during go-live, it is recommended that the test merchant website (shopping cart at least) have a working SSL certificate and testing is done on SSL .

4.	You have received the correct test credentials from Skye.

5.	Unique order number (preferred). 

6.	Save shopping cart functionality (preferred). At times there might be issues during the final confirmation from the merchant website. In such cases Skye IT can manually settle the application on behalf of a customer. Therefore it is recommended that the merchant have the shopping cart saved with a unique reference that can be retrieved and processed.

7.	Sufficiently long timeout. To avoid issues where your shopping cart may time out while the applicant is completing the finance application. it is recommended that you have a 60 minute timeout on your shopping cart.
