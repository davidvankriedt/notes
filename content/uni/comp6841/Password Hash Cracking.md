---
title: Password Hash Cracking
draft: false
tags:
  - computer-science
  - cybersec
---
## [Dictionary Attack](https://en.wikipedia.org/wiki/Dictionary_attack)

A Dictionary attack is using a subset of letters/symbols to figure out a password/decryption key. It originally used words from the dictionary, hence the name, but now refers more to the very large lists of leaked passwords found in the internet from previous attacks. This is more effective than a brute force attack because people are more likely to use a common password or the same password instead of a random set of symbols.

## [Rainbow/Lookup Tables](https://en.wikipedia.org/wiki/Rainbow_table)

This is a large pre-computed table of hashes of commonly used passwords. Attackers use it to match the hash against the target rather than having to compute a hash each time. They are ineffective if the hash algorithm uses “salt” (meaning adding random characters to the password before hashing) like bcrypt.

## [Birthday Attack](https://en.wikipedia.org/wiki/Birthday_attack)

There is a paradox in probability called the birthday paradox, which basically says that there is a very high possibility of 2 students sharing the same day in a classroom, despite there being quite a small chance that a student’s birthday is on a specific date. Through this paradox, attackers try to find a collision with a file they’re targeting, such that they can infiltrate a malicious file into a system with an identical hash that won’t alarm the system they’re attacking. This attack happens more frequently in older encryption hashing algorithms such as MD5 and SHA-1 which generate a much smaller output size (there’s less possibilities).

## [Chosen-plaintext attack](https://en.wikipedia.org/wiki/Chosen-plaintext_attack)

This attack involves using the public encryption key to learn from how the encryption system encrypts plain text. Then, by continuously inputting plain text, we can use mathematics to watch patterns arise (studied in cryptanalysis) and the attacker can reverse engineer the password. It’s basically guessing inputs, and making educated guesses, until figuring out the encryption pattern. This is used for breaking encryption like AES rather than hashing, because since hashing is a one-way function, it doesn’t use a key that can be recovered through such an attack.