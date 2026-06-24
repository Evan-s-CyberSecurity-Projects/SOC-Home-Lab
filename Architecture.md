Include a diagram: Even a simple Mermaid.js chart showing the data flow (Agent → Manager → Indexer → Dashboard).

Explain the "Why": Why did you choose Wazuh? Why did you use Sysmon? Why the specific tuning? This shows you understand the trade-offs of the tools you chose.


```mermaid
graph LR
    A[Kali Linux (Attacker)] -- "Simulated T1110" --> B[Windows 11 (Target)]
    B -- "Sysmon/Wazuh Agent Telemetry" --> C[Wazuh Manager (SIEM)]
    C -- "HTTPS (Dashboard)" --> D[Analyst Browser]
