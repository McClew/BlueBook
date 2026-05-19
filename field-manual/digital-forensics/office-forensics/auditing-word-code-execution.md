# Auditing Word Code Execution



***

A script to perform this analysis is: [word-code-execution-audit.md](../../../toolbox/snippets/digital-forensics/word-code-execution-audit.md "mention").

{% code lineNumbers="true" %}
```powershell
$regPath = "HKCU:\Software\Policies\Microsoft\Office\16.0\word\security"
$fallbackPath = "HKCU:\Software\Microsoft\Office\16.0\Word\Security"

function Check-MacroSetting ($path) {
    if (Test-Path $path) {
        $macroLevel = Get-ItemProperty -Path $path -Name "VBAWarnings" -ErrorAction SilentlyContinue
        if ($macroLevel) {
            return $macroLevel.VBAWarnings
        }
    }
    return $null
}

$result = Check-MacroSetting $regPath
if ($null -eq $result) {
    $result = Check-MacroSetting $fallbackPath
}

Write-Host "--- Word Malicious Document Susceptibility Report ---" -ForegroundColor Cyan
if ($null -eq $result) {
    Write-Host "Macro Setting: Default (User-defined / Not explicitly blocked by admin)." -ForegroundColor Yellow
    Write-Host "Risk: Moderate. Users can manually click 'Enable Content' on malicious documents." -ForegroundColor Yellow
} else {
    switch ($result) {
        1 { Write-Host "Macro Setting: 1 (All macros enabled)." -ForegroundColor Red; Write-Host "RISK: HIGH. Malicious documents will run code instantly without warning." -ForegroundColor Red }
        2 { Write-Host "Macro Setting: 2 (Disable all macros with notification)." -ForegroundColor Yellow; Write-Host "Risk: Moderate. Relies on user training not to click 'Enable Content'." -ForegroundColor Yellow }
        3 { Write-Host "Macro Setting: 3 (Disable all except digitally signed)." -ForegroundColor Green; Write-Host "Risk: Low. Only trusted code runs." -ForegroundColor Green }
        4 { Write-Host "Macro Setting: 4 (Disable all macros without notification)." -ForegroundColor Green; Write-Host "Risk: Very Low. Macros cannot execute code." -ForegroundColor Green }
    }
}
```
{% endcode %}
