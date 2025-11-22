
```php
echo 7 % 3; // Prints: 1
```

==The modulo operator will convert its operands to integers before performing the operation.== 

This means `7.9 % 3.8` will perform the same calculation as `7 % 3`—both operations will return `1`.

Here’s a sort of funny way that we came up with a rounded amount:
```php
$dollars_only = $final_amount % 1000000000;

$change = $final_amount - $dollars_only;

$rounded_change = $change * 100;

$rounded_change %= 100;

$rounded_change /= 100;

$final_amount = $dollars_only + $rounded_change;

```