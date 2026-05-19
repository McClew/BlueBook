# Inspecting Word Add-ins

Malicious actors may use Word Add-ins to establish persistence or execute unauthorised code within the context of a user’s email client.

***

A script to perform this analysis is: [find-word-add-ins.md](../../../toolbox/snippets/digital-forensics/find-word-add-ins.md "mention").

{% code lineNumbers="true" %}
```powershell
# Define the registry paths where Word add-ins are registered
$RegistryPaths = @(
    "HKCU:\Software\Microsoft\Office\Word\Addins",
    "HKLM:\SOFTWARE\Microsoft\Office\Word\Addins",
    "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Office\Word\Addins"
)

$InstalledAddins = foreach ($Path in $RegistryPaths) {
    if (Test-Path $Path) {
        Get-ChildItem -Path $Path | ForEach-Object {
            [PSCustomObject]@{
                AddinName   = $_.PSChildName
                RegistryKey = $_.Name
                Description = (Get-ItemProperty -Path $_.PSPath).Description
                FriendlyName= (Get-ItemProperty -Path $_.PSPath).FriendlyName
                LoadBehavior= (Get-ItemProperty -Path $_.PSPath).LoadBehavior
            }
        }
    }
}

if ($InstalledAddins) {
    $InstalledAddins | Format-Table AddinName, FriendlyName, LoadBehavior -AutoSize
} else {
    Write-Host "No Word add-ins found in the registry paths." -ForegroundColor Yellow
}
```
{% endcode %}
