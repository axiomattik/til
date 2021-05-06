# Needle in the Haystack

Turns out there is a pattern to the notoriously inconsistent $needle, $haystack arguments of PHP.

If you're searching for a needle in an array, then the order is $needle, $haystack.

```
array_search ( mixed $needle , array $haystack , bool $strict = false ) : int|string|false

in_array ( mixed $needle , array $haystack , bool $strict = false ) : bool
```

N.B.: Those are the only two array functions that take a needle and a haystack.

If you're searching for a needle in a string, then the order is $haystack, $needle.

```
str_contains ( string $haystack , string $needle ) : bool
substr_count ( string $haystack , string $needle , int $offset = 0 , int|null $length = null ) : int
```

N.B. There are altogether 13 string functions that take a needle and a haystack.

Unfortunately this doesn't quite hold for `str-replace` and `str-ireplace`. Their arguments are `$search, $replace, $subject` so they're not technically breaking the rule. But $search is $needle-like and $subject is $haystack-like but the order is now array-like.

To summarise:

| function | args |
| -------- | ---- |
| array | $needle, $haystack |
| string | $haystack, $needle |
| string replace functions | $search, $replace, $subject |

