---
marp: true
transition: fade-out
theme: default
class: 
  - invert
paginate: true
backgroundColor: #000
style: |
  .container{
    display: flex;
  }
  .col{
    flex: 1;
  }
  img[alt~="center"] {
    display: block;
    margin: 0 auto;
    vertical-align: middle;
  }
  section.lead {
    text-align: center;
    color: white
  }
---

![bg left](images/Foundation.jpg)
# **PKI Foundations for Security Pros**

## Jake Hildreth
## [jakehildreth.com](https://jakehildreth.com/)

Anti-Cast, 2025-11-12

---
![bg right:40% 110%](images/Family.png)
# `Get-ADUser -Identity ‘Jake Hildreth’`
- Husband, Dad, Recovering Sysadmin
* Principal Security Consultant @ Semperis
* Open-source Toolmaker:
Locksmith, BlueTuxedo, PowerPUG!
* Microsoft MVP:
PowerShell + Identity & Access

---

# Agenda
<div class="container">
<div class="col">

* History & Goals
* Encoding vs. Encryption
* Symmetric & Asymmetric Encryption
* Hashing Functions
</div>

<div class="col">

* Signing
* Certificates
* Public Key Infrastructute (PKI)
* Real-World Uses
</div>

---
<!-- _class: lead -->
# **History**
In the beginning was the word...

---

![bg right](images/BigBang.svg)
# **History**
In the beginning was the **pass**word...

---

<div class='container'>
<div class='col'>

## Antiquity
* 1900 BCE: Non-Standard Hieroglyphs
* 1500 BCE: Clay Tablets
* 600 BCE: Hebrew Scholars
* 400 BCE: Polybius Square
* 300 BCE: Kama Sutra
* 75 BCE: Caesar Cipher
</div>
<div class='col'>

## Medieval
* 750-800 CE: Arabic Scholars
* 800-1100 CE: English Scribes
* 1400 CE: Arabic Scholars
* 1508 CE: Tabula Recta
* 1626 CE: Antoine Rossignol
</div>

--- 

<div class='container'>
<div class='col'>

## Pre-WWII
* Focus on Cryptanalysis
* Many Medieval Systems Broken
* First Cryptographic Machines
* First One Time Pad
</div>
<div class='col'>

## WWII
* Allies:
  - TypeX, SIGABA, Lacida
* Axis:
  - Enigma, Purple, SG-41
</div>

---

## Modernity

<div class='container'>
<div class='col'>

* Claude Shannon
* Data Encryption Standard (DES)
* Diffie-Hellman (DH)
* Rivest, Shamir, Adelman (RSA)
* Message Digest Algorithms (MD*)

</div>
<div class='col'>

* Digital Signature Algorithm (DSA)
* Secure Hash Algorithms (SHA)
* Elliptic Curve Cryptography (ECC)
* Advanced Encryption Standard (AES)
* Post-Quantum Cryptography (PQC)
</div>

---
<!-- _class: lead -->
![bg left](images/GoalPosts.jpg)
# **Goals of Cryptography**

--- 

![bg right:41% 100%](images/Confidential.jpg)
# Confidentiality
Ensures a message is only readable by its intended recipient

---

![bg left:60%](images/Integra.jpg)
# Integrity
Ensures a message has not been tampered with or changed

---

![bg right:42%](images/Bart.jpg)
# Non-Repudiation
Ensures an author cannot refute authorship of a message

---

![bg left:40% 110%](images/Popeye.jpg)
# Authentication
Provides proof an author of a message is who they claim

---
<!-- _class: lead -->
# **Encoding vs. Encryption**
Secret or nah?

---

<div class='container'>
<div class='col'>

# Encoding
- Not intended to remain secret
* that is, no **Confidentiality**
</div>

<div class='col'>

# Common Schemes
- ASCII
- UTF-8/16/32
- Braille
- Morse Code
- Base64
</div>

---

![bg right:42%](images/Dolphin.jpeg)
# Example: Cetacean Cipher
- "Hello, Anti-Cast!" encoded:
* EEEEEEEEEeEEeEEEEEEEEEEEEeeEEeEeEEEEEEEEEeeEeeEEEEEEEEEEEeeEeeEEEEEEEEEEEeeEeeeeEEEEEEEEEEeEeeEE EEEEEEEEEeEEEEEeEEEEEEEEEeeEeeeEEEEEEEEEEeeeEeEEEEEEEEEEEeeEeEEeEEEEEEEEEEeEeeEeEEEEEEEEEeEEEEeeEEEEEEEEEeeEEEEeEEEEEEEEEeeeEEeeEEEEEEEEEeeeEeEEEEEEEEEEEEeEEEEe
<sub>Try it yourself: https://www.a.tools/Tool.php?Id=389</sub>
---

<div class='container'>
<div class='col'>

# Encryption
- Intended to remain secret
* Yes! **Confidentiality**
* Requires 1 or more "keys"
* Keys are any secret data
* In modern cryptography, keys are
**really** big numbers
</div>

<div class='col'>

# Common Schemes
- Symmetric - 1 key
  - DES
  - AES
- Asymmetric - 2+ keys
  - RSA
  - ECC
</div>

---
<!-- _class: lead -->
# **Encrypted data** ~~is~~ **should be**
# **indistinguishable from random noise**

---

![bg](images/Ciphertext.gif)

---
<!-- _class: lead -->
# **Symmetric Encryption**
Pretty much all cryptography before the 1970s

---

# Symmetric Encryption
<div class='container'>
<div class='col'>

## Pros
* Same key to encrypt/decrypt message
= Easy to understand
* Simple algorithms
= Very fast
</div>

<div class='col'>

## Cons
* Keys must be pre-shared via a secure channel before communication
= Difficult!
* One key per communication group
= Key management becomes untenable
* Does not protect Integrity, ensure Non-repudiation, or enable Authentication
</div>

---

# Example: Caesar Cipher (Symmetric)
<div class='container'>
<div class='col'>

- Also known as: Shift cipher or ROT*
- Symmetric Encryption ~= ROT13
</div>

<div class='col'>


- A(1) + Shift(13) = N(14)
- N(14) + Shift(13) = A(1)
</div>
</div>

| Original | A | B | C | D | E | F | G | H | I | J | K | L | M | 
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| **"Encrypted"** | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |

| Original | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 15 | 26 |
| **"Encrypted"** | A | B | C | D | E | F | G | H | I | J | K | L | M | 

---

# Example: Caesar Cipher (Symmetric)
| Original Message | Alice Encrypts (ROT13) | Encrypted Message | Bob Decrypts (ROT13) | Received Message |
| - | - | - | - | - | 
| Hello, Anti-Cast! | ![center w:300](images/SymmetricKey.png) | Olssv, Huap-Jhza! | ![center w:300](images/SymmetricKey.png) | Hello, Anti-Cast! |

<sub>Try it yourself: https://rot13.com</sub>

---
<!-- _class: lead -->
# **Asymmetric Encryption**
Encrypt with one & Decrypt with the other

---

# Asymmetric Encryption
<div class='container'>
<div class='col'>

## Pros
* One **key pair** (public + private) per user
= Easy(ish) to manage
* Public keys can be shared over insecure channel
= Much easier than secure channel
* Provides **Confidentiality**, **Integrity**,
**Non-repudiation**

</div>

<div class='col'>

## Cons
* Complicated algorithms
= Not fast
* No verification of other side
= Impersonation possible
</div>

---

# Example: Caesar Cipher (Asymmetric)
<div class='container'>
<div class='col'>

- Private Key ~= ROT7
- Public Key ~= ROT19
</div>

<div class='col'>


- A(1) + Shift(7) = H(8)
- H(8) + Shift(19) = A(1)
</div>

</div>

| Original | A | B | C | D | E | F | G | H | I | J | K | L | M | 
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |
| **"Encrypted"** | H | I | J | K | L | M | N | O | P | Q | R | S | T |

| Original | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 15 | 26 |
| **"Encrypted"** | U | V | W | X | Y | Z | A | B | C | D | E | F | G | 

---

# Example: Caesar Cipher (Asymmetric)
| Original Message | Alice Encrypts (ROT7) | Encrypted Message | Bob Decrypts (ROT19) | Received Message |
| - | - | - | - | - | 
| Hello, Anti-Cast! | ![center w:300](images/PrivateKey.png) | Olssv, Huap-Jhza! | ![center w:300](images/PublicKey.png) | Hello, Anti-Cast! |

<sub>Try it yourself: https://rot13.com</sub>

--- 

<!-- _class: lead -->
# **Hash Functions**
Subheading TBD

---

<div class='container'>
<div class='col'>

# Hash Functions
- Maps any data to a (probably) unique fixed-length value
- Can't be easily reversed to discover source data
- Changing even a single bit of source data changes the hash
- Ensures **Integrity**
</div>

<div class='col'>

# Common Schemes

- MD4/5
- SHA-0/1/2/3
- DSA
</div>
</div>

---

# Silly Example: Addition
| Original | A | B | C | D | E | F | G | H | I | J | K | L | M | 
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

| Original | N | O | P | Q | R | S | T | U | V | W | X | Y | Z |
| - | - | - | - | - | - | - | - | - | - | - | - | - | - |
| **Value** | 14 | 15 | 16 | 17 | 18 | 19 | 20 | 21 | 22 | 23 | 24 | 15 | 26 |

<div class='container'>
<div class='col'>

- HELLOANTICAS**T**
  - 8+5+12+12+15+1+14+
  20+9+3+1+19+**20**
  - Hash: **0139** or **0ACI**
</div>

<div class='col'>

* HELLOANTICAS**H**
  - 8+5+12+12+15+1+14+
  20+9+3+1+19+**8**
  - Hash: **0127** or **0ABG**
</div>

</div>

<sub>Note: This is a terrible hash function full of collisions. Do not use this for anything.</sub>


<!--
Max letter = 38
-->

---

# Real Examples: SHA1 & 2
| Original | Hello, Anti-Cas*t*! | Hello, Anti-Cas*h*!
| - | - | - |
| SHA1 | 94bc685b3657b730ed72 696e036260d3fea8ab23 | 6d1ceba487b84474d554 599b24dea1fed95264ab |
| SHA2-256 | a993f8f095c0c43348cd3 9fead7ec3fd4a26a53e889 d2a89e42adbdfde093398 | ea37a553bb16967a4545 b9f4fb11c19e9dfcdaf5ac 3f7fbdfa93a93f7cca145b |

<sub>Try it yourself: https://gchq.github.io/CyberChef

---
# Real Example #2: Variable-Length -> Fixed Length
1. Collisions can become a problem if your buffer is too small (e.g., MD*, SHA1).
2. A extra benefit is knowable data lengths for data you don't need in plain-text (e.g., passwords)
  - Banks! Stop. Making. Passwords. Limited. Just store the salted hash into a DB and forget my password. 

| Input                                                                                            | Output (MD5)                     | Output SHA1                              |
| ------------------------------------------------------------------------------------------------ | -------------------------------- | ---------------------------------------- |
| The quick brown fox jumps over the laxy dog.                                                     | 1c6d98786bea70b9c34ce7f33201120c | 22b759d30862cc7c7eb3ce9616a9d4e853b1e14d |
| The quick brown fox jumps over the lazy dog. The quick brown fox jumps over the lazy dog. (x50)  | 18b94cc7a461d8774a384d8b82345e51 | d04c682f53e42e09abfd8a34e810ae9555be8ca4 |
| The quick brown fox jumps over the lazy dog. The quick brown fox jumps over the lazy dog. (x100) | 49f1e3a5cc2130d1b5698f5e220598e7 | 49a0f16e0a6c13f90269cfd4f2e7edc0c95fdf22 |


---

<!-- _class: lead -->
# **Signing**
Hashing + Asymmetric Encryption = Better Than Ink

---

<div class='container'>
<div class='col'>

# Signing Process
* Alice creates a hash of a message
* Alice encrypts **the hash**
with her private key
* Alice sends the message +
the encrypted hash to Bob
* Bob decrypts the hash of the message using Alice's public key
* Bob hashes the original message himself
* If hashes match, Alice is the sender!

</div>
<div class='col'>

# Common Uses
- Used for **Non-repudiation**
- Software distribution
- Financial transactions
- Contract management
- Network protocols

---

# Example: Caesar Cipher (Asymmetric) + Addition
| Original Message + Hash | Alice Encrypts Hash (ROT7) | Original Message + Encrypted Hash | Bob Decrypts Hash (ROT19) | Received Message + Hash | Bob Hashes Message HImself |
| - | - | - | - | - | - |
| Hello, Anti-Cast! **0ACI** | ![center w:300](images/PrivateKey.png) | Hello, Anti-Cast! **0HJP** | ![center w:300](images/PublicKey.png) | Hello, Anti-Cast! **0ACI** | **0ACI** matches!|

---

<!-- _class: lead -->
# **Certificates**
(Public Key + Attributes) Signed

---

<div class='container'>
<div class='col'>

# Certificates
- Public keys don't include identifying information
* Certificates tell who owns a public key
* Certificates provide basic **Authentication**
* **If** you trust the issuer, you can trust the public key
* Self-signed certs still permit encryption!
</div>

<div class='col'>

# Typical Contents
- Subject
- Issuer
- Public Key
- Not Before/Not After
- Key Usage/Extended Key Usage
- Signature Algorithm/Signature
- Serial Number
</div>

---

# Generating a Self-Signed Certificate
| Create a Key Pair | Create CSR | Hash the CSR | Encrypt CSR Hash with Alice's Private Key| Package Certificate |
| - | - | - | - | - |
| ![w:200](images/PrivateKey.png)<br>![w:200](images/PublicKey.png) | Subject: Alice<br>Public Key:<br>![w:100](images/PublicKey.png) | 0BHF | 0UAY |  Subject: Alice<br>Issuer: Alice<br>Public Key:<br>![w:100](images/PublicKey.png)<br>Signature<br>Algorithm: Silly<br>Signature: 0UAY |

---

# Certification Authority (CA) Certificate Generation
| Create a Key Pair | Create CSR | Hash the CSR | Encrypt CSR Hash with CA's Private Key| Package Certificate |
| - | - | - | - | - |
| ![w:200](images/PrivateKey.png)<br>![w:200](images/PublicKey.png) | Subject: Alice<br>Public Key:<br>![w:100](images/PublicKey.png) | 0BHF | 0KQO |  Subject: Alice<br>Issuer: CA<br>Public Key:<br>![w:100](images/PublicKey.png)<br>Signature<br>Algorithm: Silly<br>Signature: 0KQO |

---

# Validating a Certificate
|

---

<!-- _class: lead -->
# **Public Key Infrastructure (PKI)**
Formalized trust - all the way down to the root

---

<div class='container'>
<div class='col'>

# PKI Basics
- Not **just** technology:
  - Hardware
  - Software
  - Policies
  - Procedures
- "Chains" of trust lead back to a
"root" of trust
- **If** you trust the PKI (big if),
you can trust others that use the PKI
</div>

<div class='col'>

# Common Components
- Authorities:
  - Root/Intermediate/Issuing
  - Validation
  - Registration
  - Policy
  - Timestamp
- Users:
  - End Entities
  - Relying Parties
</div>

---

<!-- _class: lead -->
# **How Do I Know If I Should Trust a PKI?**

---

![bg right](images/Collin.gif)
# How Do I Know If I Should Trust a PKI?

---

# How Do I Know If I Should Trust a PKI?
- Mostly handled for you
- OSes include lists of trusted roots
  - They're also usually out of date - Server 2025 GA included 7 Root CAs that were expired. 
- Active Directory (AD) networks have PKI: AD Certificate Services
  * Drink!
- Reputable PKIs publish their configurations and procedures
- Honestly, something I need to dig into...

---

<!-- _class: lead -->
# **Real-World Uses**
PGP/GPG, SSL/TLS, and more acronyms

---

# Thanks!
![bg right:36% 80%](images/QR.png)
| Find | Me! |
| - | - |
| Slides | github.com/jakehildreth/PKIFoundations |
| LinkedIn | /in/jakehildreth |
| BlueSky | @dotdot.horse |
| Blog | blog.jakehildreth.com |
| Site | jakehildreth.com |
