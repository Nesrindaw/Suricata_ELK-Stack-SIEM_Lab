
This project demonstrates a fully working mini-SIEM lab capable of analyzing network attacks in real time —
a strong foundation for SOC, Threat Detection, and Blue Team practical experience.


# Suricata + ELK Stack SIEM Lab

This repository showcases a practical **Security Information and Event Management (SIEM)** setup built using **Suricata**, **Filebeat**, **Elasticsearch**, and **Kibana** inside an Ubuntu-based virtual environment.  
It demonstrates the full detection pipeline from network packet capture to real-time alert visualization.

## Directory Layout

lab-siem/
│
├── docker-compose.yml
├── filebeat.yml
├── suricata.yaml
├── rules/
├── suricata-logs/
├── pcaps/
├── evidence/
└── screenshots/
     ├── 01_docker_compose_up_containers_running.png
     ├── 02_all_containers_running.png
     ├── 03__kibana_home_ready.png
     ├── 04_tcpdump_running.png
     ├── 05_attack_requests_local.png
     ├── 06_pcap_saved.png
     ├── 07_kibana_suricata_dashboard_alerts.png
     └── 08_kibana_suricata_alerts.png

---

##  Architecture Overview
[ Suricata IDS ] → [ Filebeat ] → [ Elasticsearch ] → [ Kibana Dashboards ]

All services run through **Docker Compose** for consistency and portability.

---

## Components

| Component | Description |
|------------|-------------|
| **Suricata** | Network Intrusion Detection System generating alerts in `eve.json`. |
| **Filebeat** | Transfers Suricata logs into Elasticsearch. |
| **Elasticsearch** | Centralized data index and search engine. |
| **Kibana** | Visualization and alert analysis tool. |
| **Tcpdump** | Captures live network traffic for analysis. |

---

## Environment

- **OS:** Ubuntu 22.04 (XFCE)
- **Virtualization:** Oracle VirtualBox
- **Tools:** Docker, Docker Compose, Suricata, Filebeat, ELK Stack

---

## Step-by-Step Deployment

### 1 Start Suricata in IDS Mode
```bash
docker compose up suricata
Suricata initialized in IDS mode:
### 2 Launch Full Stack (ELK + Suricata
docker compose up -d
docker ps --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
### 3 Access Kibana
Visit http://localhost:5601
### 4 Capture Live Traffic
sudo tcpdump -i enp0s3 -w ~/lab-siem/pcaps/attack.pcap
### 5 Generate Simulated Web Traffic
for i in {1..30}; do curl -s http://127.0.0.1:3000 > /dev/null; done
### 6 Stop Capture and Verify PCAP
Display captured packets:  sudo tcpdump -r ~/lab-siem/pcaps/attack.pcap -nn -tttt | head -n 20
### 7 Check Evidence Folder
ls -lh ~/lab-siem/evidence/
### 8 Verify Suricata Alerts in eve.json
grep -n "event_type\":\"alert" ~/lab-siem/suricata-logs/eve.json | tail -n 10
### 9 Explore Kibana Dashboards
Events Overview
Alert Overview

## Results Summary
Captured real network packets using tcpdump
Detected malicious-like HTTP activity using Suricata
Forwarded alerts to Elasticsearch via Filebeat
Visualized them in Kibana dashboards

## Learning Outcomes

Understand end-to-end SIEM workflow.

Integrate Suricata with the ELK stack.

Analyze alerts and visualize attack data.

Create reusable security lab environments.




<img width="1366" height="647" alt="01_docker_compose_up_containers_running" src="https://github.com/user-attachments/assets/92b69832-1750-44db-8cd1-52567b217975" />

<img width="1366" height="383" alt="02_all_containers_running" src="https://github.com/user-attachments/assets/a6572574-7660-438c-affb-6c4165dea464" />

<img width="1366" height="720" alt="03_kibana_home_ready" src="https://github.com/user-attachments/assets/d4f7428f-4b7c-451b-89ff-62da86c2c342" />

<img width="642" height="210" alt="04_tcpdump_running" src="https://github.com/user-attachments/assets/fcd3de6a-d1dd-4f82-bba0-8b68797738dd" />

<img width="576" height="153" alt="05_attack_requests_local" src="https://github.com/user-attachments/assets/6f656988-105a-4aaa-8b75-4c40005cc950" />

<img width="1361" height="422" alt="06_pcap_saved" src="https://github.com/user-attachments/assets/68892129-536e-48f0-9433-7dbb2afaea99" />

<img width="501" height="415" alt="07_kibana_suricata_dashboard_alerts" src="https://github.com/user-attachments/assets/6d04950a-8dad-4778-b316-b8bf7c40c3b2" />

<img width="1021" height="407" alt="08_kibana_suricata_alerts" src="https://github.com/user-attachments/assets/eb1eb4a0-b68c-423e-9196-5bedeb08d9b7" />

