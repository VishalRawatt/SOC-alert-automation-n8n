
## 1. Project Goal

The goal of this project is to build an automated security monitoring and incident-analysis system using **Splunk as the SIEM** and **n8n as the automation platform**.

The basic workflow is:
```
Windows 10
    │
    │ Security Logs
    ▼
Splunk SIEM
    │
    │ Relevant Events
    ▼
   n8n
    │
    │ Event Analysis
    ▼
ChatGPT / LLM (Ollama used here)
    │
    │ Security Summary
    ▼
  Slack
```

Windows logs will be collected and sent to Splunk for centralized monitoring. Relevant events will then be passed to n8n, where ChatGPT will process and analyze the events. The final analysis will be automatically sent to Slack.

---

## 2. Virtual Machine Configuration

The project environment consists of the following virtual machines:

|Machine|Configuration|Purpose|
|---|---|---|
|Windows 10 Pro|4 CPU / 60 GB|Log generation|
|Kali Linux|4 CPU / 80 GB|Security testing|
|Ubuntu – n8n|4 CPU / 50 GB|Workflow automation|
|Ubuntu – Splunk|6 CPU / 100 GB|SIEM|
|Ubuntu – IRIS|6 CPU / 50 GB|Incident response|

The Splunk server is configured with the IP address:

```
192.168.182.128
```

---

## 3. Initial System Configuration

The initial setup was performed on all virtual machines before starting the main deployment.

### SSH Configuration

SSH was configured on the Splunk and n8n Ubuntu servers to allow remote administration.

### Windows Remote Desktop

Remote Desktop was enabled on the Windows 10 Pro machine for easier remote access.

### Ubuntu Updates

All Ubuntu systems were updated and upgraded:

```
sudo apt update
sudo apt upgrade -y
```

### Windows Snapshot

A snapshot of the Windows 10 Pro machine was created before starting the security-testing phase. This provides a recovery point if any configuration or testing causes unwanted changes.

---

# 4. Splunk Installation

Splunk was selected as the central SIEM for collecting, indexing, and analyzing security logs.

The Splunk `.deb` package was downloaded from the official website and installed using:

```
sudo dpkg -i <splunk-package>.deb
```

After installation, the Splunk directory was accessed:

```
cd /opt/splunk/bin
```

Splunk was configured to run using the dedicated `splunk` user:

```
sudo -u splunk bash
```

The installation directory was then accessed again:

```
cd /opt/splunk/bin
```

---

## 5. Configure Splunk to Start Automatically

To make sure Splunk starts automatically whenever the Ubuntu server boots, boot-start was enabled:

```
sudo ./splunk enable boot-start -user splunk
```

Splunk was then started manually for the initial configuration:

```
./splunk start
```

During the first startup, the license agreement was accepted and the initial administrator credentials were configured.

---

## 6. Accessing Splunk

Once Splunk was running, the Web interface could be accessed from the host machine using port **8000**:

```
http://192.168.182.128:8000
```

The Splunk interface will be used for configuring indexes, receiving Windows logs, searching events, and creating security detections.


![](Screenshots/4.png)

