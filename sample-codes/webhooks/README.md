# Monnify Webhooks  ✨
 
This repository contains sample codes on how you can implement  [Monnify](https://monnify.com/) Webhooks in PHP. We have made this example below as simple as possible to show you the steps necesary to implement webhook.

> NOTE:
> *Please note that this is just for demonstration purposes and not production code.*
 
## Sample PHP webhook implementation



```php
<?php

// IP Whitelist - Verify IP address against monnify IP  35.242.133.146
$ip = ($_SERVER['REMOTE_ADDR'])?$_SERVER['REMOTE_ADDR']:$_SERVER['REMOTE_HOST'];
if( $ip != "35.242.133.146") die("Invalid IP");

// get raw json request string 
//{"eventData":{"product":{"reference":"111222333","type":"OFFLINE_PAYMENT_AGENT"},"transactionReference":"MNFY|76|20211117154810|000001","paymentReference":"0.01462001097368737","paidOn":"17/11/2021 3:48:10 PM","paymentDescription":"Mockaroo Jesse","metaData":{},"destinationAccountInformation":{},"paymentSourceInformation":{},"amountPaid":78000,"totalPayable":78000,"offlineProductInformation":{"code":"41470","type":"DYNAMIC"},"cardDetails":{},"paymentMethod":"CASH","currency":"NGN","settlementAmount":77600,"paymentStatus":"PAID","customer":{"name":"Mockaroo Jesse","email":"111222333@ZZAMZ4WT4Y3E.monnify"}},"eventType":"SUCCESSFUL_TRANSACTION"}
$raw_request = file_get_contents('php://input');



// your Secret Key founf in your monnidy dashboard, developer menu
$SECRET_KEY = '91MUDL9N6U3BQRXBQ2PJ9M0PW4J22M1Y';

// next, we need to compute and compare hash sent via header as "monnify-signature" is same as hash we generate using our secret key and the request payload. If it is not then the request in rejected
$signature = $_SERVER['HTTP_MONNIFY_SIGNATURE']; // monnify-signature is sent as an header to your webhook endpoint, we get the value and store in this variable
$computedHash = hash_hmac('sha512', $raw_request, $SECRET_KEY); // hash generated
if( $computedHash != $signature) die("invalid Hash");


echo "OK";

// parse request to array
$request_array = json_decode( $raw_request );


// Don't forget to Check for duplicate notifications: When a new notification is received, always check that this has not been processed before giving value bfore, you can do this by tracing all notification with your own reference and alo monnify reference and update status once it has been proceesed

// Process your business logic here... give user value.. that's all!



 ```
 
 
## Development

Want to contribute? Great! Send a a mail to integration-support@monnify.com

## License
**Free Software!**
The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[link-author]: https://jimiejosh.com
 
   [l1]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/authentication/README.md>
   [l2]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/webhooks/README.md>
   [l3]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/reservedaccount/README.md>
   [l4]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/bankverification/README.md>
   [l5]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/transfer/README.md>
   [l6]: <https://github.com/jimiejosh/monnify-php-sample-codes/tree/master/sample-codes/card/README.md>
