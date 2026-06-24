To validate the security infrastructure, a Credential Access via Brute Force attack was simulated.
Adversary Behavior Emulation
From a command shell on the Windows Target, a rapid execution script loop was launched to mimic an automated adversary attempting to brute-force network shares:
DOS
for /L %i in (1,1,20) do net use \\localhost /user:attacker_test wrongpassword123

Blue Team Detection & Triage Narrative
The Telemetry Catch: Rather than relying solely on basic Windows Logon Failure logs (Event ID 4625), the advanced Sysmon pipeline successfully intercepted the process lineage.
The High-Fidelity Alert: The Wazuh SIEM captured 20 concurrent counts of an elevated cmd.exe terminal spawning child processes of net.exe.
Analysis: This structural correlation proves that the lab successfully detects the execution of native system discovery and mapping tools ("Living off the Land" techniques) rather than generic baseline operational noise.

## Conclusion
* **Status:** Resolved / Detection Validated.
* **Tuning Recommendation:** The current rule successfully caught the simulation. Future iterations will focus on reducing noise for administrative service accounts using similar `net.exe` commands.
