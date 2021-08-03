# Vandar Laravel Package
This Laravel package allows you to connect to Vandar payment services. See vandar.io for more info.

## Installation
This package can be installed through Laravel:
```bash
composer require maryamnbyn/vandar-laravel
```
Add vandar configuration to `config/services.php`:
```php
 'vandar' => [
        'api' => 'your api key',
        'test' => false
    ]
```
You can get your api key at Vandar Dashboard

## Usage
In every class where Vandar is used, you need to use the Vandar facade:
```php
use Vandar\Laravel\Facade\Vandar;
```
Then, the payment requests can be sent like this:
```php
$result = Vandar::request($amount, $callback, $mobile = null, $factorNumber = null, $description = null);
```
Further information on the responses is available on [Vandar Documentation](https://docs.vandar.io), but keep in mind that you need to store the `$result['token']` to verify the payment later on.

After this, you may redirect the user to the payment service using one of these methods, note that token is optional:
```php
Vandar::redirect($token);
Vandar::redirectUrl($token);
```
After the user made the payment, Vandar will redirect the user to the callback specified above with a token in url. you can verify payment by passing the token to the `verify` method:
```php
$token=$_GET['token']; // You can also use $request->get('token') in the scope of a laravel controller
$result = Vandar::verify($token);
```

for get info of transaction you can make requestInfo method and send token for that then you can get information ; <br>
To get updates on any transactions you may have created, you may use the `requestInfo` method along with the token you stored:
```php
$result = Vandar::requestInfo($token);
```

## Contribution
Pull-requests fixing bugs or adding to the documentation are very appreciated!

## License
This project is licensed under the GPL-3, see LICENSE for more information.