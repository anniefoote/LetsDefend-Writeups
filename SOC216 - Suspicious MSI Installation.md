# Writeup: SOC189 - VBScript Suspicious Behaviour Detected

## Basic Info
**Category:** Incident Responder\
**Rating:** Medium\
**Type:** Malware\
**Event ID:** 139
<img width="1399" alt="Screenshot 2023-12-18 at 2 41 48 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/205fa3fe-ac0a-4793-a3f7-6dba442d5e88">

## Playbook

### Determine whether the alert was true positive or false positive
Analysis of the suspicious file in VirusTotal flags the VB script as malicious. 
<img width="1530" alt="Screenshot 2023-12-18 at 2 56 07 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/8ecae16e-93e5-450f-933e-37afc156d9e3">

Connecting to the affected machine shows that the malicious VB script is present in the users downloads folder. 
<img width="785" alt="Screenshot 2023-12-18 at 2 54 50 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/64aa33da-1d50-44cf-a2f1-a7d872ba3450">

VirusTotal analysis determined that the script contacts IP address 103.47.144.80 as the malware C2 address. The logs of the affected device show it is making connections to the same address, indiciating the device may be compromised.
<img width="1136" alt="Screenshot 2023-12-18 at 2 57 13 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/b4f39056-00af-4115-b026-025d0993401e">

Based on this information, the alert appears to tbe a true positive.

#### Playbook Action: Is the alert FP or TP? True Positive

### Incident Type
The alert type is malware. This matches the behaviour of the file and as such the incident type would be malware.

#### Playbook Action: What is the incident type? Malware 

### Malware Type
VirusTotal analysis classifies the malware as a trojan.
<img width="1335" alt="Screenshot 2023-12-18 at 3 10 21 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/5503e40e-b5fb-41d7-9df3-bee12aa6daf9">

Further investigation into the malware shows that it is part of the WSHRat family which is a remote access trojan (RAT). As such the malware should be classified as a RAT.
<img width="1691" alt="Screenshot 2023-12-19 at 10 15 54 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/9b996748-4c47-4bc8-979b-7fd250233880">


#### Playbook Action: What type of malware is used in the attack? Remote Access Trojan (RAT)

### Has the malware been executed
As the logs show the device contacting the malware C2 address and the files are present on the device, it appears that the malware has been executed.

#### Playbook Action: Has the malware been executed? Yes

### Initial Access
The browser logs of the affected device show it has accessed an AWS page hosting the malware which then installed it on the system.
<img width="1133" alt="Screenshot 2023-12-18 at 3 14 38 PM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/cb7a5b83-650f-4c10-8464-79917f86e136">

#### Playbook Action: What is the inital access method used in the attack? Drive by Compromise / Drive by Download

### Determine Scope of Threat

    Identify method of attack and systems used.
    Is threat origin internal or external to the organization?
    Were credentials compromised?
    Is sensitive data at risk?
    Is there brand reputation impact?
#### Playbook Action: -

### Persistence Method
After the malware has been executed on the system, logs show several changes to scheduled system services. This indicated that scheduled tasks / jobs are being used as a persistence method.
<img width="1254" alt="Screenshot 2023-12-19 at 10 19 58 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/52c1bb4f-39ed-4dca-889f-2a3fd8ad65a6">
<img width="1248" alt="Screenshot 2023-12-19 at 10 20 24 AM" src="https://github.com/anniefoote/LetsDefend-Writeups/assets/84354375/0ce906b2-35ec-4c86-87e9-c34c3f2b4bce">

#### Playbook Action: What is the persistence method used in the attack? Scheduled Task / Job

### Privilege Escalation

