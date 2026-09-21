
## Project Overview

The goal of this project is to build an automated security monitoring system using **Splunk as the SIEM** and **n8n as the automation platform**.

Windows security logs will be collected and sent to Splunk for centralized monitoring and analysis. Relevant events will then be forwarded to n8n, where an LLM will analyze the logs and generate a concise security summary. The final analysis will be delivered to a **Slack channel** for easy access and notification.

### Project Flow

**Windows Logs → Splunk → n8n → LLM Analysis → Slack**

## Virtual Environment

The project is implemented using multiple virtual machines:

- **Windows 10 Pro** – Generates system and security logs
    
- **Kali Linux** – Used for controlled security testing
    
- **Ubuntu (n8n)** – Handles workflow automation
    
- **Ubuntu (Splunk)** – Acts as the central SIEM
    
- **Ubuntu (IRIS)** – Used for incident response and case management
    

## Initial Setup

The virtual machines were configured with the required resources and connected to the same network. SSH was enabled on the Ubuntu servers, Remote Desktop was enabled on Windows, and all Ubuntu systems were updated before deployment.

A snapshot of the Windows machine was also created to provide a recovery point before security testing.

## Splunk Setup

Splunk was installed on the Ubuntu server using the `.deb` package. After installation, Splunk was configured to run under the dedicated `splunk` user and to start automatically when the system boots.

The Splunk service was started and the initial administrator account was created.

The Splunk Web interface was then made available on port **8000**:

`http://192.168.182.128:8000`

## Planned Workflow

Once the infrastructure is ready, Windows logs will be forwarded to Splunk and relevant security events will be identified.

These events will be passed to n8n, which will automate the analysis process. An LLM will interpret the event, identify potentially suspicious activity, and provide a short explanation and recommended investigation steps.

The result will then be sent automatically to Slack.

The final system will demonstrate how **SIEM, workflow automation, and AI-assisted analysis** can work together to reduce manual log analysis and support a small SOC environment.

