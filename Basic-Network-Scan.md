# Nessus Essentials - Basic Network Scan

## Objective

The goal is to use Nessus Essentials to reveal the vulnerability of the local machine that has Nessus Essentials installed on it.

## Run a Basic Network Scan

Within the Nessus Essentials web interface 
- click `New Scan`



<img width="1275" height="160" alt="image" src="https://github.com/user-attachments/assets/0b6aecba-b476-4af1-8a7c-6b083f8e0e5c" />

- Under `Vulnerabilities` select `Basic Network Scan`

<img width="639" height="523" alt="image" src="https://github.com/user-attachments/assets/cdc3f59e-4bb4-4830-9f99-eb025b6b7ff2" />

- In the **Name** field enter `localscan`.
- In the **Target** field enter `127.0.0.1`

<img width="1101" height="701" alt="image" src="https://github.com/user-attachments/assets/5269f29c-228d-42e8-922d-cb0b2ea9d2b4" />

- In the left pane of the **Settings** tab select `Disovery`
- In the **Scan Type** dropdown select `Port scan (all ports)`

<img width="1101" height="700" alt="image" src="https://github.com/user-attachments/assets/c3375a17-d0cb-410e-a113-cd65e1709393" />

- In the left pane of the **Settings** tab select `Assessment`
- In the **Scan Type** dropdown leave it as `Default`

<img width="1101" height="701" alt="image" src="https://github.com/user-attachments/assets/24ead76f-5110-4197-8320-e079a0b0b93c" />

- In the left pane of the **Settings** tab select `Advanced`
- In the **Scan Type** dropdown leave it as `Default`
  - The `Scan low bandwidth links` option is suitable for when the target network is low bandwidth and/or prone to network congestion
- Click the arrow beside the **Save** button.
- Click `Launch`.  

<img width="1092" height="530" alt="image" src="https://github.com/user-attachments/assets/dd0e2eb3-2f06-4b10-ad8e-dfcbc3668bbc" />

<img width="1279" height="243" alt="image" src="https://github.com/user-attachments/assets/0726f747-895e-4ec4-bb57-2edd4748458f" />

## Viewing Scan Results

A previous scan of the local machine, named `VM`, was done on November 20th.  It has the vulnerability scan results.  

<img width="1274" height="616" alt="image" src="https://github.com/user-attachments/assets/5b16be3d-787f-498b-b246-122ab2c550a6" />

- Click the host `127.0.0.1` to view its vulnerability scan results.

<img width="1379" height="685" alt="image" src="https://github.com/user-attachments/assets/1eb1894d-63fc-4c82-b040-d325fc61fbce" />

- Click the first vulnerability.  This scan found an `Ruby REXML 3.3.3 < 3.4.2 DoS vulnerability`.  

The Plugin Details lists information, such as the vulnerability severity and vulnerability ID:

```
Severity: High
ID: 265895
Version: 1.2
Type: local
Family: Misc.
Published: September 25, 2025
Modified: September 26, 2025
```

VPR key drivers in Nessus are factors that affect a vulnerabiility's Vulnerability Priority Rating (VPR).  

```
VPR Key Drivers
Threat Recency: No recorded events
Threat Intensity: Very Low
Exploit Code Maturity: Unproven
Age of Vuln: 30 - 60 days
Product Coverage: Low
CVSSV3 Impact Score: 1.4
Threat Sources: No recorded events 
```

Risk information includes the VPR rating, risk factor, and the CVSS scores measuring the vulnerability's severity.  

```
Risk Information
Vulnerability Priority Rating (VPR): 2.2
Exploit Prediction Scoring System (EPSS): 0.0001
Risk Factor: High
CVSS v3.0 Base Score: 7.5
CVSS v3.0 Vector: CVSS:3.0/AV:N/AC:L/PR:N/UI:N/S:U/C:N/I:N/A:H
CVSS v2.0 Base Score: 7.8
CVSS v2.0 Vector: CVSS2#AV:N/AC:L/Au:N/C:N/I:N/A:C
IAVM Severity: II
```

In Nessus, Common Platform Enumeration (CPE) helps document and assess vulnerabilities associated with specific software and hardware products.

```
Vulnerability Information
CPE: cpe:/a:ruby:rexml
Patch Pub Date: September 17, 2024
Vulnerability Pub Date: September 17, 2024
```

Reference information includes the CVE, which uniquely identifies the vulnerability with its own CVE number, which is `CVE-2025-58767`.  

```
Reference Information
IAVB:  2025-B-0155
CVE:  CVE-2025-58767
```

<img width="1269" height="750" alt="image" src="https://github.com/user-attachments/assets/f314d16a-4991-4c2c-a310-044deded1dc3" />

The vulnerability scan also found that the `SSL Certificate Cannot Be Trusted`.  

<img width="1269" height="750" alt="image" src="https://github.com/user-attachments/assets/735178b2-2d04-4a3f-8329-b33ffd32a5d8" />

<img width="1269" height="750" alt="image" src="https://github.com/user-attachments/assets/0338c029-5ca4-49a2-990d-5bb81e790543" />

## What I Learned

I learned
- how to run a Basic Network Scan in Nessus Essentials
- how to specify a target host or network to run a vulnerability scan on
- how to specify how many ports to scan
- how to find a plugin's vulnerability severity and vulnerability ID
- how to find the factors that inluence a vulnerability's priority
- how to find the vulnerability's risk factor and the CVSS scores
- how to find a vulnerability's CVE within Nessus Essentials
- REXML had an outdated version that is vulnerable
- mitigating the REXML DoS vulnerability is fixed by upgrading the REXML version to the patched version of `3.4.2`
- that the SSL certificate belongs to the Nessus Essentials software, is self-signed, and is not trusted

