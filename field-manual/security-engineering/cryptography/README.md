---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# Cryptography

## Symmetric Cryptography

Also known as secret-key cryptography, it uses a single shared key for both encryption and decryption.

<i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">**Pros:**</mark> Very fast, efficient for large amounts of data.

<i class="fa-chevron-down" style="color:$danger;">:chevron-down:</i> <mark style="color:$danger;">**Cons:**</mark> Key distribution is a major challenge (how do you securely share the secret key?). It does not provide non-repudiation.

<mark style="color:$info;">**Use Cases:**</mark> Because of its speed, it is the go-to method for bulk data encryption. Use symmetric encryption when the primary goal is strictly Confidentiality, such as encrypting an entire hard drive, securing a large database, or protecting files stored locally.

<mark style="color:$info;">**Common Algorithms:**</mark> AES, DES, 3DES, Blowfish.

<mark style="color:$info;">**Supports:**</mark> Confidentiality.

***

## Asymmetric Cryptography

Also known as public-key cryptography, it uses a mathematically related key pair: a public key and a private key. Data encrypted with one key can only be decrypted by the other.

<i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">**Pros:**</mark> Solves the key distribution problem. Provides non-repudiation (if you encrypt with your private key, everyone knows it came from you).

<i class="fa-chevron-down" style="color:$danger;">:chevron-down:</i> <mark style="color:$danger;">**Cons:**</mark> Much slower and more computationally intensive than symmetric cryptography.

<mark style="color:$info;">**Use Cases:**</mark> Common use cases include securely sending a confidential message or key over an insecure network. It is also the foundation of digital signatures to prove identity and ensure Authentication, Confidentiality, and Non-repudiation.

<mark style="color:$info;">**Common Algorithms:**</mark> RSA, ECC, Diffie-Hellman.

<mark style="color:$info;">**Supports:**</mark> Confidentiality, Authentication, and Non-repudiation.

***

## Hashing for Integrity

Unlike symmetric and asymmetric cryptography, hashing is a one-way function. It does not use keys for encryption or decryption. Instead, it takes an input of any size and produces a fixed-size string of characters, known as a hash value or message digest.

<mark style="color:$info;">**Core Principle:**</mark> If the input data changes even slightly (e.g., changing a single comma), the resulting hash value will change completely. This makes hashing perfect for verifying data hasn't been tampered with.

<mark style="color:$info;">**Use Cases:**</mark> Storing passwords, verifying file downloads, digital signatures.

<mark style="color:$info;">**Common Algorithms:**</mark> SHA-256, MD5 (deprecated, but you should know it).

<mark style="color:$info;">**Supports:**</mark> Integrity.
