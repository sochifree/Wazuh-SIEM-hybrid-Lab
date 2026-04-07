#  Wazuh SIEM Hybrid Lab (Cloud-Based SOC Environment)

## Overview
This repository contains a **hybrid cloud-based Security Information and Event Management (SIEM) lab** implemented using **Wazuh Cloud** and **Elastic Cloud**.  
The lab demonstrates real-time threat detection, endpoint monitoring, and alert visualization, replicating a modern Security Operations Center (SOC).

## Architecture

### Components
- **Elastic Cloud:** Centralized log storage and SIEM dashboard.
- **Wazuh Cloud:** Security manager for log analysis and alert generation.
- **Endpoints (Agents):**  
  - Windows host (target system)  
  - Kali Linux VM (attacker + monitoring node)

### Data Flow
1. Agents collect logs from endpoints.
2. Logs are sent to Wazuh Cloud for analysis.
3. Alerts are forwarded to Elastic Cloud.
4. Events visualized on Elastic dashboards.

## Setup Instructions

### 1. Kali Linux Agent
```bash
# Import Wazuh GPG key
curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import
chmod 644 /usr/share/keyrings/wazuh.gpg

# Add Wazuh repository
echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list

# Install Wazuh agent
sudo apt-get update
sudo WAZUH_MANAGER='your-cloud-address' apt-get install wazuh-agent

# Start the agent
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
