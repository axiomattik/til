# Echo Without Echo in PHP

PHP provides various I/O streams under `php://`, which means it is possible to write an echo program without touching the `echo` function.


```
// echo.php

<?php 
$stdin = file_get_contents('php://stdin', 'r');
$stdout = fopen('php://stdout', 'w');
fwrite($stdout, $stdin);
fclose($stdout);
```

```
$ echo "hello, php!" | php echo.php
hello, php!
```
