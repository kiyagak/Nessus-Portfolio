# Nessus Essentials - Basic Network Scan

## Objective

The goal is to use Nessus Essentials to reveal the vulnerability of the local machine that has Nessus Essentials installed on it.

## Run a Basic Network Scan

Within the Nessus Essentials web interface 
- click `New Scan`

<img width="1275" height="160" alt="image" src="https://github.com/user-attachments/assets/4cd24ec9-dac9-4f80-aecd-5e26c0afee8f" />

- Under `Vulnerabilities` select `Basic Network Scan`

<img width="639" height="523" alt="image" src="https://github.com/user-attachments/assets/2ef58523-0297-4f8d-aa51-f3280be40560" />

- In the **Name** field enter `localscan`.
- In the **Target** field enter `127.0.0.1`

<img width="1101" height="701" alt="image" src="https://github.com/user-attachments/assets/59dccdf6-8896-45eb-8829-e01386abdcbe" />

- In the left pane of the **Settings** tab select `Disovery`
- In the **Scan Type** dropdown select `Port scan (all ports)`

<img width="1101" height="700" alt="image" src="https://github.com/user-attachments/assets/a9e933ce-23e5-4538-b7c0-155d560aedbe" />

- In the left pane of the **Settings** tab select `Assessment`
- In the **Scan Type** dropdown leave it as `Default`

<img width="1101" height="701" alt="image" src="https://github.com/user-attachments/assets/e4b39089-873c-4295-a48a-7f9a877a7f10" />

- In the left pane of the **Settings** tab select `Advanced`
- In the **Scan Type** dropdown leave it as `Default`
  - The `Scan low bandwidth links` option is suitable for when the target network is low bandwidth and/or prone to network congestion
- Click the arrow beside the **Save** button.
- Click `Launch`.  

<img width="1092" height="530" alt="image" src="https://github.com/user-attachments/assets/1bef290d-9a3f-448a-aa6a-d5c6ce7c9c25" />

<img width="1279" height="243" alt="image" src="https://github.com/user-attachments/assets/240db540-44f4-413d-8d2a-6942acceab9a" />

## Viewing Scan Results

A previous scan of the local machine, named `VM`, was done on November 20th.  It has the vulnerability scan results. 

<img width="1274" height="616" alt="image" src="https://github.com/user-attachments/assets/f58c9267-fe0d-4d31-ba94-378f68479175" />

- Click the host `127.0.0.1` to view its vulnerability scan results.

<img width="1379" height="685" alt="image" src="https://github.com/user-attachments/assets/29712054-e7f4-4175-b05a-e23a6c4fa46c" />

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

<img width="1269" height="750" alt="image" src="https://github.com/user-attachments/assets/e95eb225-bc88-4f68-b1da-10c7efa0841e" />

The vulnerability scan also found that the `SSL Certificate Cannot Be Trusted`.  

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

