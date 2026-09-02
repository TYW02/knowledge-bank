---
title: W1 Cryptography
tags:
  - Cryptography
---

# Basic Concepts
You have:
- Cipher Text (Encrypted text / words that don't make sense)
- Key (Used to decipher / decrypt the cipher text)
- Plain Text 

## Why Cryptography ?
- Data Protection
- Digital Currency Transactions
- Safe Business Processes


## Situations where Cryptography is useful

When sending a message to another party, the communication channel is not secure. Another party can intercept it and read the content.

This is also called a **"MITM Attack"** where an attack intercepts the connection between 2 parties and reads their information.

If the message is encrypted then the attack can only see the encrypted message, but not the plain text.

# Types of Cryptography

**Symmetric Key**: Encryption and Decryption use the **SAME** key (**Private** key known only to sender and receiver)  -> Private Key Cryptography 

**Asymmetric Key**: Encryption and Decryption use **DIFFERENT** keys (**Public** key for encryption, **Private** key for Decryption, **Public** key known to authorised senders) -> Public Key Cryptography 

**Hashing**: Does NOT use keys (one-way functions can convert data to a fixed length "unique" hash value digest)


# Symmetric Cryptography

PLAIN TEXT -> ENCRYPT(PLAIN TEXT, KEY) -> CIPHER TEXT -> DECRYPT(CIPHER TEXT, KEY) -> PLAIN TEXT

## Substitution Ciphers
Replaces each plaintext character with another according to a fixed pattern.
- Monoalphabetic: Caesar Cipher
- Polyalphabetic: Vigenere Cipher


## Transposition Ciphers
Simple encryption where plaintext characters are shifted in some regular pattern to different positions to form the ciphertext
- Simple transposition cipher
- Rail fence cipher
- Columnar transposition cipher


# Caesar Cipher (Substitution Cipher)
Letters are shifted along in the alphabet to encrypt
Shifted back the same amount to decrypt

### Example:
Plain: ABCDEFGHIJKLMNOPQRSTUVWXYZ
Cipher: DEFGHIJKLMNOPQRSTUVWXYZABC

Hello World -> KHOOR ZRUOG

> [!NOTE]
> Not Restricted to only letters


# Vigenere Cipher (Substitution Cipher)
![[Pasted image 20260829154452.png]]

Given the **KEYWORD** and the **PLAINTEXT** search in the table the corresponding keyword and plain text to get the cipher text.

### Example
ALICEALI (Keyword)
HELLOBOB (Plaintext)
HPTNSBZJ (Ciphertext)

### Decryption
HPTNSBZJ (Ciphertext)
ALICEALI (Keyword)
At row 'H' look for letter 'A' then see what column corresponds that is the plaintext
'L' find 'P' = E
'I' find 'T' = 'L'
> Find Key at row then find ciphertext in that row, the column will be your plaintext

# Simple Transposition Cipher 

Just reverse the order of characters in the plaintext

YTISREVINU -> UNIVERSITY (Decrypt)
SINGPORE -> EROPGNIS (Encrypt)

# Rail Fence Cipher (Transposition Cipher)

### Example 1: (Rail key of 2)
| H   |     | L   |     | O   |     | O   |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     | E   |     | L   |     | B   |     | B   |
HELLOBOB -> HLOOELBB

### Example 2: (Rail key of 3)
| H   |     |     |     | O   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     | E   |     | L   |     | B   |     | B   |
|     |     | L   |     |     |     | O   |     |
HELLOBOB -> HOELBBLO


# Columnar Transposition Cipher

### Example 1: (Key sorting order need not be alphabetical (default))

| R   | E   | D   |
| --- | --- | --- |
| H   | E   | L   |
| L   | O   | W   |
| O   | R   | L   |
| D   | X   | X   |
HELLOWORLD -> LWLX EORX HLOD

- Plaintext is written in a grid of equal length rows and read column by column
- Columns are chosen in an order determined by the encryption key
- **Key** is RED
- **Plaintext** is HELLOWORLD
- **Padding** Character is X


### Example 2: 

| 1   | 2   | 3   | 4   | 5   | 6   | 7   |
| --- | --- | --- | --- | --- | --- | --- |
| a   | t   | t   | a   | c   | k   | p   |
| o   | s   | t   | p   | o   | n   | e   |
| d   | u   | n   | t   | i   | l   | t   |
| w   | o   | a   | m   | x   | y   | z   |
ATTACK POSTPONED UNTIL TWO AM (Plaintext)
TTNA APTM TSUO AODW COIX KNLY PETZ (Cipher text)

- Key is 3 4 2 1 5 6 7
- Padding characters are xyz


# Problems with vulnerabilities
- If I know how Caesar cipher or Rail fence works I can decrypt it
- Is knowledge of the algorithm a vulnerability ?

Algorithm - secret ?
Can you assume secrecy of the algorithm. How can you ensure knowing the algorithm doesn't help ?

**Ensure secrecy in the key only** (Doesn't matter if you know how it works, if you don't have the key you can't break it)

## Basic Solution
Secrecy should ONLY be in the key

> [!Kerckoff's Principle]
> "The security of a cryptosystem must **NOT** be dependent on the secrecy of the **ALGORITHM**. It should **ONLY** depend on the secrecy of the **KEY**"


# DES (Data Encryption Standard)
DES is a symmetric-key block cipher published by the National Institute of Standards and Technology (NIST)

![[Pasted image 20260829161010.png]]

- Each round does transposition, substitution and XOR of plaintext and sub-key
- Each 64-bit plaintext block undergoes 16 rounds of encryption individually
- A 56-bit cipher key is used to generate a different 48-bit sub-key $K_i$ for Round $i$. Key length is actually 64-bit but every 8th bit is discarded to form 56-bit key
- The 56-bit key then undergoes 2 permutations and left circular shift -> 48-bit sub-key is selected.

### Encryption
#### Example running for 2 rounds
- Plaintext = 10110010
- Split into half (L, R)
- L0 = 1011, R0 = 0010
- L1 = R0 = 0010
- R1 = L1 XOR F(R0, K1)
- F(R0, K1) = R0 XOR K1
- L2 = R1 
- R2 = L1 XOR F(R1, K2)
> Basically swap L and R then take R and XOR with F(Rn-1, Kn)


### Decryption
#### Example running for 2 rounds
Ciphertext = 01010001
- Split L2 = 0101, R2 = 0001
- R1 = L2 = 0101
- L1 = 0001 XOR F(L2, K2)
- R0 = L1
- L0 = R1 XOR F(L1, K1)
> Same thing here but you are finding L instead, and remember to use the key BACKWARDS. So K2 -> K1



# 3DES (Triple Data Encryption Standard)

Triple DES operates in 3 Steps: Encrypt-Decrypt-Encrypt ($E_{k1}D_{k2}E_{k3}$)
Reverse -> Decrypt

![[Pasted image 20260829161418.png]]

- 56-bit key was cracked in < 24 hours. But there was inertia to replace DES -> 3DES (Key length = 56 x 3 = 168 bits)
- Encrypt the plaintext blocks using single DES with key $K_1$
- Now decrypt the output of step 1 using single DES with key $K_2$
- Finally, encrypt the output of step 2 using single DES with key $K_3$

### Encryption
> Same as DES but use only 1 key for all rounds. Then after you encrypted, decrypt with K2 and encrypt again with K3


### Decryption
> Now start with Decryption with K3, then encrypt with K2 and finally decrypt with K1.
> Basically whatever you did for encryption, do it backwards.



# AES (Advanced Encryption Standard)
- AES can theoretically be cracked with quantum computing
![[Pasted image 20260829164132.png]]
- 3DES deprecated by NIST due to limited 64-bit plaintext block size support. Making it vulnerable to birthday attacks
- AES includes 3 block ciphers: AES-128, AES-192, AES-256
- Each cipher encrypts and decrypts plaintext in blocks of 128 bits. Number of encryption rounds depend on key size
- Each round does transposition, substitution and XOR of plaintext and sub-key



# OTP (One Time Password)
Plain: H A T
OTP: 6 12 17
Cipher: N M K

Real world examples: 2FA, OTP Dongles
Key must be at least as long as plaintext

Each (symmetric) key is used only once and discarded
Ideally key is truly random
![[Pasted image 20260829164334.png]]



# Random Number Generators (RNG)
```python
from random import seed, random

seed(4)

print(random(), random(), random())
```

Random numbers used in computer programs are pseudo-random, which means they are generated in a predictable fashion using a mathematical formula

- Computers can generate truly random numbers by observing some outside data, like mouse movements, electrical or fan noise, which is not predictable, and creating data from it.
- This is known as **entropy**


# Symmetric Key Problem
- Need to share key between sender and receiver
- Secure key distribution considerations (How secure ?)
- Asymmetric cryptography offers a solution.

# Asymmetric Cryptography
- Uses key pair for encryption and decryption
- Key pair generated are mathematically related
	- Then choose 1 as private, the other as public
- Key generation algorithm is one-way function
	- Given public key, computationally infeasible to get private key (public key still needs to be distributed to senders)

![[Pasted image 20260829164931.png]]


## Asymmetric Key Crypto Authentication
- We can prove you encrypted something - Authentication
- We can combine encryption using different keys to ensure only the recipient can decrypt it, and it's definitely me who wrote it
	- You also know it wasn't read or modified
	- Public key encrypts -> Private key decrypts (Confidentiality)
	- Private key encrypts -> Public key decrypts (Authentication)
![[Pasted image 20260829170702.png]]


## Combined Authentication
![[Pasted image 20260829170728.png]]

- Encrypt message using Alice's private key A_PrivKey(msg) - Alice has signed
- Then encrypt with bob's public key B_Pubkey(A_PrivKey(msg))
- Bob decrypts with bob's private key, then decrypts with Alice's public key
- Decrypting the secured message a second time authenticates Alice as sender.

# Key Generators (One-way functions)
- Needs to be computationally infeasible to get private key from public key (asymmetric key)
- Achieved using one-way functions

## Modular Arithmetic
Clocks work mod 12

$14 \equiv 2 mod 12$

$a \equiv b$ mod n if a % n = b % n

One-way-ness: Given a mod b = 2, what was a and b ?
> Can't calculate as there are many possibilities, infeasible to try all

## Prime Factorisation
- 77 = 7 * 11
- 391 = 17 * 23
- 589 = 19 * 31
- 23622320117 = 2147483647 * 11
- 15778598254603 = 3257631 * 4563413*\

# RSA Key Generation
(Rivest - Shamir - Adleman)

Pick 2 large distinct random primes (p and q)

Calculate $n = pq$
Calculate $\phi(n) = (p-1)(q-1)$ 
> $\phi(n)$ -> Euler's totient function

Pick e = number less than $\phi$, co-prime to $\phi$
Calculate d
- d * e mod $\phi(n)$ = 1

Public key is (e, n)
Private key is (d, n)
- It is computationally infeasible to compute d from e and n alone.
![[Pasted image 20260829172226.png]]

![[Pasted image 20260829172232.png]]


# Diffie-Hellman Key Exchange
![[Pasted image 20260829172406.png]]

![[Pasted image 20260829172417.png]]

![[Pasted image 20260829172607.png]]


# Hashing 
- One-way function (MD5, SHA)
- Take arbitrary length input (message) -> fixed length output (message digest)
- Same input **ALWAYS** produces **SAME** hash


## Secure Hashes
One-way Property
- It is computationally infeasible to find a message that corresponds to a given hash code
Strong Collision Resistance
- It is computationally infeasible to find 2 different messages that hash to the same hash value.


## MD-5
MD5 produces a 128 bit hash and has been proved to not be collision resistant

## SHA Collision
SHA-1, SHA-2 (SHA-256, SHA-384, SHA-512)
SHA-1 produces a 160 bit hash code

SHA-256 produces 256 bit hash code
SHA-512 produces 512 bit hash code

# Digital Signature System
![[Pasted image 20260829173102.png]]

## Hashing for Digital Signature
- Hash of a document encrypted with the sender's private key (Signed or authenticated)
- Sent to the recipient the encrypted hash with the original document (Original doc can also be encrypted)
- Recipient can decrypt the encrypted hash, and check it against the hash of the (decrypted) original document sent.
- A secure digital signature system can provide Confidentiality and Integrity for data
- Data security requires data protection as well


# Birthday Attack
In a group of 23 people, the probability that there are at least 2 person on the same day in the same month is greater than 1/2

The reason the birthday paradox works is that we are not just looking for matches between one fixed date and the other dates. We are looking for matches between any two dates in the set, so there are more opportunities for matches

# Cryptanalysis
Study of ciphers to find a weakness and break it
- Benefits subsequent efforts to strengthen existing cryptographic protocols and support development of better protocols
Techniques include: Brute Force Attack, Frequency Analysis, Known Plaintext Attack

## Brute-Force Attack

Try all possible key combinations to recover an intelligible plaintext that was used to produce the cipher text
Need to try half of all possible keys, on average
Need high performance computing resources, practically infeasible if key is sufficiently long.

## Frequency Analysis
English text has structure. 
Letter Frequencies: 
E: 12.51%
T: 9.25%
A: 8.04%
O: 7.60%
I: 7.26%

> [!Weakness]
> Main weakness of mono-alphabetic substitution/transposition ciphers is that although the letters themselves change(position), their **frequencies** do not.

![[Pasted image 20260829174932.png]]


## Known Plaintext Attack
When attacker has both the unencrypted text(plaintext) and its encrypted version(ciphertext)
![[Pasted image 20260829175020.png]]

# Characterising Cryptanalysis Attacks

- Brute Force -> Try all possible keys
	- Feasible for alphabets only (or small key space)
	- Significant computational resources needed otherwise
- Frequency Analysis -> Based on English text structure
	- Substitute most common occurring letters first
	- Then, focus on short, common words (digraphs, trigraphs)
	- Certain degree of trial and error involved
- Known Plaintext -> Correlate input-output pairs
	- Need access to crypto engine
	- Inject known plaintext and observe output ciphertext
	- Infer protocol from correlation of I/O values





















