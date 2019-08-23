# Checkout Process

The image below provides an overview of the interaction between merchant platform and the **Skye** Web service

<img src="/img/api/1.png" alt="Skye Checkout Process">

**Step 1**: The customer places an order in a shopping cart providing details such as their first/last name, email address etc. The customer chooses **Skye** as the payment method. When the user clicks submit, the **Skye** web service <a href="/developer_resources/checkout_web_service/#beginipltransaction">BeginIPLTransaction</a> is called.

**Step 2**: **Skye** web service <a href="/developer_resources/checkout_web_service/#beginipltransaction">BeginIPLTransaction</a> returns the TransactionId. Redirect the customer to **Skye** apply url and append the merchant Id and the returned transactionId as parameter.

**Step 3**: **Skye** will redirect to the provided merchant url(ReturnApprovedUrl, ReturnDeclineUrl , ReturnWithdrawUrl or ReturnReferUrl) from **Step 1** once a decision has been made.

**Step 4**: Call web service <a href="/developer_resources/checkout_web_service/#getipltransactionstatus">GetIPLTransactionStatus</a> to confirm status of transaction.

**Step 5**: If status is **APPROVED**, call web service <a href="/developer_resources/checkout_web_service/#commitipltransaction">CommitIPLTransaction</a> to finalise transaction in Skye and also update order as completed on merchant platfrom. Otherwise, update to the appropriate status.


