# Attack Script
@echo off
:: Target: Localhost / User: attacker_test
:: Purpose: Simulate an automated credential access attempt to trigger Sysmon/Wazuh telemetry.

echo Starting adversary simulation...
for /L %%i in (1,1,20) do (
    net use \\localhost /user:attacker_test wrongpassword123 >nul 2>&1
    echo Attempt %%i sent.
)
echo Simulation complete. Check SIEM dashboard for high-fidelity alerts.


# FIM script

# Purpose: Generate file activity in C:\test to validate Wazuh FIM rule states.
$testPath = "C:\test"

# 1. Ensure directory exists
if (-not (Test-Path $testPath)) {
    New-Item -ItemType Directory -Path $testPath | Out-Null
}

# 2. Create a test asset (Generates an Inventory Snapshot / Create Event)
Write-Host "Creating test file..."
"Initial baseline telemetry data" | Out-File "$testPath\fim_canary.txt"
Start-Sleep -Seconds 2

# 3. Modify the asset (Generates a Cryptographic Event Journal alert)
Write-Host "Modifying test file..."
"Attacker appended data" | Add-Content "$testPath\fim_canary.txt"
Start-Sleep -Seconds 2

# 4. Cleanup
Write-Host "Cleaning up..."
Remove-Item "$testPath\fim_canary.txt"
Write-Host "FIM Cycle complete. Verify alerts in the Wazuh Dashboard."



