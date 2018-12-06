# WalletAPI
Unofficial API for TrueMoney Wallet Application

```php
use Maythiwat\WalletAPI;
require_once('WalletAPI.php');
$tw = new WalletAPI();

// Login with Email & Password
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// Login with Phone & PIN
$token = $tw->GetToken('0698765432', '1234', 'phone');

// Logout
$tw->Logout($token);
```
