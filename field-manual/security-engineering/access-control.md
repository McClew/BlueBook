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

# Access Control

<table><thead><tr><th width="98">Model</th><th width="198">Who/What Determines Access?</th><th width="133">Flexibility</th><th width="316">Primary Use Case</th></tr></thead><tbody><tr><td>DAC</td><td>The Data Owner</td><td><i class="fa-chevron-up" style="color:$success;">:chevron-up:</i> <mark style="color:$success;">High</mark></td><td>Standard commercial operating systems (Windows, Linux file permissions).</td></tr><tr><td>MAC</td><td>The System (based on labels)</td><td><i class="fa-chevron-down" style="color:$warning;">:chevron-down:</i> <mark style="color:$warning;">low</mark></td><td>Military, intelligence, or highly secure siloed environments.</td></tr><tr><td>RBAC</td><td>The Administrator (based on job role)</td><td><i class="fa-dash" style="color:$primary;">:dash:</i> <mark style="color:$primary;">Medium</mark></td><td>Large enterprises with high employee turnover or standardized departments.</td></tr><tr><td>ABAC</td><td>The Policy Engine (based on variables)</td><td><i class="fa-chevrons-up" style="color:$success;">:chevrons-up:</i> <mark style="color:$success;">Very High</mark></td><td>Cloud environments, Zero Trust architectures, and remote workforce access.</td></tr></tbody></table>

***

## Discretionary Access Control (DAC)

In DAC, the creator or owner of the resource dictates who gets access and what privileges they have (read, write, execute).

**Mechanism:** Access Control Lists (ACLs) attached to the resource.

**Pros:** Highly flexible and easy for users to manage their own data sharing.

**Cons:** Vulnerable to user error and malware; if a user is compromised, all data they own or have access to is also compromised.

**Implementation Example:** A user right-clicking a Google Drive document and manually granting "Edit" permissions to a colleague's email address.

***

## Mandatory Access Control (MAC)

In MAC, the system enforces access decisions based on strict policies, regardless of what the data owner wants. It relies on comparing a user's clearance level with a data object's classification label.

**Mechanism:** Security Labels (e.g., Top Secret, Secret, Confidential) and Clearance matches.

**Pros:** Extremely secure; limits the damage of compromised accounts because users cannot override the system's security labels.

**Cons:** Very rigid, difficult to implement, and creates high administrative overhead.

**Implementation Example:** SE-Linux (Security-Enhanced Linux) restricting a process from accessing a file, even if the user running the process is an administrator, because the process lacks the specific "Top Secret" label.

***

## Role-Based Access Control (RBAC)

In RBAC, access is granted based on the user's role or job function within the organization, rather than their individual identity. Users are assigned to roles, and permissions are assigned to those roles.

**Mechanism:** Group memberships and role assignments.

**Pros:** Radically simplifies administration for onboarding, offboarding, and role changes (e.g., if someone changes departments, you just change their role group, rather than updating 50 individual file permissions).

**Cons:** Can lead to "role explosion" if roles are not carefully defined and audited.

**Implementation Example:** Adding a new hire to the "HR\_Managers" Active Directory group, which automatically grants them access to the payroll system and employee records share.

***

## Attribute-Based Access Control (ABAC)

ABAC is the most granular model. It evaluates a set of attributes (subject, object, action, and environmental conditions) against a set of rules to make a dynamic access decision.

**Mechanism:** IF/THEN policy engines evaluating real-time variables.

**Pros:** Context-aware and highly adaptable; the foundation of modern Zero Trust security.

**Cons:** Complex to initially design and requires a robust centralized policy engine.

**Implementation Example:** An AWS IAM policy that allows a developer to access a database _only_ if they are using a company-issued device, connected from a known corporate IP address, and accessing it during standard business hours.

***

## Applicability Assessment

Below are some scenarios showing how the different Access Controls can be assessed based on applicability, allowing us to pick the best Access Control for the clients situation and requirements:

### Example 1: The High-Turnover Hospital

A large hospital experiences frequent staff changes. Nurses often cover different wards, and temporary staff are common. The administration needs a way to quickly grant and revoke access to patient records based on a staff member's current assignment, minimising administrative overhead.

Which model is best?

{% stepper %}
{% step %}
#### Identify the key constraint

The core issue is "frequent staff changes" and the need to "quickly grant and revoke access... minimising administrative overhead."
{% endstep %}

{% step %}
#### Evaluate DAC

DAC relies on data owners managing access. In a hospital, having doctors or patients manually manage access for every new nurse would be chaotic and unscalable.
{% endstep %}

{% step %}
#### Evaluate MAC

MAC uses rigid clearance levels. While security is important, MAC is often too inflexible for dynamic environments where rapid access changes are needed.
{% endstep %}

{% step %}
#### Evaluate RBAC

RBAC assigns permissions to roles (e.g., "ER Nurse," "Pediatrics Nurse"). When a temp joins, they are assigned the role; when they leave, the role is removed. This perfectly addresses the need for efficient administration in a high-turnover environment.

RBAC is the correct choice.
{% endstep %}
{% endstepper %}

### Example 2: The Defense Contractor

A company developing targeting systems for the military requires strict control over design documents. Employees must only access information strictly necessary for their specific component. Furthermore, it is unacceptable for any employee to independently decide to share these documents, even if they created them.

Which model is best?

{% stepper %}
{% step %}
#### Identify the key constraint

The constraints are "strict control," "only access information strictly necessary," and critically, "unacceptable for any employee to independently decide to share."
{% endstep %}

{% step %}
#### Evaluate DAC

DAC explicitly allows creators (owners) to share documents. This directly violates the requirement that employees cannot independently share data.
{% endstep %}

{% step %}
#### Evaluate RBAC

While RBAC can enforce least privilege, it doesn't inherently prevent a user with access from copying or sharing data if the underlying system allows it.
{% endstep %}

{% step %}
#### Evaluate MAC

MAC enforces access through system-defined labels and clearances. Users _cannot_ override these rules to share data, even data they created. This strict, system-enforced control is exactly what's required for military-grade confidentiality.

MAC is the correct choice.
{% endstep %}
{% endstepper %}
