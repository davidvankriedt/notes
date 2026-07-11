---
title: Format Strings
draft: false
tags:
  - computer-science
  - cybersec
---
## `printf()`

printf(), when using variable placeholders like %d, and %s, it looks for those variables in the stack, and when you don't provide variables, it fetches beyond its scope until it finds a variable. This way, you can access variables outside the scope of the function, and that's the exploitation.