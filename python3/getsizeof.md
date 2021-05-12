# Checking Memory Usage of Objects in Python

Python3's sys module provides a function called `getsizeof` that takes an object and returns an integer representation of the object's memory usage.

This is useful for learning about a script's memory usage but also allows us to demonstrate the memory advantage generators can have over lists:

```
from sys import getsizeof

getsizeof(list(range(1, 1000))) # 8048 (bytes)
getsizeof(range(1, 1000))       # 48 (bytes)
```
