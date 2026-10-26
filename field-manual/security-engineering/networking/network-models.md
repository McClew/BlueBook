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

# Network Models

## OSI Model

The Open Systems Interconnection (OSI) model is a conceptual framework that standardises the functions of a communication system into seven distinct categories.

<mark style="color:$info;">**Think of it as a troubleshooting map:**</mark> when something breaks or is attacked, it can help determine which layer is affected.

<table data-search="false"><thead><tr><th width="87">Layer</th><th width="129">Name</th><th>Function</th><th>Common Protocols</th><th>Common Attacks</th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>7</strong></mark></td><td><mark style="color:blue;"><strong>Application</strong></mark></td><td>Network process to application (User interface).</td><td>HTTP, HTTPS, FTP, SMTP, DNS, SSH</td><td>Cross-Site Scripting (XSS), SQL Injection</td></tr><tr><td><mark style="color:blue;"><strong>6</strong></mark></td><td><mark style="color:blue;"><strong>Presentation</strong></mark></td><td>Data representation, encryption, and decryption.</td><td>SSL, TLS, JPEG, ASCII</td><td>SSL Stripping, Malformed data attacks</td></tr><tr><td><mark style="color:blue;"><strong>5</strong></mark></td><td><mark style="color:blue;"><strong>Session</strong></mark></td><td>Interhost communication (establishing, managing, and terminating sessions).</td><td>NetBIOS, RPC, PPTP</td><td>Session Hijacking, Man-in-the-Middle (MitM)</td></tr><tr><td><mark style="color:green;"><strong>4</strong></mark></td><td><mark style="color:green;"><strong>Transport</strong></mark></td><td>End-to-end connections and reliability (segmentation).</td><td>TCP, UDP</td><td>SYN Flood, UDP Flood, Port Scanning</td></tr><tr><td><mark style="color:yellow;"><strong>3</strong></mark></td><td><mark style="color:yellow;"><strong>Network</strong></mark></td><td>Path determination and IP (routing).</td><td>IPv4, IPv6, ICMP, IPsec, IGMP</td><td>Ping of Death, IP Spoofing, Route Poisoning</td></tr><tr><td><mark style="color:orange;"><strong>2</strong></mark></td><td><mark style="color:orange;"><strong>Data Link</strong></mark></td><td>MAC and LLC (physical addressing).</td><td>Ethernet, ARP, VLANs (802.1Q), STP</td><td>ARP Spoofing, MAC Flooding, VLAN Hopping</td></tr><tr><td><mark style="color:orange;"><strong>1</strong></mark></td><td><mark style="color:orange;"><strong>Physical</strong></mark></td><td>Media, signal, and binary transmission.</td><td>USB, Bluetooth, 802.11 (Wi-Fi physical layer)</td><td>Wiretapping, Jamming, Cable cutting</td></tr></tbody></table>

***

## TCP/IP Model

The TCP/IP model is older and more practical than OSI, as it describes the protocols actually used on the Internet. It condenses the seven OSI layers into four.

<table><thead><tr><th width="200">TCP/IP</th><th width="135">OSI Layers</th><th>Description</th></tr></thead><tbody><tr><td><mark style="color:blue;"><strong>Application</strong></mark></td><td><mark style="color:blue;"><strong>5, 6, 7</strong></mark></td><td>Handles high-level protocols, issues of representation, encoding, and dialog control.</td></tr><tr><td><mark style="color:green;"><strong>Transport</strong></mark> </td><td><mark style="color:green;"><strong>4</strong></mark></td><td>Deals with quality of service, reliability, and flow control. (TCP and UDP).</td></tr><tr><td><mark style="color:yellow;"><strong>Internet</strong></mark> </td><td><mark style="color:yellow;"><strong>3</strong></mark></td><td>Connects independent networks and routes packets across them. (IP, ICMP).</td></tr><tr><td><mark style="color:orange;"><strong>Network Access / Link</strong></mark></td><td><mark style="color:orange;"><strong>1, 2</strong></mark></td><td>Defines how data is physically sent through the network, encompassing both the logical link and physical media. (Ethernet, ARP).</td></tr></tbody></table>

***

## Application Examples

Below are some example scenarios focusing on mapping protocols and identifying vulnerabilities.

### Example 1: Identifying the Attack Layer

A security analyst is reviewing firewall logs. They notice a massive spike in half-open connection requests originating from a single IP address, overwhelming a web server.

What type of attack is this, and at what OSI layer is it occurring?

{% stepper %}
{% step %}
#### Identify the characteristic of the attack

The logs show "half-open connection requests." This describes the first step of the TCP three-way handshake (a SYN packet sent, but the final ACK is never received or sent).
{% endstep %}

{% step %}
#### Determine the attack type

A flood of SYN packets designed to exhaust server resources is known as a SYN Flood attack.
{% endstep %}

{% step %}
#### Map the protocol to the OSI layer

The attack manipulates TCP (Transmission Control Protocol). TCP operates at Layer 4.
{% endstep %}

{% step %}
#### Conclusion

This is a SYN Flood attack occurring at the Transport Layer (Layer 4) of the OSI model.
{% endstep %}
{% endstepper %}

### Example 2: Protocol Mapping and Security Controls

An organisation needs to secure data in transit between a branch office and headquarters over the public internet. They decide to implement an IPsec VPN.

Which layer of the TCP/IP model does this solution protect?

{% stepper %}
{% step %}
#### Identify the core technology

The solution being implemented is IPsec (Internet Protocol Security).
{% endstep %}

{% step %}
#### Map the protocol to the OSI model

IPsec operates by encrypting and authenticating IP packets. IP operates at the Network Layer (Layer 3) of the OSI model.
{% endstep %}

{% step %}
#### Translate to the TCP/IP model

The Network Layer (Layer 3) of the OSI model maps directly to the Internet Layer of the TCP/IP model.
{% endstep %}

{% step %}
#### Conclusion

The IPsec VPN protects data at the Internet Layer of the TCP/IP model.
{% endstep %}
{% endstepper %}
