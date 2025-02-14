# Search libc function offset

## Overview

This is a small tool designed for CTF (Capture The Flag) competitions. When you leak the address of a certain function from libc, it can be challenging to determine which operating system or version of libc the target is using. The typical approach is to extract common `libc.so` files from the system and compare the last 12 hexadecimal digits of the leaked address.

To save time and automate this process, I wrote a few lines of code for reuse in future challenges.

This tool uses the [libc-database](https://github.com/niklasb/libc-database) as its database.

## Installation

Clone the repository and install the package in development mode:

```shell
git clone https://github.com/lieanu/LibcSearcher.git
cd LibcSearcher
python setup.py develop
```

## Example Usage

Below is a basic example in Python:
```python3
from LibcSearcher import *

# The second parameter is the leaked address (can be the full address or the last 12 hex digits, e.g., d90). It should be an integer.
obj = LibcSearcher("fgets", 0X7ff39014bd90)

# Retrieve the offset for 'system'
obj.dump("system")

# Retrieve the offset for '/bin/sh'
obj.dump("str_bin_sh")

# Retrieve the offset for '__libc_start_main_ret'
obj.dump("__libc_start_main_ret")
```

If multiple libc versions match, you can use add_condition(leaked_func, leaked_address) to add additional constraints, or manually choose a libc version if you are certain.
## Notes

    The code quality might not be the best—feel free to report bugs or suggest improvements.
    Contributions adding libc information for different Linux distributions are welcome.

Happy hacking!
---

Feel free to modify it further if you need any additional details or adjustments!
