---
title: Encryption & Ciphers
draft: false
tags:
  - computer-science
  - cybersec
---
## Symmetric keys

Same key for encryption and decryption. Fast but distributing key is challenging.

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
- Input: 64-bit plaintext
- Key: 56-bit secret key (often input as 64 bits with 8 parity bits ignored)
- Rounds: 16 Feistel rounds, each involving:
	- expansion
	- substitution (S-boxes)
	- permutation
	- key mixing

Feistel Cipher Structure:
- multiple rounds
- substitution followed by permutation
- input block is partitioned into two halves
- in round i,
	$$ 
		\begin{aligned}
		L_i = R_{i-1} \\
		R_i = L{i-1} \oplus F(K_i, R_{i-1})
		\end{aligned} 
	$$
	
![[Screenshot 2026-07-07 at 12.27.27.png]]
Works between stages of confusion and diffusion within the function F, to make it harder for the attacker to predict the plain text patterns.

### Confusion
![[Screenshot 2026-07-07 at 12.32.48.png]]
### Diffusion
![[Screenshot 2026-07-07 at 12.33.31.png]]

![[Screenshot 2026-07-07 at 10.05.26.png]]

### Why DES Failed
- Vulnerabilities:
	- key length is too short (56-bit):
		- brute-force attack feasible with modern hardware
		- 2^56 = ~72 quadrillion keys
- Real-world example:
	- In 1998, the EFF built a machine that cracked a DES key in less than 3 days.

## Advanced Encryption Standard (AES)

- Stronger, more secure, and faster than DES.
- Widely used (e.g. in Wi-Fi, VPNs, and SSL).
- Like DES, based on substitution-permutation network.

### AES Overview
1. Initial round key:
	1. XOR with key
2. 9 rounds:
	1. S-Box (Simple substitution)
	2. Shift Rows (Transposition)
	3. Mix Column (Linear mixing step)
	4. XOR with key
3. Final round:
	1. No Mix Column
### AES Operations
- AES operates on a 4 x 4 column-major array of bytes ("state")
- Starts with 16 bytes of plaintext

![[Screenshot 2026-07-07 at 12.50.10.png]]
- An iterative rather than feistel cipher
	- operates on entire data block in every round rather than feistel (operates on halves at a time)

1. a) "AddRoundKey" - Key XOR
	- each byte $a_{i,j}$ of the state is XOR with the round key bytes $k_{i,j}$.
2. a) "SubBytes" - S-Box
	- each byte $a_{i,j}$ is replaced with a SubByte $S(a_{i,j})$ using 8-bit S-Box.
	b) Shift rows - cyclically shift the bytes in each row by fixed offset.
	c) MixColumns - Each column transformed by a fixed matrix, the matrix multiplication is over Galois Field GF($2^8$)
	d) "AddRoundKey" - Key XOR

## Asymmetric Encryption

Uses a pair of keys: Public and Private
- One key for encryption
- One key for decruption
Public key encrypts; private key decrypts.

Rely on "one-way functions"
- Mathematical operations that are easy to do forwards but difficult to do in reverse

No need to share secret keys. Used for secure key exchange, digital signatures.

Examples: RSA
![[Screenshot 2026-07-07 at 13.10.53.png]]

### RSA (Asymmetric Encryption)

- Invented by Rivest, Shamir, and Adleman in 1977.
- Based on the mathematical difficulty of factoring large prime numbers
- Public-key encryption scheme

Key Components:
- Public Key: Used to encrypt data --> $(e, n)$
- Private Key: Used to decrypt data --> $(d, n)$
- n = p x q where p and q are large primes

#### RSA Key Generation
1. Generate two large primes
	1. use a strong pseudo-random number generator.
	2. test candidates for primality (e.g. Miller-Rabin)
2. Compute modulus
	1. $n = p \times q$
	2. This $n$ is used as the RSA modulus (public and private).
3. Compute Euler's totient
	1. $\emptyset(n) = (p-1) \times (q - 1)$
4. Choose public exponent
	1. Select $e$ such that $1 < e < \emptyset(n)$ and gcd$(e, \emptyset(n)) = 1$
5. Compute private exponent
	1. Find private key such that $d\equiv e^{-1}(\mod\emptyset(n)). (i.e., e \times d \mod \emptyset (n) = 1)$
6. Form the key pair
	1. Public key: $(e,n)$
	2. Private key: $(d, n)$

#### RSA in Practice: What can go wrong?
Common mistakes:
- using small keys
- no padding
- weak randomness
- reusing keys badly
- leaking private keys
- failing to validate certificates

#### Merkle Puzzles
- one of the earliest public key exchange mechanisms
- based on computational asymmetry: Easy for legitimate users, hard for attackers
- goal is to establish a shared secret key over an insecure channel without prior shared secret![[Screenshot 2026-07-07 at 15.01.30.png]]

## Man-in-the-Middle (MitM) Attack
- An attacker secretly intercepts and relays communication between two parties
- Appears legitimate to both sides
- Neither party knows someone is in the middle

Why is it dangerous?
Attackers can:
- Alter messages
- Log confidential info
- Inject malicious commands

- Difficult to detect without strong encryption, authentication, and integrity checks

![[Screenshot 2026-07-07 at 15.08.18.png]]


## Locard's Principle: Digital Forensics Foundation
- Formulated by Dr. Edmonds Locard (1910)
- "Every contact leaves a trace"
- In cybersecurity: every action on a system leaves digital evidence
- Used in both physical and digital investigations
- Forms the basis of forensic science

 Every digital action leaves metadata or logs - helps in tracing intrusions, malware, unauthorised access.
 
![[Screenshot 2026-07-07 at 15.14.40.png]]


## Confidentiality - Bell-Lapadula Model

_Bell-LaPadula (BLP)_ is a formal security model focused on confidentiality. It was developed in the 1970s for military systems. It tires to stop sensitive information from leaking from higher-security areas to lower-security areas.

Two key properties:

| Rule          | Meaning                                          | Simple explanation                                              |
| ------------- | ------------------------------------------------ | --------------------------------------------------------------- |
| No Read Up    | A user cannot read files above their clearance   | A Confidential user cannot read secret files                    |
| No Write Down | A user cannot write information to a lower level | A Secret user cannot copy secret data into an unclassified file |

## Proof and Tranquility

- Proof and Tranquility = Mathematical assurance of program correctness
- Formal verification ensures a program behaves exactly as specified
- Edsger Dijkstra was a pioneer in proving programs correct using logic
- Based on invariants, structured programming, and deductive reasoning
- Used in mission-critical systems to ensure reliability and eliminate hidden bugs

## Zero Trust Security - "Never Trust, Always Verify"

Zero Trust is not one tool. It is an engineering approach for reducing blind trust.

Zero Trust assumes that attackers may already be inside the system:
- MitM attacks:
	- Do not trust a connection just because it appears to come from the right place.
- Insider threats:
	- Do not trust a user just because they are inside the organisation.
- Confidentiality:
	- Only give access to the data needed for the task.
- Zero Trust Model:
	- Every request must be verified, authorised, and monitored.

![[Screenshot 2026-07-07 at 15.33.36.png]]


![[Screenshot 2026-07-07 at 15.32.59.png]]