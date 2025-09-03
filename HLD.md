# High-Level Design Document
# CyberFort Nexux system

The CyberFort Nexus system is a comprehensive cybersecurity solution designed to protect organizational assets from cyber threats. 
This document outlines the high-level design of the system, including its architecture, components, and functionalities.

## 1. General
### 1.1 Introduction
The system aims to provide enterprise defense, by collecting and analyzing data from various sources, detecting threats, alerting incidents in real-time, and providing a Security Operation Center.
### 1.2 Glossary
- **SoC**: Security Operation Center
- **C&C**: Command and Control
- **NetFlow**: IP Metadata protocol (https://datatracker.ietf.org/doc/html/rfc3954)

## 2. Requirements
### 2.1 Functional Requirements

#### Threats & Network Forensics

Detection engines and analyzable information collection

| ID | Requirement |
|----|-----------|
| FR-TRT-101 | At Soc Analyst analysis center, the Investigation Portal shall display virus alerts |
| FR-TRT-102 | At Soc Analyst analysis center, the Investigation Portal shall display malware alerts |
| FR-TRT-103 | At Soc Analyst analysis center, the Investigation Portal shall display malware C&C alerts |
| FR-TRT-201 | At Soc Analyst analysis center, the Investigation Portal shall provide filters on NetFlow data records |
| FR-TRT-202 | When the NetFlow records are filtered at Soc Analyst analysis center, the Investigation Portal shall query the Forensics Engine for NetFlow data records |
| FR-TRT-301 | The Threat Detection Engine shall detect viruses in incoming files |
| FR-TRT-302 | When a virus in an incoming file is detected, the Threat Detection Engine shall issue a virus alert |
| FR-TRT-303 | When a detection of virus in an incoming file is failed, the Threat Detection Engine shall issue a virus detection error |
| FR-TRT-311 | The Threat Detection Engine shall detect malwares in incoming files |
| FR-TRT-312 | When a malware in an incoming file is detected, the Threat Detection Engine shall issue a malware alert |
| FR-TRT-313 | When a detection of malware in an incoming file is failed, the Threat Detection Engine shall issue a malware detection error |
| FR-TRT-321 | The Threat Detection Engine shall detect suspicious malware outgoing C&C activity on metadata of raw packets |
| FR-TRT-322 | When a malware C&C activity on raw packets metadata is detected, the Threat Detection Engine shall issue a malware C&C alert |
| FR-TRT-323 | When a detection of malware C&C activity on raw packets metadata is failed, the Threat Detection Engine shall issue a malware C&C detection error |
| FR-TRT-331 | The Forensics Engine shall index the gateway traffic as NetFlow records |

#### Dashboard

Aggregate information of alerts and investigations

| ID | Requirement |
|----|-----------|
| FR-DBR-101 | At Soc Analyst dashboard, the Investigation Portal shall display the total of uninvestigated virus, malware, and malware C&C alerts, detected in the past 24 hours frame |
| FR-DBR-102 | At Soc Analyst dashboard, the Investigation Portal shall display the count of automatic investigations initiated in the past 24 hours frame |
| FR-DBR-103 | At Soc Analyst dashboard, the Investigation Portal shall display the total of virus, malware, and malware C&C detection errors issued in the past 24 hours frame |
| FR-DBR-104 | At Soc Analyst dashboard, the Investigation Portal shall display a button to generate a report of uninvestigated virus, malware, and malware C&C alerts, detected in the past week frame |
| FR-DBR-105 | At Soc Analyst dashboard, the Investigation Portal shall display a button to generate a report of automatic investigation initiated in the past week frame |
| FR-DBR-106 | At Soc Analyst dashboard, the Investigation Portal shall display a button to generate a report of virus, malware, and malware C&C detection errors issued in the past week frame |

#### Investigations management

Initiatation and conclusion of cyber investigations

| ID | Requirement |
|----|-----------|
| FR-INV-101 | At Soc Analyst analysis center, the Investigation Portal shall allow initialize an investigation of virus alerts, malware alerts, or malware C&C alerts |
| FR-INV-102 | When an investigation is initiated, the Investigation Portal shall allow to conclude the investigation with a Resolution, Insufficient Evidence, or Other reason. |
| FR-INV-103 | At Soc Analyst analysis center, the Investigation Portal shall display investigations |

#### Automatic investigations

Automatic processing of threat investigations

| ID | Requirement |
|----|-----------|
| FR-AUT-101 | In 60 seconds intervals, the Automatic Cyber Investigator shall incrementally escalate network traffic anomaly to cyber incidents |
| FR-AUT-102 | When a virus alert fulfilling the escalation criteria is detected, the Automatic Cyber Investigator shall escalate to a cyber incident |
| FR-AUT-103 | When a malware fulfilling the escalation criteria is detected, the Automatic Cyber Investigator shall escalate to a cyber incident |
| FR-AUT-104 | When a malware C&C activity fulfilling the escalation criteria is detected, the Automatic Cyber Investigator shall escalate to a cyber incident |
| FR-AUT-201 | When a cyber incident is escalated, the Automatic Cyber Investigator shall initiate an investigation based on the incident |

#### User Management

Authorization and administration of users across all systems

| ID | Requirement |
|----|-----------|
| FR-USR-101 | At Organization Manager management screen, the User Management system shall list registered SoC Analysts |
| FR-USR-102 | At Organization Manager management screen, the User Management system shall list active SoC Analysts |
| FR-USR-102 | At Organization Manager management screen, the User Management system shall list inactive SoC Analysts |
| FR-USR-103 | At Organization Manager management screen, the User Management system shall list logged in SoC Analysts |
| FR-USR-201 | At Organization Manager management screen, the User Management system shall allow to register a SoC Analyst |
| FR-USR-202 | When a SoC Analyst is active, the User Management system shall allow to deactivate a SoC Analyst |
| FR-USR-203 | When a SoC Analyst is inactive, the User Management system shall allow to reactivate a SoC Analyst |
| FR-USR-301 | At SoC Analyst login screen, the User Management system shall authorize the SoC Analyst for the Investigation Portal |
| FR-USR-302 | When a SoC Analyst is authorized for the Investigation Portal above 5 minutes, the User Management system shall unauthorize the SoC Analyst |

#### User Workflow



===== HERE ========================================
Investigation Portal
User Management system
Automatic Cyber Investigator
Threat Detection Engine
Forensics Engine

Compute Orchestrating system
Forensics API
Logging system
Health system
Continuous Integration system


# Nonfunctional requirement

## Configuration
NFR-CFG-101 The Investigation Portal shall support a configurable number of detected in-file viruses to be displayed on the Soc Analyst analysis center
NFR-CFG-102 The Investigation Portal shall support a configurable number of detected in-file malwares to be displayed on the Soc Analyst analysis center
NFR-CFG-103 The Investigation Portal shall support a configurable number of detected malware C&C activities to be displayed on the Soc Analyst analysis center
NFR-CFG-104 The Automatic Cyber Investigator shall support a configurable number of seconds for incremental network traffic anomaly scan interval

## Quota
NFR-QUT-101 The User Management system shall support up to 50 active SoC Analysts
NFR-QUT-102 The Forensics Engine shall support data retention period of 3 months
NFR-QUT-201 For Small organizations, The Forensics Engine shall support up to 1Gbps IP traffic peak
NFR-QUT-202 For Medium organizations, The Forensics Engine shall support up to 5Gbps IP traffic peak
NFR-QUT-203 For XLarge organizations, The Forensics Engine shall support up to 50Gbps IP traffic peak
NFR-QUT-201 For Small organizations, The Threat Detection Engine shall support up to 200 devices endpoints
NFR-QUT-202 For Medium organizations, The Threat Detection Engine shall support up to 1000 devices endpoints
NFR-QUT-203 For XLarge organizations, The Threat Detection Engine shall support up to 10000 devices endpoints

## Availability
NFR-AVA-101 The Investigation Portal shall be available 99.9% of the time
NFR-AVA-102 The Forensics API shall be available 99.9% of the time
NFR-AVA-103 The User Management system shall be available only from inside a private network
NFR-AVA-104 The Investigation portal system shall be available only from inside a private network

## Performance
NFR-PFM-101 The User Management system shall perform SoC Analyst registration, deactivation, and reactivation operations within 5 seconds
NFR-PFM-102 The User Management system shall complete SoC Analyst authorization and redirection, within 5 seconds
NFR-PFM-201 The Investigation Portal shall complete retrieval and rendering of alerts and investigations within 2 seconds
NFR-PFM-201 The Threat Detection Engine shall scan files and emails, each of size up to 5GB

## Scalability
NFR-SCA-101 The Compute Orchestrating system shall orchestrate containerized components
NFR-SCA-102 The Compute Orchestrating system shall be migratable to at least one of AWS, Azure, and GCP cloud providers
NFR-SCA-103 The Compute Orchestrating system shall auto-scale components as pre a predefined policy
NFR-SCA-201 The Compute Orchestrating system shall set up a queue for threats alerts
NFR-SCA-201 The Compute Orchestrating system shall set up a load balancer behind The Forensics API

## Usability
NFR-USA-101 The Investigation portal shall provide a graphical user interface supported by all modern browsers
NFR-USA-102 The User Management system shall provide a graphical user interface supported by all modern browsers
NFR-USA-103 The Logging system shall provide a graphical user interface supported by all modern browsers

# Security
NFR-SEC-101 The Compute Orchestrating system shall host all components within a logical private network
NFR-SEC-102 The User Management system shall apply OAuth 2.0 for authorization tasks
NFR-SEC-103 The User Management system shall apply Two-Factor authentication for authentication tasks.

# Observability
NFR-OBS-101 When a component handles a synchronous message, the component shall log the request and response headers
NFR-OBS-102 When a component handles an asynchronous message, the component shall log the event metadata
NFR-OBS-103 When a component encounters an applicative error without stack trace, component shall log the error message
NFR-OBS-104 When a component encounters an applicative error with stack trace, component shall log the error message with the stack trace
NFR-OBS-105 When a auto-scaling policy is not fulfilled, the Compute Orchestrating system shall log the failure
NFR-OBS-201 The Logging system shall collect logs from all components
NFR-OBS-202 The Logging system shall provide logs querying
NFR-OBS-301 The Health system shall detect components failures of all components
NFR-OBS-302 When a system event fulfilling the health issue criteria is detected, the Health system shall alert the System Maintainer of the event

## Maintainability
NFR-MAN-101 When a new version of source code is integrated, the Continuous Integration system shall detect source code vulnerabilities
NFR-MAN-102 When a new version of source code with unit tests is integrated, the Continuous Integration system shall run the unit tests