## Overview

I built a home lab SIEM using Splunk to simulate a real-world Security Operations Centre (SOC) environment. The lab collects and analyses logs from Windows endpoints and enhances visibility using Sysmon for advanced telemetry.


## Objectives

- Deploy a working SIEM using Splunk
- Forward logs from endpoints to a central server
- Monitor system and security events
- Enhance detection visibility using Sysmon
- Troubleshoot real-world ingestion and network issues

  
## Lab Components

- **Splunk Server (Windows Server 2022)**
    - IP: 192.168.181.139 (192.168.10.
    - Role: Central SIEM (log ingestion + analysis)
- **Windows Endpoint**
    - IP: 192.168.181.136 (192.168.10.4)
    - Installed Splunk Universal Forwarder
    - Installed Sysmon
- **Domain Controller**
    - IP: 192.168.10.2
    - Role: Source of active directory logs
- **Ubuntu Server**
    - Ubuntu Server
    - Role:  Source of Linux logs

# 1) Network Configuration

- Subnet: 192.168.181.0/24
- All machines should en the same network (Custom VMnet1)
  <img width="745" height="385" alt="Screenshot 2026-05-04 110020" src="https://github.com/user-attachments/assets/98087336-80c7-4eff-8c2c-4e2d03db7bce" />
