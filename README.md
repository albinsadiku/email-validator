# emailValidation

email function for validation/parse

## reason?

 `filter_var` does not validate unicode emails.

## getting started

```sh
composer require emailValidation/email_parse
```

## functions

### email\_parse

parses an email and returns an array with the parts of an email.

```php
$parts = email_parse('user@EXAMPLE.COM');
var_dump($parts);
/*
array(11) {
  ["raw"]=>
  string(16) "user@EXAMPLE.COM"
  ["unicode"]=>
  bool(false)
  ["valid"]=>
  bool(true)
  ["idn_domain"]=>
  string(11) "example.com"
  ["idn_local"]=>
  string(4) "user"
  ["idn_tld"]=>
  string(3) "com"
  ["domain"]=>
  string(11) "example.com"
  ["tld"]=>
  string(3) "com"
  ["local"]=>
  string(4) "user"
  ["safe_email"]=>
  string(16) "user@example.com"
  ["email"]=>
  string(16) "user@example.com"
}
*/


$parts = email_parse('@테스트。テスト');
var_dump($parts);
/*
array(11) {
  ["raw"]=>
  string(26) "@테스트。テスト"
  ["unicode"]=>
  bool(true)
  ["valid"]=>
  bool(true)
  ["idn_domain"]=>
  string(25) "xn--9t4b11yi5a.xn--zckzah"
  ["idn_local"]=>
  string(8) "xn--h28h"
  ["idn_tld"]=>
  string(10) "xn--zckzah"
  ["domain"]=>
  string(19) "테스트.テスト"
  ["tld"]=>
  string(9) "テスト"
  ["local"]=>
  string(4) ""
  ["safe_email"]=>
  string(34) "xn--h28h@xn--9t4b11yi5a.xn--zckzah"
  ["email"]=>
  string(24) "@테스트.テスト"
}
*/
```

### email\_valid

checks if an email is valid/false.  
uses `email_parse` in the background and returns `email` key.

```php
$valid = email_valid('@테스트。テスト');
var_dump($valid);
// string(24) "@테스트.テスト"

// Non valid because of starting dot
$valid = email_valid('.@테스트.テスト');
var_dump($valid);
// bool(false)
```

### email\_safe

checks if an email is valid and returns it in punycode valid/false.  
uses `email_parse` in the background and returns `safe_email` key.

```php
$valid = email_safe('@테스트。テスト');
var_dump($valid);
// string(34) "xn--h28h@xn--9t4b11yi5a.xn--zckzah"

// Non valid because of starting dot
$valid = email_safe('.@테스트.テスト');
var_dump($valid);
// bool(false)
```

## License

MIT
