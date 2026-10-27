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
  anchors:
    visible: true
---

# Cryptography Entropy

Entropy is a measure of unpredictability, expressed in bits:

* Effective strength: a key is only as strong as the entropy behind it. A 256-bit key generated from 32 bits of entropy has only 2^32 possibilities, so an attacker searches that space, not the full 2^256.
* Where it's needed: keys, IVs and nonces, salts, session IDs. TLS handshake randomes and one-time tokens.
* Where it comes from: unpredictable physical events. Examples are thermal noise in circuits, clock jitter, interrupt timing, and disk and network timing. Mouse movements were a classic source on desktops.
* The core problem: computers are deterministic by design, so randomness has to be collected from the outside world and then stretched.

***

## TRNG vs PRNG cs CSPRNG

<table><thead><tr><th width="159"></th><th>TRNG</th><th>PRNG</th><th>CSPRNG</th></tr></thead><tbody><tr><td>Source</td><td>Physical noise</td><td>Mathematical algorithm from a seed</td><td>Algorithm, seeded and reseeded from true entropy</td></tr><tr><td>Deterministic</td><td>No</td><td>Yes: same seed, same output</td><td>Yes, but unpredictable without the internal state</td></tr><tr><td>Speed</td><td>Slow, limited output</td><td>Fast</td><td>Fast</td></tr><tr><td>Examples</td><td>Intel RDSEED/RDRAND, TPM RNG, HSMs, quantum RNGs</td><td><code>rand()</code>, Mersenne Twister, JavaScript <code>Math.random()</code></td><td><code>/dev/urandom</code> and <code>getrandom()</code> on Linux, <code>BCryptGenRandom</code> on Windows, <code>secrets</code> in Python</td></tr><tr><td>Safe for crypto?</td><td>Yes, usually as a speed source</td><td>No</td><td>Yes</td></tr></tbody></table>

How it works in practice: the OS gathers true entropy into a pool, then uses it to seed a CSPRNG. Applications use the CSPRNG, never the raw TRNG.

CSPRNG properties:

* Next-bit unpredictability: seeing past output doesn't help you predict the next bit.
* Backtracking resistance: compromising the current state doesn't reveal earlier output.

Standards: NIST SP 800-90A covers the DRBG algorithms, 800-90B covers entropy sources and 800-90C covers how to combine them.

Practical rule: a general-purpose PRNG used for anything security-related is a vulnerability, even if the output "looks random".

***

## Effects of Weak Entropy

Each of these makes a strong anchor example:

* **Debian OpenSSL (2008):** a code change left the process ID as the only entropy source. That produced just 32,768 possible keys per key type. Every SSH and SSL key generated on Debian and Ubuntu for about two years was guessable.
* **Sony PS3 (2010):** Sony reused the same “random” nonce in every ECDSA signature. That let attackers calculate the private signing key.
* **Android Bitcoin wallets (2013):** a flaw in Android’s `SecureRandom` caused nonce reuse, and funds were stolen.
* **“Mining your Ps and Qs” (2012):** researchers found many RSA keys on the internet sharing prime factors. The cause was mostly embedded devices generating keys at first boot, before they had gathered enough entropy. Shared primes mean the private keys can be calculated instantly.
* **Dual\_EC\_DRBG:** a NIST-standardised generator widely believed to contain an NSA backdoor. NIST withdrew it in 2014. It shows that a CSPRNG can be deliberately weakened.

Practical consequences:

* predictable keys and session tokens.
* Nonce reuse that leaks private keys.
* Cloned VMs or snapshots starting with identical RNG state.
* Headless or embedded devices short of entropy as boot.

***

## Quantum Cryptography & QKD

Quantum cryptography uses quantum physics, not mathematical hardness, to provide security.&#x20;

{% hint style="danger" %}
Not to be confused with Post-Quantum Cryptography, which is ordinary maths designed to resist quantum computers.
{% endhint %}

QKD (Quantum Key Distribution) exchanges a symmetric key using photons. The best-known protocol is BB84 (Bennett and Brassard, 1984).

* Why it's secure: measuring a quantum state disturbs it. so an eavesdropper introduces detectable errors. If the error rate is too high the key is discarded.
* What is does: it only distributes keys. The data itself is still encrypted with a symmetric cipher such as AES.

Limitations:

* Distance limits over fibre (around 100km without trusted relay nodes, and those nodes become weak points).
* Dedicated hardware and links.
* High cost.
* No built-in authentication of the other end, which still needs classical cryptography.
* Vulnerable to hardware implementation attacks.

Official stance: the NCSC (and NSA) don't recommend QKD for goverment or critical use. They favour post-quantum cryptography instead.

Quantum RNGs (QRNGs) use quantum effects as a true entropy source.

***

## Post-Quantum Cryptography

The threat: a large enough quantum computer (often called CRQC) running:

* Shor's algorithm breaks RSA, Diffie-Hellman and EXX entirely. That covers most key exchange and digital signatures in use today.
* Grover's algorithm only halves the effective strength of symmetric keys and hashes. AES-256 drops to roughly 128-bit strength, which is still fine. AES-128 becomes marginal.

Harvest now, descrypt later (HNDL): adversaries record encrypted traffic today and store it until a quantum computer can decrypt it.

* Why it matters now: this is already a risk for any data that must stay secret for 10 or more years, such as health records, government data, IP and long-term credentials.
* Mosca's inequality: if (how long the data must stay secret) + (how long migration takes) > (time until a CRQC exists), you're already late.
* Signatures are different: HNDL mainly threatens key exchange and confidentiality. Signatures only need replacing before a CRQC exists, because a forged signature can't be retroactively harmful in the same way.

The NIST standards (August 2024):

* FIPS 203 ML-KEM (formerly Kyber): Key encapsulation, replacing RSA and ECDH key exchange.
* FIPS 204 ML-DSA (formerly Dilithium): Digital signatures.
* FIPS 205 SLH-DSA (formerly SPHINCS+): Hash-based signatures, kept as a conservative backup.
* Still to come: FN-DSA (Falcon) is coming as FIPS 206, and HQC was selected in 2025 as a backup KEM.

Hybrid key exchange: classical and PQC algorithms are combined so the connection stays secure if either on holds. Examples:

* `X25519MLKEM768` in Chrome, Cloudflare and modern TLS.
* `mlkem768x25519` as the OpenSSH 10 default. The “connection is not using a post-quantum key exchange algorithm” warning in your own CTF SSH logs is this exact issue.

**NCSC migration timeline (2025):**

* by 2028: discovery, cryptographic inventory and a migration plan
* by 2031: priority migrations complete
* by 2035: full migration

**The practical answer is crypto agility:**

* know where you use cryptography (an inventory)
* prefer systems where algorithms can be swapped by configuration
* use AES-256 for long-lived data
