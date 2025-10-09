# Nessus-Portfolio
A step-by-step guide to install Nessus Essentials on Kali Linux.  

Here is a step-by-step guide to install Nessus Essentials on Kali Linux:

## Download Nessus:
- Visit the official Tenable Nessus download page.
- Select the Linux Debian-based package (.deb) suitable for your Kali Linux system architecture (usually amd64).
- Download the file to your Kali Linux machine.

<img width="1431" height="914" alt="image" src="https://github.com/user-attachments/assets/9d202049-22a0-4889-b759-aa41a77967e4" />

## Install Nessus:
- Open a terminal in the directory where the .deb file is downloaded.
- Install Nessus on Kali Linux:

		sudo dpkg -i Nessus-10.9.4-debian10_amd64.deb

- Start the Nessus service or daemon:

		sudo systemctl start nessusd.service

- Optionally, enable Nessus to start on boot with:

		sudo systemctl enable nessusd

- Check the status of the service with:

		sudo systemctl status nessusd

- Configure Nessus through the web interface by opening a web browser and going to:
		
		https://localhost:8834/

<img width="1431" height="914" alt="image" src="https://github.com/user-attachments/assets/427d3362-c160-4d6c-9147-fb5a3e871ad5" />

Accept the security warning by clicking "**Advanced**" then "**Accept the Risk and Continue**" (due to self-signed certificates).

<img width="1431" height="914" alt="image" src="https://github.com/user-attachments/assets/b592a7bb-59ab-4253-b382-290d2774d77a" />

## Register and Activate Nessus Essentials
- On the welcome screen, select "Register for Nessus Essentials".
- Enter your name and email address to receive an activation code.
- Copy and save the activation code for future use.
- Create an administrator username and password for Nessus.

## Plugin Download and Setup
- Nessus will begin downloading essential plugins needed for vulnerability scanning.
- Wait until the download and setup process completes. This may take a while.

## Login and Use Nessus
- Once setup is done, log in to Nessus using the admin account you created.
- Nessus Essentials is now ready to use for vulnerability scanning on Kali Linux.

<img width="1431" height="914" alt="image" src="https://github.com/user-attachments/assets/ff2a6cb2-54fe-4932-a643-b97906c6fda8" />
<img width="1431" height="914" alt="image" src="https://github.com/user-attachments/assets/90fe7ff4-078b-4f3b-a063-1a03ef0d8eb4" />

## What I Learned

I learned how to install and access Nessus Essentials on Kali Linux.  Nessus is the most popular vulnerability scanner and is useful for doing a variety of vulnerability scans on networks, systems, and applications.  
