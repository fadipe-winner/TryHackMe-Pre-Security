# Module 7: Cyber Security Fundamentals
## 🔗 Progress

- [x] Module 1: Introduction to Cyber Security
- [x] Module 2: Computer Fundamentals
- [x] Module 3: Operating Systems Basics
- [x] Module 4: Software Basics
- [x] Module 5: Network Fundamentals
- [x] Module 6: How the Web Works
- [x] Module 7: Attacks & Defenses
## Overview

In this module, I learned about some of the core principles used to protect
systems and information.

The main topics I covered included the CIA Triad, cryptography, symmetric
and asymmetric encryption, and basic security terminology such as
vulnerabilities, exploits, enumeration, credentials, and authentication.

This module also introduced me to the idea of identifying weaknesses in
systems and understanding how security professionals assess those weaknesses
in authorized environments.

---

# 1. The CIA Triad

The CIA Triad is a foundational cybersecurity model built around three
security principles:

- Confidentiality
- Integrity
- Availability

A secure system should consider all three.

---

## Confidentiality

Confidentiality is about preventing unauthorized access to sensitive
information.

In simple terms:

> Information should only be accessible to people or systems that are
> authorized to access it.

Examples of controls that can help protect confidentiality include:

- authentication
- access controls
- encryption
- permissions

For example, employee payroll information should not be accessible to every
employee in an organization.

---

## Integrity

Integrity is about ensuring that information remains accurate and is not
changed improperly or without authorization.

For example, if an attacker were able to change information in a company's
database without permission, the integrity of that information would be
compromised.

Mechanisms such as hashing, access controls, and digital signatures can help
support data integrity in different situations.

---

## Availability

Availability means ensuring that systems, services, and information remain
accessible when they are needed.

For example, if an organization's website or critical server becomes
unavailable, legitimate users may be unable to access the service.

Availability can be supported through things such as:

- backups
- redundancy
- monitoring
- maintenance
- disaster recovery
- protection against service disruption

---

## Understanding the CIA Triad

A simple way I remember the CIA Triad is:

| Principle | Question |
|---|---|
| Confidentiality | Who is allowed to see the information? |
| Integrity | Has the information been changed improperly? |
| Availability | Can the information/service be accessed when needed? |

---

# 2. Introduction to Cryptography

Cryptography is the use of mathematical techniques to protect information.

One of its major uses is encryption, where readable information is converted
into a form that is difficult to understand without the correct key.

Some important terms I learned are:

### Plaintext

Plaintext is the original readable information.

For example:

Hello

### Ciphertext

Ciphertext is the unreadable or scrambled-looking result produced after
plaintext has been encrypted.

### Key

A cryptographic key is a value used by a cryptographic algorithm during
encryption or decryption.

The security of modern encryption depends heavily on protecting the
appropriate keys.

### Algorithm

An algorithm is the set of mathematical rules or operations used to perform
the cryptographic process.

---

# 3. Encryption and Decryption

Encryption converts plaintext into ciphertext.

A simplified way to represent it is:

Plaintext
    ↓
Encryption Algorithm + Key
    ↓
Ciphertext

Decryption reverses the process when the correct key and algorithm are used:

Ciphertext
    ↓
Decryption Algorithm + Key
    ↓
Plaintext

Encryption is especially important for protecting confidential information.

---

# 4. Symmetric Encryption

Symmetric encryption uses the same secret key for encryption and decryption.

The basic idea is:

Plaintext
    ↓
Secret Key
    ↓
Encryption
    ↓
Ciphertext
    ↓
Same Secret Key
    ↓
Decryption
    ↓
Plaintext

Both sides therefore need access to the secret key.

### Advantages

Symmetric encryption is generally fast and efficient, which makes it useful
for encrypting larger amounts of data.

### Challenge

The secret key needs to be shared and protected securely.

If an unauthorized person obtains the key, they may be able to decrypt the
protected information.

An important symmetric encryption algorithm to recognize is:

- AES (Advanced Encryption Standard)

I do not need to understand the mathematics behind AES at this stage, but I
should understand what symmetric encryption means and why protecting the key
is important.

---

# 5. Asymmetric Encryption

Asymmetric encryption uses a pair of mathematically related keys:

- Public key
- Private key

The public key can be shared, while the private key should be kept secret by
its owner.

This solves some of the key-sharing problems found with symmetric
cryptography.

Asymmetric cryptography is used in technologies such as secure
communications and digital signatures.

Algorithms I should recognize include:

- RSA
- ECC (Elliptic Curve Cryptography)

---

# 6. Symmetric vs Asymmetric Cryptography

| Feature | Symmetric | Asymmetric |
|---|---|---|
| Keys | One shared secret key | Public/private key pair |
| Speed | Generally faster | Generally slower |
| Large amounts of data | Well suited | Usually not used alone for bulk encryption |
| Key sharing | Secret key must be protected/shared securely | Public key can be openly shared |
| Examples | AES | RSA, ECC |

In real systems, symmetric and asymmetric cryptography can be used together.

For example, secure protocols can use asymmetric cryptography to help
establish trust or exchange key material and then use efficient symmetric
encryption to protect the actual communication.

---

# 7. Hashing

Another concept related to cryptography is hashing.

Hashing is different from encryption.

A hash function takes input data and produces a fixed-size output called a
hash or digest.

Unlike encryption, hashing is designed to be one-way rather than something
that is normally decrypted back to the original value.

Hashes can be useful for checking data integrity.

A cryptographic hash algorithm I should recognize is:

- SHA-256

Password storage also commonly involves specialized password-hashing
techniques rather than storing passwords as plaintext.

The important distinction for me is:

Encryption → designed to be reversible with the appropriate key

Hashing → designed to be one-way

---

# 8. Vulnerabilities

A vulnerability is a weakness or flaw in a system, application, configuration,
or process that could potentially be abused.

Vulnerabilities can exist because of things such as:

- software bugs
- insecure configurations
- weak access controls
- outdated software
- design weaknesses

Finding a vulnerability does not automatically mean that it has been
exploited.

---

# 9. Exploits

An exploit is a method or technique that takes advantage of a vulnerability
to produce unintended behaviour.

The distinction I learned is:

Vulnerability → the weakness

Exploit → a way of taking advantage of that weakness

For example, a software flaw may be the vulnerability, while a technique
that successfully abuses the flaw would be an exploit.

Security testing should only be performed against systems where permission
has been given, such as authorized labs and training environments.

---

# 10. Enumeration

Enumeration is the process of actively gathering detailed information about
a system or service.

Depending on the authorized assessment, this might involve identifying things
such as:

- users
- services
- directories
- files
- hostnames
- application information

Enumeration can help a security professional understand what is exposed and
what may require further investigation.

From a defensive perspective, unusual or repeated enumeration activity can
also be something analysts investigate in logs.

---

# 11. Credentials and Authentication

## Credentials

Credentials are information used to help prove a user's identity.

Examples can include:

- username and password
- authentication token
- certificate

Credentials should be protected because stolen credentials may allow an
unauthorized person to access an account.

## Authentication

Authentication is the process of verifying that a user, device, or system is
who it claims to be.

A simple example is:

User provides credentials
        ↓
System verifies them
        ↓
Identity is authenticated

Authentication answers:

> "Who are you, and can you prove it?"

Authorization is different.

Authorization determines:

> "Now that we know who you are, what are you allowed to access?"

---

# 12. Web Content Discovery

The module also introduced me to the concept of discovering web content that
may not be directly linked from a website's visible pages.

A web server may contain different:

- directories
- files
- endpoints
- application paths

Understanding this concept is useful because exposed or forgotten resources
can sometimes create security risks.

From a defensive perspective, repeated requests to many unusual paths can
also appear in web server, proxy, WAF, or other security logs.

---

# 13. Gobuster

I was introduced to Gobuster as a command-line tool that can be used in
authorized security testing environments for content discovery.

It can test possible directory or file names against a web application using
a supplied wordlist.

The important concept I took from this exercise was not memorizing the
command syntax, but understanding what content discovery is doing:

Possible names
      ↓
Requests sent to authorized target
      ↓
Server responses examined
      ↓
Potential resources identified

This also helped me understand what this kind of activity might look like
from a defender's perspective: many requests for different paths from the
same source in a short period of time could be worth investigating.

---

# 14. Password Security and Hydra

The module also introduced Hydra in a controlled lab environment as an
example of a tool used to test authentication security.

The important lesson for me was understanding why weak and reused passwords
are dangerous rather than focusing on memorizing attack commands.

Organizations can reduce password-related risks through controls such as:

- strong password policies
- multi-factor authentication (MFA)
- rate limiting
- account lockout protections
- monitoring failed authentication attempts
- detecting unusual login behaviour

From a SOC perspective, a large number of failed authentication attempts can
be an indicator worth investigating.

---

# 15. Important Security Terminology

Some of the terminology I learned can be summarized as:

| Term | Meaning |
|---|---|
| Vulnerability | A weakness that could potentially be abused |
| Exploit | A method of taking advantage of a vulnerability |
| Enumeration | Actively gathering detailed information about a target |
| Credential | Information used to help prove identity |
| Authentication | Verifying an identity |
| Authorization | Determining what an authenticated identity is allowed to access |
| Encryption | Converting readable information into protected ciphertext |
| Decryption | Converting ciphertext back into readable plaintext using the appropriate key |
| Hashing | Producing a one-way digest from data |

---

# 16. Defensive / SOC Perspective

One of the most useful things I took from this module is that understanding
how systems can be tested also helps me understand what suspicious activity
may look like from the defensive side.

For example, an analyst may investigate:

- repeated failed login attempts
- unusual authentication activity
- large numbers of requests to nonexistent web paths
- access to unexpected resources
- suspicious source IP addresses
- unusual changes to important files
- unexpected service interruptions

However, one event by itself does not automatically prove an attack.

A SOC analyst needs to gather additional context from logs, alerts, network
activity, endpoint information, authentication records, and other available
evidence before reaching a conclusion.

---

# Key Takeaway

My biggest takeaway from this module is that cybersecurity is built around
protecting the confidentiality, integrity, and availability of systems and
information.

I developed a foundational understanding of cryptography, including
plaintext, ciphertext, keys, encryption, decryption, symmetric encryption,
asymmetric encryption, and hashing.

I also learned the difference between vulnerabilities and exploits and was
introduced to concepts such as enumeration, authentication, credentials,
and web content discovery.

Seeing these concepts from both an offensive and defensive perspective helped
me understand why learning how attacks and security testing work can also
help a defender recognize suspicious behaviour.

These are still foundational skills, but they give me a stronger base as I
continue toward more hands-on SOC and Blue Team learning.
