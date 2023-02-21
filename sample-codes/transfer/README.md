# Bank Transfer  ✨
 
To initiate a single transfer,  you will need to send a request to the endpoint below:


> NOTE:
> *Please note that this is just for demonstration purposes and not production code.*
 

## Requirement

Steps for generating a custoemr reserved account.

- You need to authenticate to get bearer token. - See guide [sample-codes/authentication/README.md][l1] 
- You can get your Client ID and Secret from within your Monnify dashboard. If you haven't already, click [here](https://monnify.com/) to sign up on Monnify



## Initiate Transfer (Single)

Below is a sample request for initiating a single transfer:



```php
<?php

$access_token = "<access_token>"; // add you access token here

$postData = array(    
    "amount" => 20,
    "reference" =>"ben9-jlo00hdhdjjdfjoji", // unique transaction reference
    "narration" =>"Test01",
    "destinationBankCode" => "057",
    "destinationAccountNumber" => "2085096393",
    "currency" => "NGN",
    "sourceAccountNumber" => "8016472829",
    "destinationAccountName" => "Marvelous Benji" 
);

$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v2/disbursements/single");
curl_setopt($handler, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_POST, true);
 
$response = curl_exec($handler); 

if($response !==false)
{
  var_dump($response); // you can parse this response to get the response body
}
else {
  print "Could not get a response";
}


 ```
 
  

## Initiate Transfer (Bulk)

Bulk transfers allows you send a single request with a list of disbursements you want to be processed. Below is a sample request for initiating a bulk transfer



```php
<?php

$access_token = "<access_token>"; // add you access token here

$postData = array(     
     "title"  => "Game of Batches",
    "batchReference" =>"batchreference12934",
    "narration" =>"911 Transaction",
    "sourceAccountNumber" => "9624937372",
    "onValidationFailure"  => "CONTINUE",
    "notificationInterval" => 10,
    "transactionList"  => [
    	[
	    	"amount" => 1300,
	    	"reference" =>"Final-Reference-1a",
	    	"narration" =>"911 Transaction",
	    	"destinationBankCode" => "058",
			"destinationAccountName" => "Benjamin Wilson",
	    	"destinationAccountNumber" => "0111946768",
	    	"currency" => "NGN"
    	],
		[
    		"amount" => 570,
	    	"reference" =>"Final-Reference-2a",
	    	"narration" =>"911 Transaction",
	    	"destinationBankCode" => "058",
			"destinationAccountName" => "Benjamin Wilson",
	    	"destinationAccountNumber" => "0111946768",
	    	"currency" => "NGN"
    	],
		[
    		"amount" => 230,
	    	"reference" =>"Final-Reference-3a",
	    	"narration" =>"911 Transaction",
			"destinationAccountName" => "Benjamin Wilson",
	    	"destinationBankCode" => "058",
	    	"destinationAccountNumber" => "0111946768",
	    	"currency" => "NGN"
    	]

   	]
);

$handler = curl_init();
$headers[] = 'Authorization: bearer '.$access_token;
$headers[] = 'Content-Type: application/json';


curl_setopt($handler, CURLOPT_URL, "https://sandbox.monnify.com/api/v2/disbursements/batch");
curl_setopt($handler, CURLOPT_POSTFIELDS, http_build_query($postData));
curl_setopt($handler, CURLOPT_HTTPHEADER,$headers);
curl_setopt($handler, CURLOPT_POST, true);
 
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
