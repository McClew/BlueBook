# Find Word Add-ins

{% code lineNumbers="true" %}
```powershell
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
