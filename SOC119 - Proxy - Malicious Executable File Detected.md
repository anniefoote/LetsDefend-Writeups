# Writeup: SOC119 - Proxy - Malicious Executable File Detected

## Basic Info
**Category:** Security Analyst\
**Rating:** Medium\
**Type:** Proxy\
**Event ID:** 79

<img width="1579" alt="Screenshot 2023-12-01 at 9 56 26 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/b5384860-8b5d-43b9-9e70-6cb9a3ae4153">

## Playbook

### Collect Data
**Source Address:** 172.16.20.5 (Internal - within company network)
**Destination Address:** 140.82.121.4 (External)
**User Agent:** Penetration Test - Do Not Contain

The source address belongs to the PentestMachine on the company network
<img width="655" alt="Screenshot 2023-12-01 at 10 01 23 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/5573277d-ebbe-4101-b9b3-ce171f325961">

#### Playbook Action: None

### Search Logs
Logs show a request from the pentest machine made to the destination address 140.82.121.4 requesting the github page of bloodhound - an Active Directory reconnaissance tool located at the URL `https://github.com/BloodHoundAD/BloodHound/releases`
<img width="1526" alt="Screenshot 2023-12-01 at 10 02 49 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/9aa376b8-aa1c-4565-8c7c-5e0c5ff38a4b">
The request was sent using HTTPS over port 443 and was allowed.
No other requests were made to the same destination IP from any devices on the network.

#### Playbook Action: None

### Analyse URL
Analysis of the URL in VirusTotal doesn't flag the address as malicious.
<img width="1534" alt="Screenshot 2023-12-01 at 10 17 31 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/26329809-7dae-46b0-be1f-b7908871ec15">
As the URL is within github, a trusted site, it is unlikely that the address itself is malicious however, as github is a site for hosting code repos, it is possible there could be malicious files stored within the repo.
In this case, BloodHound is a tool commonly used by penetration testers during assessments.
#### Playbook Action: Is the URL malicious? No (Non-malicious)

