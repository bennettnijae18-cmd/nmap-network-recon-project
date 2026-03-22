# nmap-network-recon-project
Network reconnaissance project using Nmap to identify open ports and services.

🧪 Network Reconnaissance Report using Nmap

 🎯 Objective
To identify open ports, services, and potential vulnerabilities using Nmap.

🛠️ Tools Used
- Nmap
- Kali Linux

- ⚙️ Methodology
The following command was used:
nmap -sS -sV -A scanme.nmap.org


🔍 Findings

| Port  | State   | Service    | Version                          | Risk                              |
|-------|---------|------------|----------------------------------|-----------------------------------|
| 22    | Open    | SSH        | OpenSSH 6.6.1 (Ubuntu)           | Brute-force, outdated version     |
| 80    | Open    | HTTP       | Apache 2.4.7 (Ubuntu)            | Web vulnerabilities (XSS, SQLi)   |
| 9929  | Open    | nping-echo | Nping tool service               | Uncommon service, possible misuse |
| 31337 | Open    | tcpwrapped | Unknown                          | Hidden/filtered service           |
| 25    | Filtered| SMTP       | -                                | Protected by firewall filtering   |               |
| 135   | Filtered| MSRPC      | -                                | Protected by firewall filtering   | 
| 139   | Filtered| NetBIOS    | -                                | Protected by firewall filtering   | 
| 445   | Filtered| SMB        | -                                | Protected by firewall filtering   | 

⚠️ Risk Analysis

The scan revealed multiple open ports, which increase the attack surface of the system. 
Port 22 (SSH) is particularly sensitive, as it allows remote access and may be vulnerable to brute-force attacks, especially if weak credentials are used. 
Port 80 (HTTP) exposes a web server, which is a common target for attacks such as cross-site scripting (XSS) and SQL injection. 
Additionally, uncommon services such as nping-echo (9929) and tcpwrapped (31337) may indicate non-standard configurations that could be exploited by attackers.
Filtered ports suggest that a firewall is in place, which is a positive security measure.

🛡️ Recommendations

- Disable or restrict SSH access (use key-based authentication)
- Keep all services updated to the latest versions
- Close unnecessary ports
- Monitor unusual services such as port 9929 and 31337
- Implement firewall rules to restrict access
- Regularly scan the system for vulnerabilities

 📡 Traceroute Analysis

A traceroute was performed to identify the path taken to reach the target system.

| Hop | IP Address        | Description                  |
|-----|------------------|------------------------------|
| 1   | 192.168.1.1      | Local router                 |
| 2   | 192.168.0.1      | ISP internal network         |
| 3-5 | *No response*    | Likely filtered routers      |
| 6   | 69.79.207.38     | ISP (Flow Jamaica network)   |
| 7   | 100.64.6.8       | Carrier-grade NAT            |
| 8   | 45.33.32.156     | Target (scanme.nmap.org)     |

The traceroute shows that the target is 8 hops away from the source. Some intermediate hops did not respond, which is common due to firewall filtering. The network latency appears stable, indicating a reliable connection path.
