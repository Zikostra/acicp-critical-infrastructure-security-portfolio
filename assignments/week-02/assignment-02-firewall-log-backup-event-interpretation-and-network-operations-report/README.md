# ACICP201 Week 2 Assignment 02

## Firewall Log Backup, Event Interpretation and Network Operations Report

**Student:** Praise Nze  
**Registration Number:** C11/26/ACIS/17358  
**Course:** ACICP201 – Network Security Engineering  
**Programme:** Advanced Critical Infrastructure Security  
**Assessment Type:** Individual written assignment  
**Due:** Friday, 14 August 2026, 11:59 PM WAT

## Scope

This assignment uses only the fictional firewall events supplied by ICDFA. It does not require access to a production firewall, SIEM, VPN, OT system or log server.

## Completed Work

- [Full integrated assignment](assignment.md)
- [Task 1 – Firewall log backup plan](task-01-firewall-log-backup-plan.txt)
- [Task 2 – Storage and retention calculations](task-02-log-storage-and-retention-calculations.txt)
- [Task 3 – Event interpretation](task-03-event-interpretation.txt)
- [Task 4 – Evidence handling and chain of custody](task-04-evidence-handling-and-chain-of-custody.txt)
- [Task 5 – Mini network-operations report](task-05-mini-network-operations-report.txt)
- [References](references.txt)
- [Submission checklist](submission-checklist.txt)

## Key Calculation Results

| Requirement | Result |
|---|---:|
| Total uncompressed volume | 6.0 GB/day |
| Compressed volume after 60% reduction | 2.4 GB/day |
| Compressed 90-day retention | 216 GB |
| Compressed 365-day retention | 876 GB |
| Monthly archive cost | ₦15,768 |
| Volume after two quarters of 12% growth | 7.53 GB/day |
| Restore time for 1 TB | 5 hours 50 minutes |

## Highest-Priority Events

| Event | Reason | Severity |
|---|---|---|
| E01 | Non-approved Modbus request from CORP-LAN to OT-SCADA | Critical |
| E05 | Outbound internet attempt from an OT workstation | Critical |
| E08 | Non-allowlisted RDP attempt from jump zone to OT engineering station | Critical |

## Final Submission Filename

`ACICP201_Wk2_Assignment02_Praise_Nze_C11-26-ACIS-17358`

## Privacy and Safety

No real organizational logs, credentials, customer information, operational secrets or production addresses are included.
