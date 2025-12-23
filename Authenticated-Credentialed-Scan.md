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

<img width="398" height="206" alt="image" src="https://github.com/user-attachments/assets/5a982084-64bf-4162-b14c-a5de5b360318" />

<img width="949" height="591" alt="image" src="https://github.com/user-attachments/assets/abce7e96-19f9-42d6-80aa-ecddadac6dce" />

<img width="949" height="591" alt="image" src="https://github.com/user-attachments/assets/3f73ae8e-bec9-4ac0-b645-fb05ca69c7a1" />

<img width="949" height="591" alt="image" src="https://github.com/user-attachments/assets/71ad56de-16fd-4413-bcb0-b6603c8e4661" />

<img width="949" height="591" alt="image" src="https://github.com/user-attachments/assets/8db5dae9-861a-494c-80ba-64e9a5023f07" />

- Allow inbound connections on ports 139/445 and others Nessus needs.
	- In the bottom-left search bar search for **Windows Defender Firewall**.
	- Open Windows Defender Firewall.
	- In the left pane click **Advanced settings**.
	- Scroll to and enable these rules (right-click > Enable Rule):
		- File and Printer Sharing (NB-Session-In) to allow TCP 139.
		- File and Printer Sharing (SMB-In) to allow TCP 445.
		- Optionally: File and Printer Sharing (NB-Name-In) and (NB-Datagram-In) to allow NetBIOS (UDP ports 137-138, less critical for Nessus).
		- Windows Management Instrumentation (WMI-In) to allow For WMI access (TCP 135 and dynamic ports).

<img width="785" height="681" alt="image" src="https://github.com/user-attachments/assets/7e58f649-8c3c-4de4-a54a-3e4bf49f5276" />

<img width="1127" height="593" alt="image" src="https://github.com/user-attachments/assets/7ea5c67b-2f6d-4408-a9c9-08b730c7fa1c" />

<img width="1246" height="783" alt="image" src="https://github.com/user-attachments/assets/e691db2d-c1c7-410c-af8d-84540b43b4b3" />

<img width="1246" height="783" alt="image" src="https://github.com/user-attachments/assets/b68fa4ca-d8bd-47cb-aa38-43befa6f8edc" />

<img width="1246" height="783" alt="image" src="https://github.com/user-attachments/assets/5d2d2fc8-6c0f-42b4-b23e-3a34e67782d6" />

<img width="1246" height="783" alt="image" src="https://github.com/user-attachments/assets/c9b9f706-e839-4618-8d2f-d032137fe749" />

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

<img width="401" height="207" alt="image" src="https://github.com/user-attachments/assets/6a6a25f1-116c-45a5-b068-63038e842367" />

<img width="458" height="315" alt="image" src="https://github.com/user-attachments/assets/979f3fe4-cd61-48b3-9859-1cb7a16f413a" />

<img width="1063" height="615" alt="image" src="https://github.com/user-attachments/assets/06688d9f-4118-47dd-a918-72e9e24aaf9d" />

<img width="1063" height="615" alt="image" src="https://github.com/user-attachments/assets/32bea16e-e0ed-4a29-929b-e80112b0f8fb" />

<img width="1063" height="615" alt="image" src="https://github.com/user-attachments/assets/63067723-04cb-40b0-8106-1127e1da786c" />

<img width="1063" height="615" alt="image" src="https://github.com/user-attachments/assets/13ee1a95-6cf9-4e3b-89ec-c03f44efbd9c" />

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

<img width="1283" height="690" alt="image" src="https://github.com/user-attachments/assets/374687bd-6353-4274-90a6-8bb31bedea26" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/d5d58355-28a9-4cba-86a8-65ae66d9ca36" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/f8cb630a-6d43-48c0-b9c7-a38c29c8b265" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/1d36fae7-f29f-4924-a29a-7d19c58112fd" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/59742f18-4774-4d52-8f91-55bdb02c64b4" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/13e273e3-ed7d-408a-bdd4-1381b29542da" />

<img width="1283" height="692" alt="image" src="https://github.com/user-attachments/assets/59a0c08e-b3be-4dd5-bc68-880ca8d51613" />

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
