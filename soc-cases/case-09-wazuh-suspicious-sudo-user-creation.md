# Case 09 – Linux Privilege Escalation and Docker Activity Investigation

## Executive Summary
A security investigation was conducted on a Linux host (Ubuntu-lab) after privileged activity was observed involving sudo usage, Docker service execution, and container deployment. The activity was performed by a local authorized user but matched multiple MITRE ATT&CK techniques and resulted in operational impact due to disk space exhaustion. No evidence of external compromise or malicious intent was identified.

## Environment
- OS: Ubuntu 24.04.3 LTS
- Hostname: Ubuntu-lab
- User involved: analyst
- Logging source: /var/log/auth.log
- Container engine: Docker
- Security tooling: Wazuh (local components)

## Detection & Trigger
The investigation was initiated after reviewing authentication and system logs showing multiple sudo sessions, service execution as root, Docker container activity, and recurring cron executions. Subsequent system instability caused by full disk utilization prompted deeper log analysis.

## Timeline of Events
- User analyst logged into the Ubuntu-lab host
- sudo systemctl start docker executed
- Docker service started with root privileges
- docker run -it --rm alpine sh executed
- Interactive shell spawned inside Docker container
- Multiple cron jobs executed as root
- Log and queue files increased rapidly
- System disk reached 100 percent utilization
- Operational impact observed (unable to create new directories)

## Log Evidence
Relevant excerpts from /var/log/auth.log:

sudo: analyst : TTY=pts/0 ; PWD=/home/analyst ; USER=root ; COMMAND=/usr/bin/systemctl start docker  
sudo: analyst : TTY=pts/0 ; PWD=/home/analyst ; USER=root ; COMMAND=/usr/bin/docker run -it --rm alpine sh  
pam_unix(cron:session): session opened for user root  
pam_unix(cron:session): session closed for user root  

## MITRE ATT&CK Mapping
- T1548.003 – Abuse Elevation Control Mechanism: Sudo
- T1543.003 – Create or Modify System Process: Service Execution
- T1610 – Deploy Container
- T1059 – Command and Scripting Interpreter
- T1053.003 – Scheduled Task: Cron
- T1499 – Endpoint Denial of Service (Impact)

## Analysis & Verdict
The activity was confirmed to be performed by an authorized local user for administrative and testing purposes. No indicators of compromise, lateral movement, persistence mechanisms, or external access were identified. While the behavior aligned with several ATT&CK techniques, it was determined to be legitimate. However, the actions resulted in unintended operational impact due to uncontrolled disk usage.

## Lessons Learned & Recommendations
- Implement log rotation policies to prevent disk exhaustion
- Monitor disk usage thresholds and trigger alerts proactively
- Restrict Docker execution to approved administrative users
- Create alerts for chained sudo and Docker activity
- Periodically audit cron jobs executed with root privileges


