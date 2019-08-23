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
TransactionInformation **Required**         | This parameter contains all the information to be passed to the Skye system. Such as the applicant’s name and merchant site return URL. | TransactionData
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