---
title: Chapter 7 - Cryptography and the PKI
tags:
  - "#project/comptia"
  - "#notes"
start: 04/15/2025
---
## Vocabulary
- **Cryptography:** The process of encoding information in a manner that cannot be decoded without the key.
- **Cipher:** A method used to scramble or obfuscate characters to hide their value
- **Substitution Cipher:** A cipher in which one character is changed for another according to a key
- **Polyalphabetic Cipher:** A substitution cipher which uses multiple substitution alphabets for the same message
- **Transposition Cipher:** A cipher that involves transposing or scrambling symbols in a certain manner
- **Steganography:** The use of cryptographic techniques to embed messages in other data
- **Symmetric Cryptography:** Uses the same shared secret key to encrypt and decrypt data. Also called secret or private key cryptography
- **Asymmetric Cryptography:** Uses pairs of public and private keys to encrypt and decrypt data. Also called public key cryptography
- **Data at Rest:** Data which resides in a permanent location awaiting access
- **Data in Transit:** Data being transmitted across a network between two systems, often using TLS
- **Data in Use:** Data stored in the active memory of a computer system where it may be accessed by processes on the system
- **Obfuscation:** The practice of making it difficult for humans to understand how code works
- **Full-Disk Encryption (FDE):** A system in which all the data on a hard drive is automatically encrypted
- **Partition Encryption:** A system in which a particular partition of a hard drive is automatically encrypted
- **File-Level Encryption:** A system in which individual files are encrypted
- **Volume Encryption:** A system in which a particular volume (grouping of files and folders) on a hard drive is automatically encrypted
- **Database Encryption:** Encryption that targets database data
- **Transparent Data Encryption (TDE):** A system which encrypts the entire database
- **Column-level Encryption (CLE):** A system in which individual chosen columns in a database are encrypted
- **Record-level Encryption:** A system in which individual records in a database are encrypted
- **Digital Signature:** An encrypted message digest that represents unchanged data to preserve integrity
- **Non-repudiation:** Assurance to a message recipient that the message was originated from the desired sender, offered only by asymmetric cryptosystems
- **Repudiation:** A sender claiming they never sent a message
- **Key Space:** The range of usable values for a cryptographic key
- **Key Length:** The number of binary bits in a cryptographic key
- **The Kerckhoffs' Principle:** The principle that a cryptographic algorithm should be fully secure even if someone knows all details about the system/algorithms except the key. "The enemy knows the system"
- **Cryptovariables:** Another word for cryptographic keys
- **Cryptography:** The art of creating and implementing secret codes and ciphers
- **Cryptanalysis:** The study of methods to defeat codes and ciphers
- **Cryptology:** The combination between cryptography and cryptanalysis
- **Cryptosystem:** A specific implementation of a code or cipher in hardware and software
- **Cipher:** The algorithm used to perform encryption and decryption operations
- **Block Cipher:** A cipher which operates on split-up chunks of a message
- **Stream Cipher:** A cipher which operates on one character or one bit of a message at a time
- **Data Encryption Standard (DES):** A now-deprecated cryptosystem used by the U.S. government from 1977 until it was deprecated in 2001
- **Triple-DES (3DES):** An advanced version of DES which uses the same algorithm three times with different keys. Also deprecated and insecure
- **Advanced Encryption Standard (AES):**  A modern encryption algorithm which uses the Rijndael block cipher
- **Key Management Practices:** Measures taken to protect keys and key generation information
- **Key Exchange:** The secure distribution of secret keys for symmetric cryptosystems
- **Diffie-Hellman Exchange:** An algorithm used to exchange secret keys when PKI and physical exchanges are not available
- **Split Knowledge Principle:** The act of providing different individuals or systems with part of the key and having them combine them
- **Key Escrow:** A third party which securely stores a copy of an encryption key for emergency use later
- **RSA:** A widely used public key algorithm which relies on the difficulty of factoring large primes
- **Elliptic Curve Cryptography (ECC):** A public key cryptography algorithm which relies on the difficulty of solving the elliptic curve discrete logging problem
- **Message Digest:** The result of running a message through a hash function. Also *hash, hash value, hash total, CRC, fingerprint, checksum*, and *digital ID*
- **Secure Hash Standard / FIPS 180:** The U.S. government publication which defines SHA, SHA-1, SHA-2, and SHA-3
- **SHA-1:** A hashing algorithm which produces a 160-bit digest after processing a message in *only* 512 bit blocks. Considered weak today
- **SHA-2:** A collection of related hashing algorithms (upgrades of SHA-1) generally considered secure today
- **SHA-3:** The most modern iteration of SHA using the Keccak algorithm
- **MD5:** An algorithm which processes 512 bit message blocks. Considered insecure due to collision generation being too possible
- **Hash-Based Message Authentication Code (HMAC):** A process in which a shared secret key is used in combination with a hashing algorithm to provide integrity and speed but NOT non-repudiation (due to using a symmetric key) !
- **Public Key Infrastructure (PKI):** The global infrastructure that defines how cryptographic security is used in computing systems
- **Digital Certificate:** Copies of an individual's public key endorsed and signed by a third party
- **X.509:** The international standard which defines construction of digital certificates !
- **Certificate Authority (CA):** An organization that notarizes digital certificates
- **Registration Authority (RA):** An organization that verifies a user's identity to assist the CA at certificate notarization request
- **Root Certificate:** The top-level certificate for an organization's entire PKI that serves as the root of trust. Generally kept completely offline
- **Intermediate CA:** Subordinate CAs that actually distribute certificates to clients and remain online, linked to the root using certificate chaining
- **Certificate Chaining:** A system in which each certificate held is signed by a higher level CA until the root
- **Certificate Pinning:** A practice in which browsers pair certificates to subjects (often domains) for an extended period of time, allowing them to notice if the certificate changes !
- **Certificate Revocation Lists (CRLs):** Offline lists of revoked certificate serial numbers, provided by the CA
- **Online Certificate Status Protocol (OCSP):** A protocol that allows a client to request the status of a given certificate from a CA !
- **Certificate Stapling:** A practice that adds a copy of a recent OCSP request to the web server's CA for the client to verify itself !
- **Distinguished Encoding Rules (DER):** A binary certificate file format !
- **Privacy Enhanced Mail (PEM):** An ascii certificate file format !
- **Personal Information Exchange (PEX):** A binary certificate file format typically used by windows !
- **Hardware Security Module (HSM):** A physical device which store and manage encryption keys in a secure manner !
- **Birthday Attack:** A type of brute-force attack that relies on the fact that finding a hash or key collision is probable (but not guaranteed) within a surprisingly small number of tries
- **Downgrade Attack:** An attack which attempts to get a device or system to use a less secure cryptographic system
- **Salting:** Adding a randomly generated value to stored passwords *before* hashing
- **Key Stretching:** Using an algorithm such as PBKDF2 to salt/"stretch" passwords into strong ciphertexts !
- **Homomorphic Encryption:** Encryption methods that allow calculations to be performed on encrypted data while maintaining the validity of the data after it is decrypted (i.e. the operation is done to both the encrypted and plain data)
- **Perfect Forward Secrecy:** An encryption system that ensures a breach in key privacy does not allow for decryption of past or future communications

## Modern Cryptography

Cryptography is a set of very widely used protocols and algorithms that encode data to maintain confidentiality, integrity, authentication, and non-repudiation. There are a variety of old cryptographic techniques that are keyed or unkeyed, such as substitution/Caesar ciphers, rotation ciphers, polyalphabetic ciphers, etc. Most of these simple methods are easily breakable by today's standards using methods like frequency analysis. For this reason, more advanced mathematics-based cryptographic algorithms were invented to be used with computers.

Encryption is commonly applied at a variety of levels. In ascending order of specificity the most common ones are:
- Full-Disk
- Volume
- Partition
- File
- Database (Transparent Data Encryption)
- Column (in database)
- Record (in database)

Any cryptographic algorithm requires the use of keys, sets of data that the system uses to encrypt or decrypt data. A key is just a file or record, and the key space of an algorithm is comprised of every possible value that a binary value of that size (key length) can hold. The key length is the most crucial modifiable aspect of securing a crypto system. The longer the key, the more secure the system is against a variety of attacks. However, longer keys typically increase the time and processing power it takes to run the system.

Cryptography maintains its four goals through either symmetric or asymmetric key systems. 

**Symmetric systems** work by having all parties that wish to communicate share a pair of identical keys. When someone wishes to send a message, they encrypt their message with the key, send the message, and then the receiver decrypts it with the same key. There are a couple key issues with this framework.
- **Exchanging keys is difficult.** It's not safe to share symmetric encryption keys over any kind of plain text protocol, as someone who intercepts the key will be able to decode all of your encrypted messages. This is typically solved with a key exchange algorithm, utilizing asymmetric encryption first, or by physically transporting keys (out of band exchange).
- **There is no non-repudiation.** Because everyone's key is identical, there's no way to verify that a given message come from any particular individual.
- **It's unscalable.** In a network of systems, each pair of systems needs its own set of keys in order to communicate privately with one another. As the number of systems grows, this quickly becomes impractical.
- **Keys must be regenerated.** Every time a participant leaves the group, all the keys they know of must be re-generated.

There is a major strength of symmetric systems, though - they are significantly faster than asymmetric systems. For this reason, keys are often exchanged over an asymmetric system and then the systems switch to symmetric encryption to operate at a higher speed.

**Asymmetric systems** work by having each individual generate their own public key and private key. When someone wishes to send a message to someone else, they get that person's public key and encrypt the data with it. Once the data is encrypted with someone's public key, only that someone's private key can decrypt it. This solves all of the above issues with symmetric systems - public keys can be exchanged publicly, one can implement non-repudiation through hashing and encrypting the hash with their private key, each user only needs 2 keys, and keys only need to be regenerated if a private key is compromised. 

Asymmetric key systems are used often to initiate connections or send secure messages to the general public, but they are very rarely used where speed is a concern, because they are 1000-10000x slower than symmetric key systems.

## Cryptographic Algorithms

**DES** is a now deprecated algorithm that was proposed for all government communications in 1977 by the U.S. It's widely considered insecure and breakable at this point in time.
**3DES** is an adapted version of DES which triple-encrypts data using DES. It is also considered insecure.
**AES** is a collection of algorithms which use the Rijndael block cipher to encrypt data. AES includes
- **AES-128** (10 rounds)
- **AES-192** (12 rounds)
- **AES-256** (14 rounds)

	Where the number indicates the size of the key. The block size of each AES algorithm is equal to its key size.
**RSA** is an asymmetric cryptosystem released in 1977 which is still widely used today.  It relies on the difficulty of factoring prime numbers to prevent keys being broken.
**ECC** is an asymmetric cryptosystem released in 1985 that relies on the difficulty of the "elliptic curve discrete logarithm" problem to prevent keys being broken.
**SHA** and its successors are hashing algorithms that turn data of unlimited length into a digest.
- **SHA/SHA1** is outdated and insecure.
- **SHA-2**, a theoretically insecure standard, is split up into 4 algorithms:
	- **SHA-256**, which produces a 256-bit digest
	- **SHA-224**, which produces a truncated version of the SHA-256 hash
	- **SHA-512**, which produces a 512-bit digest
	- **SHA-384**, which produces a 384-bit digest with a 1024 block size
- **SHA-3** is a drop-in replacement for SHA-2 and is still considered secure.
**MD5** is a fast hashing algorithm that creates 128-bit digests, but it is generally considered insecure due to collision problems.
**HMAC** implements part of a digital signature solution but does not provide non-repudiation. It guarantees integrity of a message during transmission. You can drop any hash algorithm into HMAC using a shared secret key. It's a half-and-half solution between full digital signatures and symmetric encryption systems.

## Public Key Infrastructure

**Digital Signatures** provide a mechanism to verify that the person who sent a message actually sent it, and they also provide a mechanism to verify that the message has not been changed from its originally sent state. They do so by following these steps:
1. The sender generates a hash of their plaintext message.
2. The sender encrypts the hash using their private key.
3. The sender appends the encrypted hash to their message.
4. When the receiver receives the message, they then decrypt it using their private key.
5. The receiver decrypts the hash using the sender's public key.
6. The receiver hashes the plaintext message themselves and compares the hashes.

A matching hash means that the message was sent by the claimed sender and that it has not been modified.

**Digital Certificates** are a way of ensuring that a public key actually belongs to the person who it claims to belong to. Certificate infrastructure relies on the trust of private third parties called Certificate Authorities such as IdenTrust or AWS to issue the certificates. A certificate ordered according to the X.509 standard looks like this:
- The X.509 version that the certificate was written in
- The serial number
- A Signature Algorithm Identifier that describes which cryptosystem was used to sign the contents
- The name of the issuer
- The start date and end date of the certificate
- The subject's "common name", usually a domain name
- Optional Subject Alternative Names (SANs) which allow the requester to specify extra domains or IP addresses to be covered under the certificate
- The subject's public key

Certificate authorities are the issuers of these certificates. The actual servers that issue and sign these certificates are mid-level CA servers called intermediate CAs. While intermediate CAs stay online, they hold certificates to a higher-level CA server, and so on until the root CA server is reached. The root server is kept powered down and offline unless it is needed to issue additional certificates. Organizations can issue and configure their web browsers to use their own custom certificates from an in-house CA server.

To receive a certificate, you must first go through the enrollment process with your RA of choice. This is often difficult, requiring extensive proof that you are who you say you are, often including physical meetings at the CA's offices. Once you have proven that you are you, you can make a Certificate Signing Request to the CA. They then send you back your certificate, signed with their private key.

There are different levels of certificate that one may acquire - a domain validation certificate verifies that the subject has control over the domain name, whereas an extended validation certificate ensures that the person holding the certificate is a legitimate organization.