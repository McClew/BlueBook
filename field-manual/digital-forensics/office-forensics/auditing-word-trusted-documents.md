# Auditing Word Trusted Documents



***

A script to perform this analysis is: [word-trusted-documents.md](../../../toolbox/snippets/digital-forensics/word-trusted-documents.md "mention").

{% code lineNumbers="true" %}
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
