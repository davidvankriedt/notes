---
title: Format Strings
draft: false
tags:
  - computer-science
  - cybersec
---
## `printf()`

printf(), when using variable placeholders like %d, and %s, it looks for those variables in the stack, and when you don't provide variables, it fetches beyond its scope until it finds a variable. This way, you can access variables outside the scope of the function, and that's the exploitation.

### `%n`

The `%n` argument says "Take the number of characters printed so far in this printf() statement and write that number to memory at the address of a given pointer". This leads to arbitrary memory writes.

This is further done in COMP6447