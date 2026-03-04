# Inspecting Outlook Add-ins

Malicious actors may use Outlook Add-ins to establish persistence or execute unauthorised code within the context of a user’s email client.

***

A script to perform this analysis is: [get-outlookaddins.md](../../../toolbox/snippets/powershell/get-outlookaddins.md "mention").

{% code lineNumbers="true" %}
```powershell
$Paths = @(
    "HKCU:\Software\Microsoft\Office\Outlook\Addins",
    "HKLM:\SOFTWARE\Microsoft\Office\Outlook\Addins",
    "HKLM:\SOFTWARE\WOW6432Node\Microsoft\Office\Outlook\Addins"
)

foreach ($Path in $Paths) {
    if (Test-Path $Path) {
        Write-Host "`n--- Checking Path: $Path ---" -ForegroundColor Cyan
        Get-ChildItem $Path | ForEach-Object {
            $Name = $_.PSChildName
            $Desc = Get-ItemProperty $_.PSPath | Select-Object -ExpandProperty Description -ErrorAction SilentlyContinue
            $LoadBehavior = Get-ItemProperty $_.PSPath | Select-Object -ExpandProperty LoadBehavior -ErrorAction SilentlyContinue
            
            [PSCustomObject]@{
                AddinName    = $Name
                Description  = $Desc
                LoadBehavior = $LoadBehavior # '3' means it loads on startup
            }
        } | Format-Table -AutoSize
    }
}
```
{% endcode %}

The script enumerates subkeys within known Outlook Add-in registry paths. It specifically retrieves the Add-in Name, Description, and LoadBehavior.

In a DFIR context, this helps analysts:

1. Identify Anomalies: Spot suspicious or unrecognised add-ins.
2. Detect Persistence: Identify add-ins configured to launch automatically.
3. Audit Software: Verify the legitimate business tools installed across a workstation.

***

## Forensic Investigation Steps

{% stepper %}
{% step %}
### Verify Digital Signatures

For any unknown add-in name, locate the DLL/manifest file on the disk (usually found in a subkey value named `Manifest` or `DllPath`) and check for a valid code-signing certificate.
{% endstep %}

{% step %}
### Cross-Reference Descriptions

Malicious add-ins often have blank descriptions or mimic legitimate names (e.g., "Office Update Helper").
{% endstep %}

{% step %}
### Check Creation Timestamps

Use `Get-Item` on the registry key to check the `LastWriteTime`. If the timestamp aligns with the suspected compromise window, treat it as high-priority.
{% endstep %}
{% endstepper %}
