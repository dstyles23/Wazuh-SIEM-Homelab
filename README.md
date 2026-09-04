# Wazuh SIEM Homelab

## Overview

This project documents the deployment and configuration of a Wazuh Security Information and Event Management (SIEM) environment within my personal cybersecurity homelab.

The purpose of this project is to gain hands-on experience with centralized security monitoring, endpoint telemetry collection, Windows event analysis, detection validation, and security event investigation.

Wazuh is hosted on an Ubuntu Server virtual machine running on Microsoft Hyper-V. A Wazuh agent installed on the Windows Server 2022 Hyper-V host collects security telemetry for analysis within the Wazuh environment.

---

## Lab Architecture

### Physical Host

| Component | Configuration |
|---|---|
| Host | N10 Homelab Server |
| Operating System | Windows Server 2022 |
| Hypervisor | Microsoft Hyper-V |
| Processor | Intel Core i5-12600K |
| Memory | 32 GB DDR4 |

### Wazuh Server

| Component | Configuration |
|---|---|
| Virtual Machine | N10-WAZUH |
| Operating System | Ubuntu Server |
| Allocated Memory | 8 GB |
| SIEM Platform | Wazuh |
| Virtualization Platform | Microsoft Hyper-V |

### Monitored Endpoint

The Windows Server 2022 physical host is enrolled in Wazuh using the Wazuh endpoint agent.

The agent provides security telemetry from the Windows system for centralized monitoring and analysis within the Wazuh SIEM.

---

## Architecture

```text
                 N10 Homelab Server
                 Windows Server 2022
                         |
                         |
                    Wazuh Agent
                         |
                         |
                Security Telemetry
                         |
                         v
              +---------------------+
              |    N10-WAZUH VM     |
              |    Ubuntu Server    |
              |                     |
              |   Wazuh Manager     |
              |   Wazuh Indexer     |
              |   Wazuh Dashboard   |
              +----------+----------+
                         |
                         |
                         v
                 Detection & Analysis
```

---

## Wazuh Deployment

The Wazuh SIEM platform was deployed on a dedicated Ubuntu Server virtual machine hosted through Microsoft Hyper-V.

The deployment provides centralized security monitoring capabilities for endpoints within the homelab.

The Wazuh environment includes:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

After deployment, the Wazuh web dashboard was verified to be accessible from the local network.

---

## Endpoint Agent Deployment

The Wazuh agent was installed on the Windows Server 2022 N10 host.

The agent was configured to communicate with the Wazuh Manager running on the N10-WAZUH virtual machine.

After enrollment, the Windows Server endpoint successfully appeared within Wazuh with an active agent status.

This established the endpoint telemetry pipeline between the monitored Windows system and the Wazuh SIEM.

---

# Detection Validation

## Windows Failed Authentication

A controlled failed-authentication test was performed to validate Windows security auditing and the SIEM telemetry pipeline.

A temporary Windows account named:

`WazuhTestUser`

was created specifically for the detection test.

An authentication attempt was then performed using intentionally incorrect credentials.

Windows successfully recorded the activity as:

**Event ID 4625 — An account failed to log on**

The event was verified within the Windows Security Event Log using Windows Event Viewer.

The event was generated to test security-event collection and visibility within Wazuh.

### Detection Flow

```text
Controlled Failed Login
          |
          v
Windows Security Event 4625
          |
          v
Windows Security Event Log
          |
          v
Wazuh Agent
          |
          v
Wazuh Manager
          |
          v
Wazuh Detection
          |
          v
Security Event Investigation
```

---

## Detection Evidence

### Windows Event ID 4625

Windows Event Viewer confirmed that the controlled authentication failure generated Security Event ID 4625.

The event represents a failed account logon and provides information that can be used during authentication-related security investigations.

Evidence collected during the test includes:

- Windows Security Event ID: `4625`
- Event Type: Failed Logon
- Test Account: `WazuhTestUser`
- Log Source: Windows Security Event Log
- Endpoint: Windows Server 2022

Screenshots documenting the detection process will be stored in the repository's `screenshots` directory.

---

## Security Event Investigation

The controlled authentication test demonstrates the basic workflow used when investigating endpoint security activity:

1. Generate controlled security activity.
2. Verify that the endpoint recorded the activity.
3. Confirm that endpoint telemetry is collected by the SIEM.
4. Identify the corresponding security event.
5. Review relevant event attributes.
6. Determine the reason the event occurred.
7. Document the results of the investigation.

This workflow provides a foundation for more advanced detection engineering and incident investigation exercises.

---

# Skills Demonstrated

This project demonstrates hands-on experience with:

- Security Information and Event Management (SIEM)
- Wazuh deployment and administration
- Endpoint security monitoring
- Wazuh agent deployment
- Windows Security Event Logs
- Windows Event Viewer
- Security event analysis
- Authentication monitoring
- Log collection and analysis
- Detection validation
- Security event investigation
- Microsoft Hyper-V
- Virtual machine administration
- Ubuntu Server administration
- Windows Server administration
- Defensive security monitoring

---

# Security Considerations

This repository is publicly accessible. Sensitive information is sanitized before screenshots, configuration examples, or other evidence are uploaded.

Information intentionally excluded or redacted includes:

- Passwords
- API keys
- Authentication tokens
- Private keys
- Wazuh enrollment credentials
- Public IP addresses
- Sensitive usernames
- Personally identifiable information
- Other authentication material

Internal infrastructure information may also be redacted when it is not necessary for demonstrating the technical objective of the project.

---

# Future Improvements

This homelab will continue to be expanded as additional defensive security concepts are implemented.

Planned improvements include:

- Sysmon deployment and integration
- Advanced Windows event monitoring
- Custom Wazuh detection rules
- Detection rule tuning
- False-positive reduction
- Additional Windows endpoint monitoring
- MITRE ATT&CK technique mapping
- Automated high-severity alert notifications
- Additional controlled detection scenarios
- Incident investigation documentation
- Security monitoring dashboards
- Expanded endpoint telemetry collection

---

# Project Status

**Status:** Active / In Development

Current functionality includes:

- Wazuh SIEM deployed
- Wazuh Dashboard accessible
- Windows Server endpoint enrolled
- Wazuh agent reporting as active
- Windows security auditing operational
- Controlled Windows Event ID 4625 generated successfully
- Detection validation testing in progress

Additional detection scenarios and security monitoring capabilities will be added as the homelab develops.

---

# Disclaimer

This project was created for educational and defensive cybersecurity purposes.

All testing is performed within a privately owned homelab environment on systems that I am authorized to administer.

No testing documented in this repository is performed against third-party systems or infrastructure without authorization.
