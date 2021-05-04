## 1 Bar

Precedence of the string concatenation operator has been fixed in PHP 8.0.

What is the expected output of this PHP [program](https://stackoverflow.com/a/1105565)?

```
<?php
$x = 1;
echo "foo: " . $x+1 . " bar";
```

Unless you are already familiar with the intricacies and quirks of PHP, you might expect it to print `foo: 2 bar`. This would seem reasonable.

However, the actual output depends on the version of PHP you are running.

| Version | Output |
| ------- | ------ |
| 5.6     | 1 bar  |
| 7.4     | Warning: a non-numeric value encountered in ... on line 3 1 bar |
| 8.0     | foo: 2 bar |

What's going on?

In PHP 5.6, the `+`, `-` and `.` all have the same precedence and are left associative. So `"foo: " . $x+1 . " bar"` (despite the use of whitespace that indicates to the human reader that we want to do a bit of simple arithmetic before our string concatenations) is actually parsed as:

`((("foo: " . $x) + 1) . " bar")`

The first thing PHP attempts to do is concatenate a string with an integer. This is acceptable in PHP so `"foo: " . $x` evaluates to `string (6) "foo: 1"`. The second thing PHP attempts to do, then, is to find the sum of a string and an integer. Again, this is acceptable in PHP. If the string can be parsed as an integer, then the sum will be what we might expect. So `"1"+1` would evaluate to `int(2)`. However, the string we are trying to sum (`"foo: 1"`) cannot be parsed to an integer and so PHP essentially treats it as 0. In other words, the addition of a non-numeric string to an integer in PHP is equivalent to the identity function of the integer.

So the last thing PHP attempts to do in our expression is concatenate `int(1)` with `" bar"` resulting in `string (5) "1 bar"`.

In version 7.4, things have improved somewhat and PHP recognises that if you are trying to find the sum of a non-numeric string and an integer, you might have made a mistake, so it includes a helpful warning.

At last, however, in version 8.0, `+` and `-` now have higher precedence than `.`. So our expression gives the desired result because it is evaluated as a human might expect it to be:

`(("foo: " . ($x+1)) . " bar")`

