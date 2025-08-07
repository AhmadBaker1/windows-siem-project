# Windows Security SIEM with ELK Stack and Winlogbeat

## Project Overview

This project implements a Security Information and Event Management (SIEM) system using the ELK stack (Elasticsearch, Logstash, Kibana) and Winlogbeat to collect, process, and visualize Windows Event Logs in real-time.

The SIEM monitors critical Windows security events such as failed logins, privilege escalations, PowerShell activity, and system logs, providing visibility to detect potential security threats and anomalies.

## Why This Matters

- Provides hands-on experience with widely used cybersecurity tools and logging frameworks.
- Demonstrates real-time log collection, ingestion, and visualization skills.
- Builds foundational expertise for roles in Security Operations Centers (SOC) and cybersecurity monitoring.
- Lays groundwork for further enhancements such as alerting and automated incident response.

### SCREENSHOTS
<img width="1766" height="931" alt="image" src="https://github.com/user-attachments/assets/64c1bedc-32d6-406d-9c29-c68358c1579d" />
<img width="1903" height="938" alt="image" src="https://github.com/user-attachments/assets/efeca4bf-1528-48a5-a7aa-b66a4ac04359" />



## Tools Used

- **Winlogbeat**: Lightweight shipper to collect Windows event logs.
- **Elasticsearch**: Search and analytics engine to index and store logs.
- **Kibana**: Visualization dashboard for exploring and analyzing log data.
- **Logstash** (optional): Pipeline to filter and transform logs before Elasticsearch.
- Windows 10 Host machine as log source.

## Setup Instructions

### 1. Install ELK Stack

- Install Elasticsearch, Kibana, and Logstash (if used) on your machine or VM.
- Ensure Elasticsearch and Kibana are running (`localhost:9200` and `localhost:5601`).

### 2. Install Winlogbeat

- Download Winlogbeat from [Elastic Downloads](https://www.elastic.co/downloads/beats/winlogbeat).
- Extract and place in `C:\Program Files\Winlogbeat`.
- Edit `winlogbeat.yml` to configure the output to Elasticsearch:
  
```yaml
output.elasticsearch:
  hosts: ["http://localhost:9200"]
  username: "elastic"
  password: "<your_password>"
setup.kibana:
  host: "localhost:5601"
winlogbeat.event_logs:
  - name: Application
  - name: Security
  - name: System
  - name: Microsoft-Windows-PowerShell/Operational
  - name: Microsoft-Windows-Sysmon/Operational
```

### 3. Install Winlogbeat as a Service
* Open PowerShell as Administrator.
* Run:
  ```bash
  cd 'C:\Program Files\Winlogbeat'
  .\install-service-winlogbeat.ps1
  Start-Service winlogbeat
  ```

### 4. Load Kibana Dashboards
* Run:
```arduino
.\winlogbeat.exe setup
```
* Open Kibana at **http://localhost:5601** and navigate to dashboards.

### 5. Explore Data
* Verify data ingestion by checking the winlogbeat-* index in Elasticsearch.
* Explore Kibana dashboards such as Winlogbeat Overview and security-related dashboards.

### What You Will See
* Real-time event log data from Windows security, system, and PowerShell logs.
* Visualizations showing failed logins, user activity, and system errors.
* Searchable event data to investigate incidents.
