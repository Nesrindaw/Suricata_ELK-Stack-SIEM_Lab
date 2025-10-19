
This project demonstrates a fully working mini-SIEM lab capable of analyzing network attacks in real time
a strong foundation for SOC, Threat Detection, and Blue Team practical experience.


# Suricata + ELK Stack SIEM Lab

This repository showcases a practical **Security Information and Event Management (SIEM)** setup built using **Suricata**, **Filebeat**, **Elasticsearch**, and **Kibana** inside an Ubuntu-based virtual environment.  
It demonstrates the full detection pipeline from network packet capture to real-time alert visualization.

## Directory Layout
```
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
    ├── 03_kibana_home_ready.png
    ├── 04_tcpdump_running.png
    ├── 05_attack_requests_local.png
    ├── 06_pcap_saved.png
    ├── 07_kibana_suricata_dashboard_alerts.png
    └── 08_kibana_suricata_alerts.png
```

---

##  Architecture Overview
[ Suricata IDS ]  [ Filebeat ]  [ Elasticsearch ]  [ Kibana Dashboards ]

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



## Screenshots

### 01 docker compose up containers running

![01_docker_compose_up_containers_running](https://github.com/user-attachments/assets/47e95e13-8a1b-4040-98c4-86d8ae61e0db)

### 02 all containers running                   
                       
![02_all_containers_running](https://github.com/user-attachments/assets/8c9f21f7-d727-40f9-bdb7-ac2cd113044b)

 ### 03 kibana home ready                      
                       
![03_kibana_home_ready](https://github.com/user-attachments/assets/6ff8e0a6-ba5f-4970-ba8e-c5b5d83c3fed)

### 04 tcpdump running                       
            
![04_tcpdump_running](https://github.com/user-attachments/assets/94b6f416-7945-4092-8873-9735c2c91591)

 ### 05 attack requests local                       
                        
![05_attack_requests_local](https://github.com/user-attachments/assets/3876a978-2e57-4712-aa42-8e0f2cbdb6df)

  ### 06 pcap saved                       

![06_pcap_saved](https://github.com/user-attachments/assets/6fc694a3-a0e7-46e0-9aa9-dc2c49b59e48)

### 07 kibana suricata dashboard alerts                      
                       
![07_kibana_suricata_dashboard_alerts](https://github.com/user-attachments/assets/e44ad1b4-7ed9-4d33-9fdb-69d840212b76)

 ### 08 kibana suricata alerts                   
                     
![08_kibana_suricata_alerts](https://github.com/user-attachments/assets/b8c90860-ee90-483e-9e0b-8abd35ffe59b)

                     



