# Laravel API wrapper for PCA Predict formerly Postcode Anywhere

[![Build Status](https://travis-ci.org/alexpechkarev/postcode-anywhere.svg?branch=master)](https://travis-ci.org/alexpechkarev/postcode-anywhere)

This wrapper simplifies process of making API calls to [**PostcodeAnywhere**](http://www.postcodeanywhere.co.uk/)  web services.
Single line of code within your [**Laravel**](http://laravel.com/) application that's all it takes.


Dependency
------------
[**PHP cURL**] (http://php.net/manual/en/curl.installation.php) required


Installation
------------

To install issue following command in console
```
composer require alexpechkarev/postcode-anywhere:dev-master
```

Alternatively edit `composer.json` by adding following line and issue `composer update` command in console.

```php
"alexpechkarev/postcode-anywhere": "dev-master"
```


Configuration
-------------

Once installed, register Laravel service provider, in your `config/app.php`:

```php
'providers' => [
	...
    'PostcodeAnywhere\PAServiceProvider',
]

'aliases' => [
	...
    'PA' => 'PostcodeAnywhere\PAFacade' ,
]
```

Publish configuration file and don't forget to replace service key with your own:

```php 
    php artisan vendor:publish
``` 



Configuration file have multidimensional array 'services' that defines web services by type 'find' and 'retrieve' and store each services request path. Feel free to add / remove any other PCA Predict services. 


Usage
-----
Here is an example of making call to find address records for the given postcode. 
See API documentation [***PostcodeAnywhere Interactive FindByPostcode (v1.00)***](http://www.postcodeanywhere.co.uk/support/webservice/postcodeanywhere/interactive/findbypostcode/1/) for required parameters and response.

Within your application call `\PA::getResponse( array $param )` with array of parameters. 
```
$param = [
	'action' => 'Web Service',
	'parameters' => 'array of parameters for Web Service called'
];
```

Example:
```
$param = [
	'find' => 'FindByPostcode', // perform 'find' action calling 'FindByPostcode' web service 
	'param' => ['postcode'=>'SW1A 1AA', 'endpoint'=>'json'] // parameters for web service called
];
```

Note: defaulted to `json` when `endpoint` parameter ommited.

```php
$response = \PA::getResponse( $param );
```


Here is another example of retrieving full address details based on the id. 
See API documentation [***PostcodeAnywhere Interactive RetrieveById (v1.30)***](http://www.postcodeanywhere.co.uk/support/webservice/postcodeanywhere/interactive/retrievebyid/1.3/) for required parameters and response.

```php
$param = [
	'retrieve'=>'RetrieveById', 
        'param'=>['id'=>'23747212.00'] 
];

$response = \PA::getResponse( $param );
```



Support
-------

[Found errors or to suggest improvements please open an issue on GitHub](https://github.com/alexpechkarev/postcode-anywhere/issues)


License
-------

Laravel API wrapper for PCA Predict formerly Postcode Anywhere is released under the MIT License. See the bundled
[LICENSE](https://github.com/alexpechkarev/postcode-anywhere/blob/master/LICENSE)
file for details.
