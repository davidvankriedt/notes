---
title: Integrity
draft: false
tags:
  - cybersec
  - computer-science
---
Maintaining integrity ensures data is authentic, untampered, and reliable.

## Checksums

A checksum is a small-sized piece of data (often a number) used to detect errors in data. It's generated from a larger block of data (like a file, message, or number).

It's used to verify integrity during:
- File downloads
- Data transmission
- Storage systems

#### How do checksums work?
1. Input data --> passed through a checksum function
2. Function computes a checksum value
3. This value is sent or stored alongside the data
4. On receipt, the checksum is recomputed and compared
5. If they match --> data is likely intact
6. if not --> data may be corrupted or tampered

Examples of checksum methods:
- simple byte addition
- CRC (Cycle Redundancy Check)
- Luhn Algorithm
- Hash functions (for more secure checks)

#### Credit Card Security - Online Validation

When you enter your credit card number online, it's immediately validated before being sent to the payment gateway.

This checks if:
- the number is formatted correctly
- It passes the Luhn check (basic error detection)
It helps catch:
- Typos
- Fake/incomplete numbers

Not a fraud check; just ensures the number is mathematically valid.

#### Luhn Algorithm as a checksum

The Luhn Algorithm is a type of modulo-10 checksum.

It's commonly used for:
- Credit cards
- IMEI numbers
- Apple & Google Pay

It detects input errors like:
- Single-digit mistakes
- Digit transpositions

It's not cryptographically secure.

How it works:
1. Starting from the right, double every second digit
2. If doubling gives a number $> 9$, subtract $9$
3. Add all digits
4. If total % $10 == 0$ --> valid

## What is a Hash Function?

A hash function is a mathematical algorithm that maps data of any size to a fixed-size string of characters (usually a sequence of numbers and letters). The result is called a hash value or digest.

Properties:
- Deterministic
- Fast to compute
- Pre-image resistance (hard to reverse-engineer the original input)
- Collision resistance (hard to find two inputs with the same hash)

It's a quick way to verify whether a file sent and a file received are exactly the same.

A hash value acts like a digital fingerprint of a file or message. Even a tiny change in the original data leads to a completely different hash. This makes hashes useful for detecting tampering or corruption.

It's used in:
- File verification (e.g. checksums)
- Digital signatures
- Blockchain
- Password storage

#### Cryptographic Hashes

A cryptographic hash function is a special type of hash function that:
- Takes any input and returns a fixed-size hash value
- Is deterministic
- Is designed to be secure against manipulation and reversal

Examples: SHA-256, SHA-3, BLAKE3
![[Screenshot 2026-07-07 at 16.03.54.png]]

## Avalanche Effect

The avalanche effect refers to how a small change in input (even 1 bit) causes a significant change in output. A good cryptographic hash function exhibits a 50% bit change on average in the hash output for any small input change.

This ensures unpredictability and security in cryptographic systems, preventing attackers from guessing relationships between similar inputs and outputs.

## Github

Evey Git commit is identified by a cryptographic hash, which uniquely represents the content and history of that commit.
![[Screenshot 2026-07-07 at 16.06.57.png]]


## Hash Collision

A hash collision occurs when two different inputs produce the same hash output. Hash functions are many-to-one mappings (many possible inputs, limited number of outputs). This is unavoidable due to the [Pigeonhole Principle](https://en.wikipedia.org/wiki/Pigeonhole_principle)

Factors that increase collision risk:
- Low entropy inputs: similar or patterned data
- Short hash lengths: fewer possible output values
- Malicious attempts: attackers may try to intentionally generate collisions

MD5 and SHA-1 are known to be vulnerable to collision attacks.

SHA-2 (e.g. SHA-256, SHA-512) are more resistant (no practical collisions found).

This is important in digital signatures, file verification, certificate authorities.

## MAC (Message Authentication Codes)

The problem with regular hashes are that they don't authenticate the message origin. Since hash functions are public, anyone can forge new hashes for fake messages.

As a solution to this, we use MAC:
- Add a shared secret
- Only someone with the secret key can compute the correct hash.
- The receiver knows if the message was changed, or if the sender is legitimate.![[Screenshot 2026-07-07 at 16.15.58.png]]
However, since the hash function is still public, and the secret key is just appended to the message, attackers could append extra data to the end of the message without knowing the key. This is known as a length extension attack.

## HMAC (Hash-based Message Authentication Code)

- It provides data integrity + authentication
- Prevent length extension attacks
- Mix the secret securely into the hash using inner and outer padding

How it works:
- uses a shared secret key and a hash function
- computes a MAC that:
	- Confirms the message hasn't been altered
	- Verifies the sender is trusted

![[Screenshot 2026-07-07 at 16.23.02.png]]

## Cryptographic vs Non-Cryptographic Hashes

Why aren't Non-crypto hashes secure?
- Fast and efficient for lookup tables or file deduplication
- Not safe against intentional tampering
- Vulnerable to collisions and reversing

Use cryptographic hashes when:
- Verifying integrity
- Authenticating messages (HMAC)
- Signing digital documents![[Screenshot 2026-07-07 at 16.27.06.png]]

## Attacks on Hash Functions

Common attacks:
- Brute force (not effective)
- Rainbow table attack (large database of common plaintext inputs and their hash outputs)![[Screenshot 2026-07-07 at 16.28.58.png]]