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

# Secure Protocols

Intro

***

## Services & Protocols

### TLS

It authenticates the server (and optionally the client\_ and then encrypts and integrity-protects the session. It is hybrid cryptography in action:

* asymmetric cryptography authenticates the server and agrees the session keys
* symmetric cryptography then protects the bulk data

It sits between the transport layer and the application, so HTTP, SMTP, IMAP, LDAP and others can all run over it.

### IPsec



### SSH



### SFTP & FTPS



### HTTPS



### S/MIME



### DNSSEC



### SNMPv3



***

## Common Use Cases



***

## Limitations & Vulnerabilities

