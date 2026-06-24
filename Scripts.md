# Security Engineering & Threat Emulation Scripts

This repository contains automated scripts used to validate defensive controls, generate telemetry, and perform baseline testing within the lab environment.

---

## 1. Credential Access Simulator (Brute Force)
* **Purpose:** Emulates automated credential discovery and brute-force attempts on local network shares.
* **MITRE ATT&CK Mapping:** [T1110.001 - Brute Force: Password Guessing](https://attack.mitre.org/techniques/T1110/001/)
* **Detection Goal:** Validate Sysmon Event ID 1 (Process Creation) and Event ID 3 (Network Connection) logs within the Wazuh SIEM.

```batch
@echo off
:: Target: Localhost / User: attacker_test
echo Starting adversary simulation...
for /L %%i in (1,1,20) do (
    net use \\localhost /user:attacker_test wrongpassword123 >nul 2>&1
    echo Attempt %%i sent.
)
echo Simulation complete. Check SIEM dashboard for high-fidelity alerts.


# Define test path
$testPath = "C:\test"

# 1. Ensure directory exists
if (-not (Test-Path $testPath)) { New-Item -ItemType Directory -Path $testPath | Out-Null }

# 2. Create a test asset (Baseline Snapshot)
"Initial baseline telemetry data" | Out-File "$testPath\fim_canary.txt"
Start-Sleep -Seconds 2

# 3. Modify the asset (Generate Cryptographic Event)
"Attacker appended data" | Add-Content "$testPath\fim_canary.txt"
Start-Sleep -Seconds 2

# 4. Cleanup
Remove-Item "$testPath\fim_canary.txt"
Write-Host "FIM Cycle complete. Verify alerts in the Wazuh Dashboard."
