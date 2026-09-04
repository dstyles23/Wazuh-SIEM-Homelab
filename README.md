# Wazuh SIEM Homelab

## Overview

This project documents the deployment and configuration of a Wazuh SIEM environment within my personal cybersecurity homelab.

The purpose of the project is to gain hands-on experience with centralized security monitoring, endpoint telemetry collection, Windows event analysis, detection validation, and security event investigation.

Wazuh is hosted on an Ubuntu Server virtual machine running on Microsoft Hyper-V. A Wazuh agent installed on the Windows Server 2022 Hyper-V host forwards security telemetry to the Wazuh environment for analysis.

---

## Lab Architecture

### Physical Host

| Component | Configuration |
|---|---|
| Host | N10 Homelab Server |
| Operating System | Windows Server 2022 |
| Hypervisor | Microsoft Hyper-V |
| CPU | Intel Core i5-12600K |
| Memory | 32 GB DDR4 |

### Wazuh Server

| Component | Configuration |
|---|---|
| VM | N10-WAZUH |
| Operating System | Ubuntu Server |
| Memory | 8 GB |
| SIEM | Wazuh |
| Virtualization | Microsoft Hyper-V |

### Monitored Endpoint

The Windows Server 2022 physical host is enrolled in Wazuh using the Wazuh endpoint agent.

The agent provides security telemetry that can be centrally analyzed through the Wazuh platform.

---

## Architecture

```text
Windows Server 2022 (N10)
          |
          | Wazuh Agent
          |
          | Security Telemetry
          v
+---------------------------+
|       N10-WAZUH VM        |
|       Ubuntu Server       |
|                           |
|   Wazuh Manager           |
|   Wazuh Indexer           |
|   Wazuh Dashboard         |
+-------------+-------------+
              |
              v
      Detection & Analysis
