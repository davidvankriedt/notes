---
title: Encryption & Ciphers
draft: false
tags:
  - computer-science
  - cybersec
---
## Symmetric keys

#### Enigma Machine

WW2 German encryption

#### One time pad (OTP)

Given a random key as long as the message being encrypted, mathematically impossible to decipher - key can only be used once to not create patterns


A good symmetric key changes around half the bits of the output every time a bit is changed during encryption.

## Encryption

#### Block Cipher

Encrypts fixed-size chunks
![[Screenshot 2026-07-07 at 09.41.35.png]]

However, if we encrypt each chunk individually, you can find patterns, and if you try encrypt an image, you get the similar contrast.

![[Screenshot 2026-07-07 at 09.43.31.png]]
##### Cipher Block Chaining
In this algorithm, each chunk is encrypted, and the XORed against the next block, and the last block is simply encrypted
![[Screenshot 2026-07-07 at 09.46.39.png]]
Decrypting:
![[Screenshot 2026-07-07 at 09.48.36.png]]

#### Padding Oracle Attack
There's a complicated way to flip a bit when decrypting, and that can be used to attack a system.
#### Stream Cipher

Generates keystream and XORs data
![[Screenshot 2026-07-07 at 09.41.13.png]]


### DES (Data Encryption Standard)

What is DES?
- A symmetric-key block cipher developed by IBM in the 1970s.
- Adopted by NIST in 1977 as a federal standard for secure data encryption.
- Operates on 64-bit blocks with a 56-bit key.
- Same key used for encryption and decryption.

Legacy:
- Was a dominant encryption method for decades.
- 1999 - first successful attack by EFF
- 2002 - replaced by AES
- 2018 - finally retired Triple DES / 3DES

__How it works?__
Works between stages of confusion and diffusion


![[Screenshot 2026-07-07 at 10.05.26.png]]