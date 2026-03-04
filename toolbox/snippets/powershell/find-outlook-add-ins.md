# Get-OutlookAddIns

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
