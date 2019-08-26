# Checkout web services

The primary purpose of the Skye web service is to expose key functionalities of the Skye system to merchants. Using the Skye web service merchants can initiate, retrieve, confirm and cancel their customer’s Skye transactions. 
The Skye web services are only accessible by registered merchants.

To be able to call the web services, you need to have the following:

* Merchant Id
* Secret Key
* Operator Id
* Password
* Product Code

There are 4 main methods available in the Skye Web Service: 

## BeginIPLTransaction

This method is used to confirm, the connectivity, pass information about the applying applicant and initiate a new online credit transaction. 

### Method Inputs

 Parameter | Description | Data Type 
-----------|-------------|-----------
TransactionInformation **Required**         | This parameter contains all the information to be passed to the Skye system. Such as the applicant’s name and merchant site return URL. | <a href="/developer_resources/checkout_web_service/#transactiondata-object-type">TransactionData</a>
SecretKey **Required**         | This parameter contains a secret key that will be provided by Skye IT and will need to be passed to get a transaction ID from the Skye Systems | String


### Method Output

If this method successfully runs (no exceptions are passed to your system), a string value containing the unique transaction ID will be returned. This ID is used for all future method calls relating to this Skye transaction.

### Method Specification

The method input and output specification can be found here: [https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=BeginIPLTransaction](https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=BeginIPLTransaction)


## GetIPLTransactionStatus

This method is used to query the status of the transaction for a given transaction ID (given to you when you call BeginIPLTransaction).

### Method Inputs

 Parameter | Description | Data Type 
-----------|-------------|-----------
TransactionID **Required**         | This is the unique transaction ID that was returned from the BeginIPLTransaction method. | String
MerchantId **Required**         | Your unique merchant id that was provided to you for the Skye service. | String


### Method Output

This method will return a string value of the current status of this transaction.

### Method Specification

The method input and output specification can be found here: [https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=GetIPLTransactionStatus](https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=GetIPLTransactionStatus)

## CommitIPLTransaction

This method is used to commit the transaction upon final confirmation of the order by the customer.

### Method Inputs

 Parameter | Description | Data Type 
-----------|-------------|-----------
TransactionID **Required**         | This is the unique transaction ID that was returned from the BeginIPLTransaction method. | String
MerchantId **Required**         | Your unique merchant id that was provided to you for the Skye service. | String

### Method Output

This method will return a Boolean value of true if the commit succeeded or false if it failed. If a transaction isn't committed successfully, it will be withdrawn automatically.

### Method Specification

The method input and output specification can be found here:
[https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=CommitIPLTransaction](https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=CommitIPLTransaction)

## GetIPLTransaction

This is an optional method which can be used to return all the information passed through to the Skye system (including the Skye Application ID). 

### Method Inputs

 Parameter | Description | Data Type 
-----------|-------------|-----------
TransactionID **Required**         | This is the unique transaction ID that was returned from the BeginIPLTransaction method. | String
MerchantId **Required**         | Your unique merchant id that was provided to you for the Skye service. | String

### Method Output

This method will return a TransactionData object of the current Skye transaction, which contains all the information that was passed in the BeginIPLTransaction method call.

### Method Specification

The method input and output specification can be found here: [https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=GetIPLTransaction](https://applications.flexicards.com.au/IPL_service/ipltransaction.asmx?op=GetIPLTransaction)

## TransactionData Object Type

The TransactionData object is a complex object type that is passed to the BeginIPLTransaction method in order to load applicant details and information about the merchant. 

This object contains the following values, most of these are optional (with different requirements for different products), though if customer details are available they will be automatically used in the Skye screens to make the application process easier for the customer: 

 Name | Description | Valdiation | Required?
------|-------------|------------|----------
MerchantId | The merchant id that has been provided to you by Skye. | | Yes
OperatorId | Operator ID that has been provided to you by Skye. | | Yes
Password | Password that has been provided to you by Skye. *NB: DO NOT PASS THE ENCRYPTED PASSWORD, that is only used for the redirect.*| | Yes
CreditProduct | | | Yes
Offer | **One** of the Valid Offer ID’s provided to you by Skye | | Yes
OrderNumber | The merchant’s identifier for this application | | No
Description | The description of the transaction | Not used yet | No
Amount | The amount of  the transaction | A numeric value above the agreed minimum, and below the agreed maximum (a range of 500 to 6000 is normal, but can be extended). | Yes
ExistingCustomer | Existing customer flag to indicate if the applicant is a returning customer of the retailer. | Boolean | Yes
Title | The salutation of the applicant. | Must be one of the following values: Mr, Miss, Ms, Mrs, Dr, Prof, Rev, Sir, Unknown | Can be blank
FirstName | The first given name of an applicant | 2 - 32 characters | Can be blank
MiddleName | The middle name(s) of an applicant | 1 - 32 characters | Optional
Surname | The surname of an applicant. | 2 - 32 characters | Can be blank
BillingAddress | Holds the billing address details of an applicant | See [AddressDetails Object Type](/developer_resources/checkout_web_service/#addressdetails-object-type) | Yes
DeliveryAddress | Holds the delivery address of an applicant | See AddressDetails Object Type | Yes
WorkPhoneArea | Area code for a work phone number | 2 numbers starting with a 0 | Required if WorkPhoneNumber supplied
WorkPhoneNumber | Phone number of a work phone | 8 digits long | No
HomePhoneArea | Area code for a home phone number | 2 numbers starting with a 0 | Required if HomePhoneNumber supplied
MobilePhoneNumber | Applicant's mobile number | 10 numbers long, must start '04' | No
EmailAddress | Applicant's email address | Must be a valid email address | No
ReturnApprovedUrl | The return web address back to the merchant site when the application is APPROVED. If you add “transaction=[TRANSACTIONID]” to the end then it will be replaced with the actual Transaction ID upon returning. | Must be a valid URL to return back to | Yes
ReturnDeclineUrl | The return web address back to the merchant site when the application is DECLINED. If you add “transaction=[TRANSACTIONID]” to the end then it will be replaced with the actual Transaction ID upon returning. | Must be a valid URL to return back to | Yes
ReturnWithdrawUrl | The return web address back to the merchant site when the application is WITHDRAWN by the customer. If you add “transaction=[TRANSACTIONID]” to the end then it will be replaced with the actual Transaction ID upon returning. | Must be a valid URL to return back to | Yes

## AddressDetails Object Type

The AddressDetails object is a complex object type that is passed to the [BeginIPLTransaction](/developer_resources/checkout_web_service/#beginipltransaction) method inside a [TransactionData object](/developer_resources/checkout_web_service/#transactiondata-object-type), which holds information about an applicant’s address. 

This object contains the following values:

 Name | Description | Valdiation | Required? 
------|-------------|------------|-----------
AddressType | The type of address supplied | Must be one of: Residential or Delviery | Yes
UnitNumber | Address unit number | 1 - 8 characters long | No
StreetNumber | Address street number | 1 - 8 characters long | Can be blank
StreetName | Address street name | 2 - 64 characters long | Can be blank
StreetType | Address street type | Must be a valid street type. Please see Street type codes. | Can be blank
Suburb | Address suburb name | 2 - 64 characters long | Can be blank
State | State of an address | Must be one of the followign values: NSW, VIC, TAS, WA, SA, ACT, NT, QLD | Can be blank
Postcode | Address postcode | 4 digits | Can be blank

## Street Type Code

The street type supplied with addresses MUST be one of these; any other will cause the application to be declined.



