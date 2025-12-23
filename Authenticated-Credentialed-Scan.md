# Authenticated (Credentialed) Scan

## Objective

The goal is to use Nessus Essentials to run an authenticated (credentialed) scan on a Windows target.  

## 1. Prepare the Target Systems

**For Windows Targets:**
- Use a local or domain account with **administrative privileges** that is not your daily admin account for security purposes.
- Enable **File and Printer Sharing** (for SMB access on ports 139/445).
	- In the bottom-left search bar search **advanced sharing settings**.
	- Click `Managed advanced sharing settings`.
 	- Choose **Turn on file and printer sharing**.
	- Click **Save changes**.  

<img width="784" height="680" alt="image" src="https://github.com/user-attachments/assets/586d9d6e-8f4a-4693-8043-7059f809b7ad" />

<img width="786" height="620" alt="image" src="https://github.com/user-attachments/assets/75b846d4-990d-443d-af78-d41f3d4ac000" />

- Enable/start the **Remote Registry** service (or allow Nessus to start it).
	- Press the **Win+R** buttons simultaneously on your keyboard to open the **Run** dialog box.
 	- Type in `services.msc`.
	- Click **OK**.
	- Find and right-click **Remote Registry**.
	- Click **Properties**.
	- Set **Startup type** to **Automatic**.
	- Click **OK**.
	- Click **Start** the service.  

<img width="399" height="206" alt="image" src="https://github.com/user-attachments/assets/96535795-8c22-4606-904b-2dafc219509f" />

<img width="945" height="593" alt="image" src="https://github.com/user-attachments/assets/379e5aca-9f0a-4e61-be1a-e0f5db3d719c" />

<img width="408" height="470" alt="image" src="https://github.com/user-attachments/assets/0a7475b5-180c-4cd8-8d42-7aa62002ad76" />

<img width="948" height="593" alt="image" src="https://github.com/user-attachments/assets/c044a8ee-d832-4ff4-89d4-60122b24b3df" />

<img width="948" height="593" alt="image" src="https://github.com/user-attachments/assets/b7deb767-7143-4c50-a478-8d7c32d51ba2" />

- Allow inbound connections on ports 139/445 and others Nessus needs.
	- In the bottom-left search bar search for **Windows Defender Firewall**.
	- Open Windows Defender Firewall.
	- In the left pane click **Advanced settings**.
	- Scroll to and enable these rules (right-click > Enable Rule):
		- File and Printer Sharing (NB-Session-In) to allow TCP 139.
		- File and Printer Sharing (SMB-In) to allow TCP 445.
		- Optionally: File and Printer Sharing (NB-Name-In) and (NB-Datagram-In) to allow NetBIOS (UDP ports 137-138, less critical for Nessus).
		- Windows Management Instrumentation (WMI-In) to allow For WMI access (TCP 135 and dynamic ports).

<img width="784" height="680" alt="image" src="https://github.com/user-attachments/assets/4062143e-5f83-4a5a-bf1d-cd85bf8d6676" />

<img width="793" height="632" alt="image" src="https://github.com/user-attachments/assets/f2524f97-ea6d-4ddd-9764-1c77fc6dcdc5" />

<img width="1047" height="784" alt="image" src="https://github.com/user-attachments/assets/8c8b7fc9-fedb-45c6-abf0-21ada79025a0" />

<img width="1047" height="784" alt="image" src="https://github.com/user-attachments/assets/dcd96844-2f42-430b-8524-10e02d98a336" />

<img width="1097" height="784" alt="image" src="https://github.com/user-attachments/assets/a19da8f4-5844-4ae5-89d0-591b2606fa3c" />

<img width="1097" height="784" alt="image" src="https://github.com/user-attachments/assets/f51cffdb-39eb-4294-b1c9-3cfee8e29d87" />

- Disable or configure **User Account Control (UAC)** restrictions for remote access (e.g., set the registry key `LocalAccountTokenFilterPolicy` to 1 for local accounts).
	- Press **Win + R**, type `regedit`, and press Enter (run as administrator if prompted).
	- Navigate to:
   		`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System`
	- If the key **LocalAccountTokenFilterPolicy** does not exist:
		- Right-click in the right pane > **New** > **DWORD (32-bit) Value**.
		- Name it `LocalAccountTokenFilterPolicy`.
	- Double-click **LocalAccountTokenFilterPolicy**.
	- Set **Value data** to `1` (Base: Hexadecimal).
	- Click **OK**.
	- Close Registry Editor.
	- **Restart your computer**.

<img width="399" height="206" alt="image" src="https://github.com/user-attachments/assets/104562d2-9c67-45d9-9ec0-ab7867465b87" />

<img width="1066" height="617" alt="image" src="https://github.com/user-attachments/assets/92e18c48-ec12-4354-ae58-22a5700b20bf" />

<img width="1063" height="617" alt="image" src="https://github.com/user-attachments/assets/1cf4263e-5483-48cf-b149-b664436289bd" />

<img width="1066" height="617" alt="image" src="https://github.com/user-attachments/assets/80c1b40f-fa9b-42ea-a0b7-39af1266ada0" />

<img width="1063" height="635" alt="image" src="https://github.com/user-attachments/assets/3eff2f46-c977-4911-8ec1-42792293921c" />

<img width="331" height="199" alt="image" src="https://github.com/user-attachments/assets/c70908c2-1f6f-48a6-a9c0-b6a5a1365ec3" />

<img width="1066" height="617" alt="image" src="https://github.com/user-attachments/assets/1f01c42f-bf0b-4d81-b90b-c042197fc45a" />

- Make sure to add the account used for scanning to local groups if needed.
 
## 2. Configure the Scan in Nessus Essentials
1. Log in to your Nessus web interface (usually https://localhost:8834 or the host's IP).
2. Create a new scan: Click **Scans** > **New Scan**.
3. Choose a template: Use **Advanced Scan** or **Basic Network Scan** for flexibility. (For patch audits, select relevant policies if available.)
4. In the scan settings:
   - Enter your target IPs (up to 16 total in Essentials).
   - Go to the **Credentials** tab.
   - Under **Host** category:
     - For Windows: Add **Windows** credentials (username, password, domain if applicable).
   - You can add multiple credential types.
5. Optionally, in **Discovery** or **Assessment**, enable thorough checks.
6. Save and launch the scan.

<img width="1282" height="648" alt="image" src="https://github.com/user-attachments/assets/3c1d10c5-4a69-4175-8bf8-1b7f748cc966" />

<img width="1282" height="646" alt="image" src="https://github.com/user-attachments/assets/0e034a62-8d44-4a52-b6e6-410628d134ce" />

<img width="1282" height="690" alt="image" src="https://github.com/user-attachments/assets/770a10c9-7832-481e-a495-0d3cdf8a4b55" />

<img width="1282" height="646" alt="image" src="https://github.com/user-attachments/assets/530e5f85-ffad-40d5-8807-eb28cd690838" />

<img width="1281" height="685" alt="image" src="https://github.com/user-attachments/assets/b23a304d-ec1c-4c66-884b-6db03cf7dc28" />

## 3. Verify Authentication Success
- After the scan, check results for plugin ID **21745** ("Authentication Failure" or similar) — if it appears, credentials failed.
- Successful credentialed checks will show more detailed vulnerabilities (e.g., missing patches confirmed via registry/filesystem).

### Successful Authentication

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/ccb5ff3e-f486-4457-a7c2-3fa068c4d461" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/ff3cdb74-bd7d-41a0-8b80-47e17e621499" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/61a42c61-26fb-4060-9fe9-56e106d9e49a" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/39653858-4aec-4195-a337-fc81a4ea4633" />

### Failed Authentication

The failed authentication can be filtered by searching for **plugin ID** 21745.  

<img width="1282" height="692" alt="image" src="https://github.com/user-attachments/assets/5763bc8e-f9a0-42cc-9225-b218e00b2bd8" />

<img width="1281" height="689" alt="image" src="https://github.com/user-attachments/assets/de0fd368-1ed3-467c-a472-e92ba71e4648" />

<img width="1282" height="648" alt="image" src="https://github.com/user-attachments/assets/5210c3ed-466b-452c-8101-ae525ab7fe62" />

<img width="1282" height="648" alt="image" src="https://github.com/user-attachments/assets/1b49e79e-2beb-4012-9477-2dab4ef5fd96" />

<img width="1282" height="692" alt="image" src="https://github.com/user-attachments/assets/90bb2a81-0ce6-4012-bf33-85a85fe65b87" />

## What I Learned

I learned how to prepare a target for a credentialed or authenticated scan by
- enabling **File and Printer Sharing** (for SMB access on ports 139/445)
- enabling/starting the **Remote Registry** service (or allow Nessus to start it).
- allowing inbound connections on ports 139/445 and others Nessus needs.
- disabling or configuring **User Account Control (UAC)** restrictions for remote access
- how to configure and verify the credentialed scan in Nessus Essentials
