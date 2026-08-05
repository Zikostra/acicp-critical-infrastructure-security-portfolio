# ACICP201 Assignment 02

## Firewall Log Backup, Event Interpretation and Network Operations Report

**Student:** Praise Nze  
**Registration Number:** C11/26/ACIS/17358  
**Course:** ACICP201 – Network Security Engineering  
**Programme:** Advanced Critical Infrastructure Security  
**Week:** 2  
**Due:** Friday, 14 August 2026, 11:59 PM WAT

## Assignment Scope

This response uses only the fictional event samples supplied in the assignment. It does not rely on production firewall access or real organizational logs.

# Task 1: Firewall Log Backup Plan

## Log Sources and Log Types

| Log Source | Required Log Types |
|---|---|
| Internet edge firewall | Traffic, deny, threat, administrator, configuration and system-health logs |
| Internal segmentation firewall | Inter-zone traffic, policy deny, threat, configuration and system-health logs |
| VPN gateway | Authentication, MFA, session, tunnel, administrator and health logs |
| DMZ firewall | Internet-to-DMZ traffic, threat, deny, NAT, configuration and health logs |
| Jump-host firewall | Jump-zone access, allowlist violations, authentication and administrator logs |
| SIEM/log collector | Ingestion status, parsing, correlation, alert, access, health and audit logs |

## Transfer and Protection

Logs should be securely forwarded to a central SIEM or collector, preferably through encrypted syslog over TLS. Backups should be encrypted, access-controlled and stored separately from the source system. Every export should receive a SHA-256 hash. Original logs should be protected from alteration, while analysts use verified working copies.

## Retention and Backup Schedule

| Storage Tier | Proposed Retention | Purpose |
|---|---|---|
| Hot | 0–30 days | Immediate search, monitoring and incident triage |
| Warm | 31–90 days | Investigation and operational review |
| Cold archive | 91–365 days | Compliance, historical investigation and long-term evidence |
| Legal/compliance hold | Until formally released | Preserve records linked to incidents, audits or legal matters |

| Activity | Frequency |
|---|---|
| Incremental backup | Daily |
| Full export | Weekly |
| Archive review | Monthly |
| Restore test | Quarterly |
| Additional incident export | After a major incident or significant configuration change |

## Evidence Controls

SHA-256 hashing, synchronized NTP time, chain-of-custody records, role-based access control, encryption, immutable storage where available, tamper detection and quarterly restoration testing should be used.

# Task 2: Log Storage and Retention Calculations

| Question | Working | Answer |
|---|---|---:|
| A | 2.8 + 1.6 + 0.7 + 0.9 | 6.0 GB/day |
| B | 6.0 × 40% remaining | 2.4 GB/day |
| C | 2.4 × 90 | 216 GB |
| D | 2.4 × 365 | 876 GB |
| E | 876 × ₦18 | ₦15,768/month |
| F | 6.0 × 1.12² | 7.5264 ≈ 7.53 GB/day |
| G | (1,000 ÷ 100) × 35 | 350 minutes = 5 hours 50 minutes |

**Assumption for G:** 1 TB is treated as 1,000 GB. Under a 1,024 GB assumption, the estimated time would be approximately 5 hours 58 minutes.

# Task 3: Event Interpretation

| ID | Event Type and Likely Meaning | Severity | Required Response | Escalate? |
|---|---|---|---|---|
| E01 | Unauthorised Modbus attempt from CORP-LAN to OT-SCADA | Critical | Identify and contain the source; preserve related evidence; verify deny control | Yes, immediately |
| E02 | Approved VPN-to-jump-zone SSH session with MFA during change window | Low | Verify change ticket and monitor routinely | No |
| E03 | Web exploit signature against DMZ; session reset | High | Review server/WAF logs, patch status and follow-on activity | Yes |
| E04 | Successful administrator login outside maintenance window | Medium | Verify identity, approval and actions performed | Yes if not approved |
| E05 | OT workstation attempted outbound internet HTTPS connection | Critical | Investigate and isolate/monitor the workstation; review process and destination | Yes, immediately |
| E06 | Normal syslog forwarding from DMZ to SIEM | Low | Confirm time, event flow and ingestion health | No |
| E07 | 950 MB corporate upload to internet in eight minutes | High | Validate business purpose; inspect DLP, proxy and endpoint evidence | Yes |
| E08 | Non-allowlisted RDP attempt from jump zone to OT engineering station | Critical | Identify account/process; verify work order; preserve evidence | Yes, immediately |

# Task 4: Evidence Handling and Chain of Custody

1. Collect logs through secure centralized forwarding and export only the required date range.
2. Record the source device, timezone, collection time, log type, case reference and collector.
3. Protect the originals as read-only or immutable records.
4. Generate a SHA-256 hash immediately after export and record it with the filename and file size.
5. Restrict repository access to authorised custodians, incident responders, forensic analysts and approved legal/compliance personnel.
6. Verify NTP status, timezone and time drift across all evidence sources.
7. Record every transfer in a chain-of-custody register, including sender, receiver, date, purpose and hash verification.
8. Transfer evidence through encrypted, access-controlled channels and provide only the minimum necessary information.
9. Retain records according to policy and legal hold.
10. Securely dispose of expired evidence only after documented approval.

# Task 5: Mini Network-Operations Report

This report reviews fictional firewall events and proposes a log-backup approach for a critical infrastructure environment containing an internet edge, corporate network, DMZ, VPN zone, engineering jump zone and OT-SCADA segment. The review shows that the environment has useful visibility across access, threat, administrative and traffic events, but the value of those records depends on reliable forwarding, protected retention, synchronized time and tested restoration.

The most serious events are the unauthorised Modbus request from the corporate network to the OT-SCADA zone, the outbound internet attempt from an OT workstation and the non-allowlisted RDP attempt from the jump zone to an OT engineering station. All three events were denied, which demonstrates useful preventive control, but each indicates behaviour that requires immediate investigation. The web-exploit attempt against the DMZ and the large corporate upload also require urgent review.

NETWORK ZONES REVIEWED

The fictional environment includes the INTERNET, CORP-LAN, DMZ-WEB, VPN-ZONE, JUMP-ZONE, ADMIN-NET, FIREWALL, SIEM and OT-SCADA zones. The internet edge controls external access. The DMZ contains public-facing services. The VPN zone provides authenticated remote access. The jump zone acts as a controlled path toward sensitive engineering systems. The administrative network supports privileged firewall access. The SIEM receives centralized events. The OT-SCADA zone contains industrial systems and therefore requires the strictest segmentation and monitoring.

SUMMARY OF LOG BACKUP STATUS

The proposed backup design sends traffic, threat, authentication, VPN, configuration-change, administrator-activity and system-health logs to a central SIEM or log collector. Secure forwarding should use encrypted syslog or a protected management path. Daily incremental backups, weekly full exports, monthly archive reviews and quarterly restore tests provide a practical operating schedule.

The design uses thirty days of hot storage for rapid investigation, days thirty-one to ninety in warm storage and the remaining period up to one year in encrypted cold archive. At the calculated compressed rate of 2.4 GB per day, ninety days require 216 GB and a full year requires 876 GB. The estimated monthly cost of maintaining the one-year archive volume at ₦18 per GB is ₦15,768. SHA-256 hashing, role-based access, immutable storage where available, NTP verification and chain-of-custody records protect evidence integrity.

TOP THREE SECURITY EVENTS

The first priority is E01, where a corporate host attempted a Modbus connection to the OT-SCADA zone from a non-approved source. Modbus traffic into an industrial segment can affect controllers and process operations. Although the firewall denied the request, the source host, user and initiating process must be identified immediately. Related endpoint, DNS, authentication and network events should be preserved.

The second priority is E05, an outbound HTTPS attempt from an OT workstation to an internet address. Direct OT-to-internet communication is normally inconsistent with strong industrial-network segmentation. The denial prevented the session, but the event may indicate malware, unauthorized software, misconfiguration or an attempted remote service. The workstation should be isolated or placed under enhanced monitoring while the process and destination are investigated.

The third priority is E08, where the jump zone attempted RDP access to a PLC engineering station that was not on the allowlist. A jump host is trusted only when its sessions follow approved accounts, destinations and work orders. The denied event may represent operator error, a stale rule, compromised credentials or misuse of the jump host. The session owner, change ticket and endpoint activity require immediate review.

Two additional events deserve high attention. E03 shows a web-exploit signature against the DMZ, with the session reset by the control. E07 shows a 950 MB upload from the corporate network to an internet destination in eight minutes. The upload may be legitimate, but it also matches a possible data-exfiltration pattern and should be checked against user activity, proxy records and data-loss-prevention alerts.

OPERATIONAL IMPACT AND RISK

The denied OT events show that segmentation controls are functioning, but repeated or unexplained attempts may indicate compromised hosts, incorrect access paths or weak change control. A successful industrial-protocol connection from an unauthorized source could affect availability, safety or physical operations. An OT workstation with unauthorized internet access could introduce malware or expose operational information. Misuse of a jump host could bypass the intended control boundary around engineering systems.

The administrative login outside the maintenance window creates governance risk even if the account is valid. Privileged actions must be traceable to an approved reason. Log loss would increase every risk because investigators would be unable to reconstruct actions, prove policy enforcement or support regulatory and legal review.

RECOMMENDED ACTIONS FOR THE NEXT 7 DAYS

1. Open incident records for E01, E05 and E08 and preserve all related firewall, SIEM, endpoint, VPN, authentication and change-control evidence.
2. Identify the users, devices and processes associated with the three critical events.
3. Verify that the Modbus, OT internet and RDP deny rules remain active and correctly ordered.
4. Review the DMZ server affected by E03 for patches, web logs and indicators of compromise.
5. Validate the business purpose of the 950 MB upload in E07.
6. Confirm the administrator identity and actions for E04.
7. Check NTP status and log-forwarding health across all zones.
8. Generate hashes for current exports and create chain-of-custody records.
9. Test restoration of a representative backup sample.

RECOMMENDED ACTIONS FOR THE NEXT 30 DAYS

1. Implement the proposed hot, warm and cold retention model.
2. Move supported log forwarding to encrypted transport and protect legacy forwarding through the management network.
3. Establish immutable or write-once storage for critical evidence.
4. Review OT allowlists, jump-host destinations and remote-access approvals.
5. Tune SIEM alerts for unauthorized Modbus, OT-to-internet traffic, non-allowlisted engineering access, large outbound transfers and privileged access outside maintenance windows.
6. Perform a quarterly restore test and document recovery time, missing data and hash verification.
7. Review role-based access to the evidence repository and remove unnecessary privileges.
8. Develop dashboards for log-source health, time drift, backup failure, archive capacity and critical OT policy violations.
9. Exercise the legal-hold and secure-disposal procedures.

CONCLUSION

The fictional events demonstrate that firewall prevention must be supported by reliable evidence handling and operational follow-up. The environment successfully denied several dangerous connections, but the attempts still require investigation because they may reveal compromised systems, misuse or incorrect policy. A centralized, encrypted and hash-verified backup process with tested restoration will preserve the visibility required for security operations, incident response, compliance and management decision-making.

# Overall Conclusion

The fictional data shows that the firewall controls denied several dangerous OT-related connections, but the attempts still require investigation and evidence preservation. A centralized, encrypted and hash-verified log-backup programme with tested restoration is necessary to support incident response, compliance and critical-infrastructure operations.

# References

1. NIST SP 800-41 Rev. 1, Guidelines on Firewalls and Firewall Policy.
2. NIST SP 800-82 Rev. 3, Guide to Operational Technology Security.
3. NIST SP 800-92, Guide to Computer Security Log Management.
4. CISA and partner guidance, Best Practices for Event Logging and Threat Detection.
5. RFC 8446, The Transport Layer Security Protocol Version 1.3.
6. RFC 5280, Internet X.509 Public Key Infrastructure Certificate and CRL Profile.
7. RFC 4253, The Secure Shell Transport Layer Protocol.
