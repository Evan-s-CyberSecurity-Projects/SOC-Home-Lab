Issue 1: E_FAIL (Same UUID Fingerprint Panic)
Symptom: VirtualBox rejected the secondary boot sequence of the virtual appliance image.
Root Cause: Double-clicking pre-packaged assets registered identical Universally Unique Identifiers (UUIDs) within the hypervisor VDI cache.
Resolution: Purged the conflicting cache entries from the VirtualBox Command Center using a "Remove Only" flag and registered a fresh host registration boundary.

Issue 2: Syntax Errors in Local Schema Tuning
Symptom: Wazuh Agent service failed to start or ignored custom monitoring paths.
Root Cause: Malformed XML inside ossec.conf (specifically an unclosed <frequency> tag block).
Resolution: Analyzed the local ossec.log text dump to pinpoint the exact broken schema line notation, manually closed the structural tag, and forced a clean service state restart via Powershell.

Issue 3: 95% Host RAM Exhaustion & Service Throttling
Symptom: Delayed log shipping and a complete drop in active SIEM handshakes following a hard environment crash.
Root Cause: Running an enterprise Java application pipeline (Wazuh Indexer/OpenSearch) alongside a Windows 11 VM pushed the host machine beyond its physical RAM threshold, forcing massive disk swapping.
Resolution: Implemented resource optimization strategies:
Modified the Indexer JVM heap allocation rules inside /etc/wazuh-indexer/jvm.options from -Xmx2g down to -Xmx1g.
Transitioned the Wazuh Manager engine into a headless execution state (Shift + Start) to remove graphical buffer overhead.
Closed unneeded foreground host browser processes, allowing the background WazuhSvc data pipe to gracefully flush its tracking benchmarks.
