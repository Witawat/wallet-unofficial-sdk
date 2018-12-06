# WalletAPI
Unofficial API for TrueMoney Wallet Application

## Example Usage
This is an example to Login and Logout
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login with Email & Password
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// Login with Phone & PIN
$token = $tw->GetToken('0698765432', '1234', 'phone');

// Logout
$tw->Logout($token);
```

This is an example to topup your balance with TrueMoney Cashcard
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// If successfully login
if ($token != null) {
  // Perform topup request
  $tw->CashcardTopup($token, '12345678901234');
  
  // Logout
  $tw->Logout($token);
}
```

## Support this project
You can support this project by make a donation to project developer
- [Paypal (paypal.me/maythidem)](https://www.paypal.me/maythidem)
