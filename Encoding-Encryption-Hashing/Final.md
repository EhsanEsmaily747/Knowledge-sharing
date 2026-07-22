# Encoding vs Encryption vs Hashing

Understanding the difference between **Encoding**, **Encryption**, and **Hashing** is important in software development and cybersecurity.

Although all three transform data, they solve completely different problems.

| Method | Purpose |
|---|---|
| Encoding | Change data format |
| Encryption | Hide data from unauthorized access |
| Hashing | Create a fingerprint to verify data |

---

# 1. Encoding (The Translator)

## What is Encoding?

Encoding converts data from one format into another format so that different systems can understand or transfer it.

The most important rule:

> **Encoding is not security.**

Encoding:

- Does not hide information
- Does not use a secret key
- Can always be reversed

It only changes **how data is represented**.

---

## How Encoding Works

```
Original Data
      |
      ▼
   Encoding
      |
      ▼
 Encoded Data
      |
      ▼
   Decoding
      |
      ▼
Original Data
```

---

# Example: Base64

Base64 converts binary data into text.

Original:

```
Hello
```

Encoded:

```
SGVsbG8=
```

Anyone can decode it:

```
SGVsbG8=
      |
      ▼
    Hello
```

No password.

No secret key.

No protection.

---

## Why Base64 Exists

Computers store files as binary data:

```
01001010 10101001 00101010
```

However, many systems are designed to transfer text.

Base64 converts binary bytes into a text representation, not binary data into actual text data.

It is commonly used for:

- Images inside HTML
- File transfer
- JSON APIs
- Email attachments

Example:

```html
<img src="data:image/png;base64,...">
```

---

# Common Encoding Methods

## Base64

Used for converting binary data into text.

Examples:

- Images
- Files
- API data

---

## UTF-8

A standard for representing text.

Supports:

- English
- Arabic
- Chinese
- Emojis

Used in:

- HTML
- JSON
- Databases
- Source code

---

# 2. Encryption (The Lock)

## What is Encryption?

Encryption protects information by converting readable data into unreadable data.

The important rule:

> **Encryption is reversible only with the correct key.**

Encryption provides:

- Confidentiality
- Privacy
- Protection from unauthorized access

---

## How Encryption Works

The original data is called:

**Plaintext**

The encrypted data is called:

**Ciphertext**

```
Plaintext
    |
    ▼
Encryption + Key
    |
    ▼
Ciphertext
    |
    ▼
Decryption + Key
    |
    ▼
Plaintext
```

---

# Example

Original:

```
Credit Card Number
```

Encrypted:

```
8F91A7C2D91B...
```

An attacker sees only meaningless data.

With the correct key:

```
8F91A7C2D91B...
          |
          ▼
Credit Card Number
```

---

# Types of Encryption

## Symmetric Encryption

Uses one secret key.

The same key is used for:

- Encryption
- Decryption

```
             Key
              |
              ▼
Data → Encryption → Ciphertext
              |
              ▼
          Decryption
              |
              ▼
             Data
```

Advantages:

- Very fast
- Efficient for large amounts of data

Example:

## AES-256-GCM

Used in:

- HTTPS
- VPNs
- Disk encryption
- Cloud storage

---

## Asymmetric Encryption

Uses two keys:

1. Public key
2. Private key

The public key can be shared.

The private key must remain secret.

Used for:

- Secure communication
- Key exchange
- Digital signatures

Examples:

- RSA
- X25519

---

# 3. Hashing (The Fingerprint)

## What is Hashing?

Hashing converts data into a fixed-size fingerprint called a hash.

The important rule:

> **Hashing is one-way.**

You cannot reverse a hash to get the original data.

---

## How Hashing Works

```
Original Data
      |
      ▼
 Hash Function
      |
      ▼
 Hash Value
```

---

# Example: SHA-256

Input:

```
Hello
```

Hash:

```
185f8db32271fe25f561a6fc938b2e...
```

A small change creates a completely different hash.

Input:

```
hello
```

Hash:

```
2cf24dba5fb0a30e26e83b2ac5b9e...
```

Only one character changed, but the fingerprint changed completely.

---

# Common Uses of Hashing

## 1. Password Storage

Websites should never store passwords directly.

Bad:

```
password123
```

Instead, they store:

```
hashed_password
```

During login:

```
User Password
      |
      ▼
    Hash
      |
      ▼
Compare With Stored Hash
```

If they match:

```
Access Granted
```

---

## Password Hashing Algorithms

Recommended:

- Argon2id
- bcrypt

They are intentionally slow to make password guessing attacks expensive.

---

## 2. File Integrity Checking

Hashing can verify that a file was not modified.

Example:

Original file:

```
SHA-256:
abc123xyz...
```

Downloaded file:

```
SHA-256:
abc123xyz...
```

Same hash means:

```
The file is unchanged.
```

---

# Quick Comparison

| Feature | Encoding | Encryption | Hashing |
|---|---|---|---|
| Purpose | Format conversion | Data protection | Data verification |
| Reversible | Yes | Yes (with key) | No |
| Uses key | No | Yes | No |
| Security | ❌ No | ✅ Yes | ✅ Yes |
| Example | Base64 | AES-256-GCM | SHA-256 |

---

# Modern Recommendations

| Goal | Recommended |
|---|---|
| Text representation | UTF-8 |
| Binary data transfer | Base64 |
| Data encryption | AES-256-GCM |
| Key exchange | X25519 |
| Password storage | Argon2id / bcrypt |
| File verification | SHA-256 |

---

# Common Mistakes

## ❌ Base64 is not encryption

Example:

```
SGVsbG8=
```

is not protected.

Anyone can decode it.

---

## ❌ Hashing is not encryption

A hash cannot be decrypted.

It is designed to be one-way.

---

## ❌ Plain SHA-256 is not for passwords

SHA-256 is fast.

Fast hashing is good for files but bad for passwords because attackers can try many guesses quickly.

Use:

```
Argon2id
```

or:

```
bcrypt
```

instead.

---

# Final Memory Trick

```
Encoding
=
Change the format


Encryption
=
Hide the information


Hashing
=
Verify the information
```

---

# Simple Question Guide

When you have a problem, ask:

### "How can another system understand this data?"

Use:

```
Encoding
```

---

### "How can I stop others from reading this data?"

Use:

```
Encryption
```

---

### "How can I know if this data changed?"

Use:

```
Hashing
```
