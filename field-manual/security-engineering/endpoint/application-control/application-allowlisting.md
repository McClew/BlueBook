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

# Application Allowlisting

## Positive Control as a Trust-Centric Model

Positive control in the form of allowed listing is described as <mark style="color:$primary;">**trust-centric**</mark> - in order for allowed listing to work, the organisation must trust its software logistics, support and supply chain to provide software that meets or exceeds both performance requirements and information security needs across the lifecycle of that software's use.

NIST and many other authorities argue that a positive control model is the best - if not the only sensible - approach when dealing with highly secure environments. These evironments are characterised by the willingness to spend money, time and effort in having strong, positive configuration management and control of all aspects of their systems.

In highly secure environments operating under positive control, user-written code is simply not allowed and attmepts to introduce it can get its user-as-creator fire or even prosecuted. This reflects the depth of commitement that positive control requires from the organisations culture and governance.&#x20;

The model works precisely because the organisation has made a deliverate decision to trust not only what has been explicitely authorised and to treat everything else as prohibited by default. This stands in direct contrast to the blocked listing model, where everything not explicitly prohibited is allowed.

***

## Administrative Effort & Practical Considerations

Making allowed listing for software control work requires administrative effort and the amount of effort is strongly related to the number of applications applications programs that need to be allowed, the frequency of their updates and the numbers of systems - servers, endpoints, or both - that need to be under positive control.

As new programs, or updates to existing programs are authorised for use, a "push" of the approed allowed list to all devices can help ensure that old versions can no longer run without intervention or authorisation.&#x20;

While new versions of apps are still being tested for compatibility with existing systems or for operability considerations, It managers can prevent the inadvertent update of endpoints or servers.

Individual users and departments may have legitimate business needs for unique software not used by others in the company and allowed listing systems can keep this under control fown to the by-name individual who is requesting exceptions or attempting to override the allowed listing system.

Allowed listing can also be an active part of seperation of duties and functions, preventing the execution of otheriwse authorised apps by otherwise authorised users when not accessing the system from the proper set of endpoints.

Additionally, allowed listing can be an active part in license and seat management if a particular app is licensed only to a fixed number of users. These capbilities make allowed listing a multifunctional ladministrative tool beyond its primary security role.
