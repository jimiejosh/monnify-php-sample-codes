# Monnify Customer Reserved Account  ✨
 
This repository contains sample codes on how you can create REserved Account for yur customers on [Monnify](https://monnify.com/) in PHP.

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

$postData = array(     
      "accountReference" => "mN84t584ffgg75t84758478754", // unique reference
           "accountName" => "Damilare Ogunnaike",
          "currencyCode" => "NGN",
          "contractCode" => "8389328412",
         "customerEmail" => "test@tester.com",
                   "bvn" => "2233445566778899",
          "customerName" => "Damilare Ogunnaike",
  "getAllAvailableBanks" => true
);

$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v2/bank-transfer/reserved-accounts");
curl_setopt($handler, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_POST, true);

$response = curl_exec($handler); 

if($response !==false)
{
  var_dump($response); // you can parse this response to get the reserved account details
}
else {
  print "Could not get a response";
}


 ```
 
 
## Reserve Account Request (Get an account for preferred partner bank only)

If you want to reserve accounts for only preferred partner banks for your customers, you will need to pass "False" for "getAllAvailableBanks" and supply the bank codes of the preferred banks in an array.


```php
<?php


$access_token = "<access_token>"; // add you access token here

$postData = array(     
      "accountReference" => "mN84t584ffgg75t84758478754", // unique reference
           "accountName" => "Damilare Ogunnaike",
          "currencyCode" => "NGN",
          "contractCode" => "8389328412",
         "customerEmail" => "test@tester.com",
                   "bvn" => "2233445566778899",
          "customerName" => "Damilare Ogunnaike",
  "getAllAvailableBanks" => false,
        "preferredBanks" => ["035"]
);

$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v2/bank-transfer/reserved-accounts");
curl_setopt($handler, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_POST, true);

$response = curl_exec($handler); 

if($response !==false)
{
  var_dump($response); // you can parse this response to get the reserved account details
}
else {
  print "Could not get a response";
}


 ```
 
 
## Split payments on Reserved Accounts

incomeSplitConfig allows you to use split payments with your reserved accounts by specifying one or more sub-account(s) and a specific percentage of each payment to be credited into each sub-account. IncomeSplitConfig is an array of objects so you can split into multiple sub-accounts per transaction.

Reserve Account Request with SubAccount


```php
<?php


$access_token = "<access_token>"; // add you access token here

$postData = array(     
      "accountReference" => "mN84t584ffgg75t84758478754", // unique reference
           "accountName" => "Damilare Ogunnaike",
          "currencyCode" => "NGN",
          "contractCode" => "8389328412",
         "customerEmail" => "test@tester.com",
                   "bvn" => "2233445566778899",
          "customerName" => "Damilare Ogunnaike",
  "getAllAvailableBanks" => true,
     "incomeSplitConfig" => [
         {
           "subAccountCode" => "MFY_SUB_319452883228",
            "feePercentage" => 10.5,
          "splitPercentage" => 20,
                "feeBearer" => true
         }
      ]
);

$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v2/bank-transfer/reserved-accounts");
curl_setopt($handler, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_POST, true);

$response = curl_exec($handler); 

if($response !==false)
{
  var_dump($response); // you can parse this response to get the reserved account details
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
