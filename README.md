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

-Download and install Splunk on the Windows server 2022 VM

-Set credentials:
Username and password

*Once it opens it takes you to the Web UI at: https://192.168.10.2 <br><br>
<img width="1164" height="797" alt="Screenshot 2026-05-04 102605" src="https://github.com/user-attachments/assets/01a6ab9b-1d9c-43d5-bb2d-a399b76e0bc2" /> <br>

***Splunk settings**

- Go to **Settings**
- Click **Forwarding and receiving**
- Click **Configure receiving**
- Click **New Receiving Port**
- Enter: 9997

<img width="1167" height="518" alt="Screenshot 2026-05-04 102851" src="https://github.com/user-attachments/assets/05856607-1f38-491a-a054-bd8e9078fec3" /> <br>
*Then test to see if Splunk is alive and can generate logs by entering “index=_internal” into the search bar in order to start seeing logs.

<img width="1203" height="587" alt="Screenshot 2026-05-04 103042" src="https://github.com/user-attachments/assets/759cac02-5c94-4421-b3ac-50d0755c2c01" /> <br><br>
<img width="1194" height="783" alt="Screenshot 2026-05-04 103427" src="https://github.com/user-attachments/assets/ff0cd849-da30-48f6-bd3a-c47ab974a656" /> <br>

-Splunk has been successfull deployed the Windows server and configured as a central log receiver

# 2) Sending real logs from other machines in the virtual network

Install Splunk universal forwarder on:
-Domain controller
-Windows Machine 1

-I first downloaded Splunk Universal Forwarder on the machine

**Splunk settings**
<img width="564" height="435" alt="Screenshot 2026-05-04 105747" src="https://github.com/user-attachments/assets/823f7837-8a1b-4a7f-af51-5179da7bc4eb" />

-Leave Deployment server blank

Receiving Indexer IP: The splunk server (192.168.10.3) on port 9997


## **Enable Windows Logs**

Make sure that SplunkForwarder service is Running

<img width="898" height="641" alt="Screenshot 2026-05-04 111033" src="https://github.com/user-attachments/assets/3f1f4a69-ae56-4558-8bd0-d9cf883066c5" />


## **Add Windows Event Logs**

Add “inputs.conf”  to this path “C:\Program Files\SplunkUniversalForwarder\etc\system\local\”

Add this config to the file

<img width="527" height="279" alt="Screenshot 2026-05-04 112318" src="https://github.com/user-attachments/assets/3e772cc4-21c2-4f03-8790-5ea34ff0e836" />


## 6. Restart Forwarder

-Open CMD and run these commands to stop and start splunk forwarder 

-net stop splunkforwarder
-net start splunkforwarder

<img width="662" height="325" alt="Screenshot 2026-05-04 112820" src="https://github.com/user-attachments/assets/7b852750-3c8d-4c12-a044-db064dddd522" />


## Check in Splunk

Type this query into the search bar to start seeing logs coming from Windows endpoint (DESKTOP-5CR0NHB)

<img width="1213" height="816" alt="Screenshot 2026-05-04 113429" src="https://github.com/user-attachments/assets/a0e3c280-7eaa-4551-93d3-9b14167a1127" />


## Install SYSMON

Test Sysmon

<img width="949" height="512" alt="Screenshot 2026-05-04 120318" src="https://github.com/user-attachments/assets/86e2882a-b5be-4627-b30f-82fad5fa9719" /><br><br>


-Start and stop splunkforwarder
<img width="662" height="325" alt="Screenshot 2026-05-04 112820" src="https://github.com/user-attachments/assets/24e87662-4d8d-4b27-905a-637f920c00ac" />



-Tigger events like notepad.exe and calc.exe

-Run “index=* Sysmon” in order to see the events that took place


