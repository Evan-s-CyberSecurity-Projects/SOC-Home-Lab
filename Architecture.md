Include a diagram: Even a simple Mermaid.js chart showing the data flow (Agent → Manager → Indexer → Dashboard).

Explain the "Why": Why did you choose Wazuh? Why did you use Sysmon? Why the specific tuning? This shows you understand the trade-offs of the tools you chose.


```mermaid
```mermaid
graph LR
    A[Kali Linux] -- "Simulated T1110" --> B[Windows 11]
    B -- "Telemetry" --> C[Wazuh Manager]
    C -- "Dashboard" --> D[Analyst Browser]
