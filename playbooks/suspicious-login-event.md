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
---

# Suspicious Login Event

An unauthorised or Suspicious Login event occurs when a threat actor gains access, or attempts to gain access, to an organisational cloud identity (such as Microsoft 365 or Entra ID). This often serves as the "Beachhead" for further malicious activity, including data exfiltration, privilege escalation, or lateral movement within the cloud environment.

Unlike targeted BEC attacks, suspicious logins are often the result of credential stuffing, brute force, or session hijacking, where the goal is to establish a persistent foothold within the corporate network.

***

## Preparation

### Conditional Access Policies

Control Type: Technical & Preventative

Implement robust Conditional Access (CA) policies to restrict logins based on risk factors. This includes blocking legacy authentication and enforcing stricter controls for "High-Risk" sign-ins.

### Managed Device Compliance

Control Type: Technical & Preventative

Ensure that only "Compliant" or "Hybrid Joined" devices can access sensitive cloud resources. This prevents threat actors from using unmanaged, personal, or attacker-controlled machines even if they possess valid credentials.

### Multi-Factor Authentication (MFA)

Control Type: Technical & Preventative

Enforce MFA across the entire estate. Utilise "Phishing-Resistant" MFA (such as FIDO2 security keys or Certificate-Based Authentication) for privileged roles to mitigate the risk of MFA fatigue or proxy-based phishing.

### Logging & Monitoring

Control Type: Technical & Detective

Enable comprehensive logging, ensuring that Azure AD (Entra ID) Sign-in logs, Audit logs, and Non-Interactive sign-in logs are ingested into a central SIEM. Retention should meet the UK standard of at least 90 days.

### Geo-Fencing & IP Whitelisting

Control Type: Technical & Preventative

Configure "Named Locations" within the cloud tenant. Block authentications from countries where the organisation has no operational presence and whitelist known UK office egress IPs to reduce the attack surface.

### Cloud Detection & Response (CDR)

Control Type: Technical & Preventative, Detective

Deploy a CDR solution to provide advanced telemetry and automated responses. Key features include:

* Risk-Based Alerts: Integration with Identity Protection to flag "Leaked Credentials" or "Anomalous Token" usage.
* Impossible Travel: Automatic identification of sessions where the geographical distance between two logins is physically impossible to cover in the time elapsed.
* New Device Enrolment: Alerts for when a new, unmanaged device is registered to a user account or enrolled in MDM.

***

## Detection & Analysis

### Indicators of Attack (IOA)

* Brute Force/Password Spraying: A high volume of "Failure" logs from a single IP address across multiple usernames.
* MFA Spamming: A surge in MFA push notifications sent to a user in a short window, often during unsociable UK hours.
* Suspicious User Agent: Logins originating from "Headless" browsers, outdated operating systems, or known TOR exit nodes.
* Legacy Auth Attempts: Repeated attempts to authenticate via IMAP, POP3, or SMTP, which do not support modern MFA prompts.

### Indicators of Compromise (IOC)

* Impossible Travel: A successful login from London followed by a successful login from an overseas region within an hour.
* MFA Method Changes: The addition of a new "Authenticator App" or phone number that does not belong to the user.
* Token Theft: A successful login that bypasses MFA entirely, suggesting the use of a stolen session cookie (AiTM attack).
* ISP Mismatch: A user normally connecting via a known UK ISP (e.g., BT, Virgin Media) suddenly connecting via a foreign hosting provider or VPS.

### Triage & Scope

1. Session Context: Verify if the login matches the user’s typical working hours and device fingerprint.
2. Breadth Check: Use the SIEM to determine if the suspicious IP address has attempted to access other accounts within the tenant.
3. Privilege Review: Assess if the targeted account holds "Global Admin," "Security Admin," or "Conditional Access Admin" roles.

***

## Investigation

### Common Tactics, Techniques, and Procedures (TTPs)

#### Adversary-in-the-Middle (AiTM)

Threat actors use proxy tools to intercept the user’s password and, crucially, the session cookie. This allows them to bypass MFA and gain full access to the cloud session without needing the physical MFA device.

#### Session Hijacking

By stealing a valid session token from a compromised endpoint, attackers can "inject" themselves into an active cloud session, maintaining access even after a password change unless sessions are explicitly revoked.

#### MFA Fatigue (MFA Spamming)

The attacker sends dozens of MFA prompts to the victim’s phone, hoping the user will eventually click "Approve" out of frustration or by accident to stop the notifications.

#### Persistence via OAuth Apps

Attackers may register a "Malicious App" and trick the user into granting it "Read/Write" permissions. This provides a persistent back-door into the data (e.g., Mail, SharePoint) that survives password resets.

### Investigation Steps

#### Phase A: Persistence & Access (Immediate)

1. Sign-in Log Review: Filter for "Failure Reason" and "MFA Requirement" to identify how the actor got in.
2. MFA Audit: Check for any newly registered MFA methods or changed "Default" methods in the user's security info.
3. Device Enrolment: Review the "Devices" list in Entra ID/Intune for any unfamiliar hardware registered during the window of suspicion.

#### Phase B: Lateral Movement (Mid-Investigation)

4. Audit Log Analysis: Search for "Add member to role" or "Update policy" events to see if the attacker attempted to elevate their privileges.
5. App Permissions: Inspect the "Enterprise Applications" for any new apps granted `Mail.Read`, `Notes.Read.All`, or `Files.ReadWrite.All` permissions.
6. Resource Access: Identify which SharePoint sites or Teams channels were accessed by the suspicious session.

#### Phase C: Root Cause (Post-Containment)

7. Endpoint Health: Scan the user’s primary workstation for "Infostealer" malware that may have harvested cookies or credentials.
8. Phishing Link Discovery: Check the user's web history or "Junk" mail for links to known proxy/phishing sites visited prior to the login.

***

## Containment

### Account Disabling

Immediately disable the compromised user account in Entra ID/Active Directory to prevent further access.

### Session Revocation

Force a "Revoke Refresh Tokens" command via the admin portal or PowerShell to terminate all active sessions across all devices.

### MFA Reset

Remove any suspicious MFA methods and require the user to re-register their MFA factors in a secure, "In-Person" or verified environment.

### Password Reset

Perform a mandatory password reset, ensuring the new password meets organisational complexity requirements and is not reused from previous breaches.

### OAuth App Removal

Revoke any malicious or unverified third-party applications identified during the investigation to close persistent API access.
