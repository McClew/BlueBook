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

# Word Trusted Documents

{% code overflow="wrap" lineNumbers="true" %}
```powershell
$trustedDocsPath = "HKCU:\Software\Microsoft\Office\16.0\Word\Security\Trusted Documents\TrustRecords"

if (Test-Path $trustedDocsPath) {
    Write-Host "Files this user has manually approved in the past:" -ForegroundColor Yellow
    Get-Item -Path $trustedDocsPath | Select-Object -ExpandProperty Property
} else {
    Write-Host "No manually trusted documents found." -ForegroundColor Green
}
```
{% endcode %}
