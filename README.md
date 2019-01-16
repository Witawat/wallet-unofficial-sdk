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

This is an example to fetch your account balance
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// If successfully login
if ($token != null) {
  // Fetch Balance
  echo $tw->GetCurrentBalance($token);
  
  // Logout
  $tw->Logout($token);
}
```

This is an example to fetch your profile details
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// If successfully login
if ($token != null) {
  // Fetch Profile
  var_dump($tw->GetProfile($token));
  
  // Logout
  $tw->Logout($token);
}
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

This is an example to fetch transactions/activities in your account
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// If successfully login
if ($token != null) {
  
  // Transaction date range
  $start_date = date('Y-m-d', strtotime('-1 days'));
  $end_date = date('Y-m-d', strtotime('1 days'));
  
  // Perform Fetch
  $activities = $tw->FetchActivities($token, $start_date, $end_date);
  
  foreach($activities as $arr) {
    var_dump($arr);
  }
  
  // Logout
  $tw->Logout($token);
}
```

You can also create a **simple** Transaction ID checker (for receiving money)
```php
use Maythiwat\WalletAPI;
require_once(__DIR__ . '/WalletAPI.php');
$tw = new WalletAPI();

// Login
$token = $tw->GetToken('email@provider.com', 'your_p@ssw0rd');

// If successfully login
if ($token != null) {
  
  // Transaction date range
  $start_date = date('Y-m-d', strtotime('-1 days'));
  $end_date = date('Y-m-d', strtotime('1 days'));
  
  // Perform Fetch
  $activities = $tw->FetchActivities($token, $start_date, $end_date);
  
  foreach($activities as $arr) {
    // Check is paid-in
    if ($arr['original_action'] == 'creditor') {
      $data = $tw->FetchTxDetail($token, $arr['report_id']);
      
      // Transaction ID
      $tx['id'] = $data['section4']['column2']['cell1']['value'];
      
      // Amount
      $tx['amount'] = str_replace(',', '', $data['section3']['column1']['cell1']['value']);
      
      // Then you can check user input and connect to database.
    }
  }
  
  // Logout
  $tw->Logout($token);
}
```

## Support this project
You can support this project by make a donation to project developer
- [Paypal (paypal.me/maythidem)](https://www.paypal.me/maythidem)
