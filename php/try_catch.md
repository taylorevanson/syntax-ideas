```php
<?php
$file = NULL;
$path = './test.txt';

try unlink($path);

try $file = file_get_contents($path);
if($file) {
    //...
}

try $file = file_get_contents($path);
try $file = file_get_contents($path); catch function(e) {
    //...
}

$errorHandler = function(e) {
    newrelic_send_error(e);
    throw e;
};
try $file = file_get_contents($path); catch $errorHandler;
try $file = file_get_contents($path); catch $file = file_get_contents('./default.txt');
```