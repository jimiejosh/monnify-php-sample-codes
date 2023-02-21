# Monnify PHP Sample Codes  ✨
 
This repository contains sample codes on how you Authorize / Authenticate to get bearer token with [Monnify](https://monnify.com/) API in PHP. 

> NOTE:
> *Please note that this is just for demonstration purposes and not production code.*
 
## How to Obtain your API Keys
Your API keys are available on your Monnify Dashboard. You can find it by following the steps below:

- Login to your [Monnify Dashboard](https://app.monnify.com/login).
- Navigate to settings.
- Select API Keys and Webhooks on the settings tab.
- Get your unique API Key and Secret Key.

## Get Token using CURL PHP

```php
<?php

// A very simple PHP example that sends a HTTP POST using CURL to Monnify to get access token


// 1. Get API Key and Secret Key from Monnify Dashboard
$API_Key = "MK_TEST_SAF7HR5F3F";
$Secret_Key = "4SY6TNL8CK3VPRSBTHTRG2N8XXEGC6NL";

$ch = curl_init();

// Concatenate "ApiKey" + ":" +  "SecretKey", then Base 64 encode the string and prefix with the word "Basic". See in next line
$headers = array(
    'Content-Type:application/json',
    'Authorization: Basic '. base64_encode($API_Key . ":" . $Secret_Key) // <---
);
curl_setopt($ch, CURLOPT_HTTPHEADER, $headers);
curl_setopt($ch, CURLOPT_URL,"https://sandbox.monnify.com/api/v1/auth/login");
curl_setopt($ch, CURLOPT_POST, 1);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$output = curl_exec($ch);

curl_close($ch);

$json = json_decode($output, true);
// print_r($json);

$accessToken = $json['responseBody']['accessToken'];

// this is your access token
echo $accessToken;;

// Further processing ...
if ($server_output == "OK") { ... } else { ... }
```
 

## Get Token using Guzzle HTTP PHP Client

Guzzle help you with Making request with PHP. To read more about Guzzle visit https://docs.guzzlephp.org/en/stable/overview.html

```php
<?php
use GuzzleHttp\Client;
use GuzzleHttp\RequestOptions;

// 1. Get API Key and Secret Key from Monnify Dashboard
$userName = 'MK_TEST_SAF7HR5F3F'; // API key
$password = '4SY6TNL8CK3VPRSBTHTRG2N8XXEGC6NL'; // Secret Key

$httpClient = new Client();

$response = $httpClient->post(
    'https://sandbox.monnify.com/api/v1/auth/login',
    [
        RequestOptions::AUTH => [$userName, $password]
    ]
);

$json = (string) $response->getBody();
$json = json_decode($json); // Using this you can access any key like below
$accessToken = $json->responseBody->accessToken; //access key
```
 
 
 
## Get Token using Unirest for PHP – PHP HTTP Client
To read more about Unirest for PHP visit https://github.com/Kong/unirest-php

 ```php
 <?php
 
 // 1. Get API Key and Secret Key from Monnify Dashboard
$API_Key = "MK_TEST_SAF7HR5F3F";
$Secret_Key = "4SY6TNL8CK3VPRSBTHTRG2N8XXEGC6NL";

 Unirest::post(
     "https://sandbox.monnify.com/api/v1/auth/login", 
     array( "Accept" => "application/json",  "Content-Type" => "application/json" ), 
     NULL, 
     $API_Key, 
     $Secret_Key
 )


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
