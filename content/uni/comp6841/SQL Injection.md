---
title: SQL Injection
draft: false
tags:
  - computer-science
  - cybersec
---
### Data vs Control

Data and Control have a close relationship, and are normally mixed together.

__Data__:
- usernames and passwords
- barcodes
- voice in a discord call

__Control__:
- semi-colon on a code line
- a null byte on the end of a string
- commands to my chicken-stealing cat

### Vulnerabilities by Mixing
- Unreliably mixing data and control leads to a set of vulnerabilities known as "Injection" vulnerabilities.
- Examples: SQL Injection, buffer overflows, XSS, template injection, RCE.
