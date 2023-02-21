# Monnify Validate Bank Account  ✨
 
This allows you to check if an account number is a valid NUBAN, and to confirm if the account name is valid. 


> NOTE:
> *Please note that this is just for demonstration purposes and not production code.*
 

## Requirement

Steps for generating a custoemr reserved account.

- You need to authenticate to get bearer token. - See guide [sample-codes/authentication/README.md][l1] 
- You can get your Client ID and Secret from within your Monnify dashboard. If you haven't already, click [here](https://monnify.com/) to sign up on Monnify



## Reserve Account Request (Get an account each for all available partner banks)

If you want to reserve accounts for only preferred partner banks for your customers, you will need to pass "False" for "getAllAvailableBanks" and supply the bank codes of the preferred banks in an array.

```php
<?php

$access_token = "<access_token>"; // add you access token here
$accountNumber = "0068687503"; // 
$bankCode = "232"; // 


$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v1/disbursements/account/validate?accountNumber=$accountNumber&bankCode=$bankCode");
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_RETURNTRANSFER, true);


$response = curl_exec($handler); 

if($response !==false)
{
  var_dump($response); // you can parse this response to get the response body
}
else {
  print "Could not get a response";
}


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
