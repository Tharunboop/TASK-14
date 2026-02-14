Linux Server Hardening & Secure Configuration (Kali Linux)

🔐 Task 14 – Linux Server Hardening

📖 Overview

This task demonstrates practical implementation of Linux server hardening techniques using Kali Linux.
The objective was to reduce the system’s attack surface, secure authentication mechanisms, enforce least privilege, configure firewall rules, and monitor system logs.

All configurations were implemented and verified through command-line validation and screenshots.

🛠 Environment Details

Operating System: Kali Linux (Rolling)

Virtualization: VirtualBox

Shell: zsh

Firewall: UFW

SSH Server: OpenSSH

Update Mechanism: unattended-upgrades

✅ Step-by-Step Hardening Implementation


1️⃣ User & Account Review

Reviewed system users using:

cat /etc/passwd
awk -F: '$3 >= 1000 {print $1}' /etc/passwd


Verified only valid user account (kali) exists.

Confirmed no unauthorized or unused user accounts.

✔ System complies with least privilege principle.

2️⃣ Sudo Privilege Verification

Checked sudo group membership:

getent group sudo

Result:

Only kali user has sudo privileges.

No unnecessary administrative accounts found.

3️⃣ SSH Hardening
🔒 Disabled Root Login

Edited:

/etc/ssh/sshd_config

Set:

PermitRootLogin no

🔐 Configured Key-Based Authentication

Generated SSH key:

ssh-keygen -t ed25519

Installed public key:

ssh-copy-id kali@localhost


Verified successful login:

ssh kali@localhost


Confirmed:

Accepted publickey authentication

Password authentication disabled

Final SSH configuration:

PermitRootLogin no
PasswordAuthentication no
PubkeyAuthentication yes

4️⃣ System Updates & Patch Management

Updated system packages:

sudo apt update
sudo apt upgrade -y


Installed automatic security updates:

sudo apt install unattended-upgrades -y


Enabled unattended upgrades service.

✔ System now automatically applies security patches.

5️⃣ Firewall Configuration (UFW)

Installed firewall:

sudo apt install ufw -y


Configured default policies:

sudo ufw default deny incoming
sudo ufw default allow outgoing


Allowed SSH:

sudo ufw allow 22/tcp


Enabled firewall:

sudo ufw enable


Verified:

Status: active
Default: deny (incoming)


✔ Only required port (22) allowed.

6️⃣ Disable Unnecessary Services

Reviewed enabled services:

systemctl list-unit-files --type=service --state=enabled


Disabled non-essential services:

snapd.service

ModemManager.service

Verified:

inactive (dead)
disabled


✔ Reduced attack surface.

7️⃣ Secure File Permissions

Secured critical system files:

chmod 640 /etc/shadow
chmod 600 /etc/ssh/sshd_config


Secured SSH directory:

chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/id_ed25519


Verified:

-rw-------


✔ Sensitive files protected.

8️⃣ Log Monitoring & Verification

Reviewed authentication logs:

sudo journalctl -u ssh -n 20
Verified:

Successful SSH login entries

No critical system errors

✔ System logging functioning properly.

| Security Control                 | Status      |
| -------------------------------- | ----------- |
| User Review                      | ✔ Completed |
| Sudo Restriction                 | ✔ Completed |
| Root Login Disabled              | ✔ Completed |
| SSH Key Authentication           | ✔ Completed |
| Password Authentication Disabled | ✔ Completed |
| System Updated                   | ✔ Completed |
| Automatic Updates Enabled        | ✔ Completed |
| Firewall Configured              | ✔ Completed |
| Unnecessary Services Disabled    | ✔ Completed |
| File Permissions Secured         | ✔ Completed |
| Logs Reviewed                    | ✔ Completed |




🎯 Final Outcome

The Kali Linux system has been hardened against common security threats by:

Reducing attack surface

Enforcing least privilege

Securing authentication mechanisms

Applying patch management

Restricting network access

Monitoring system activity

The system now follows industry-recommended Linux hardening practices.

💬 Interview Questions & Answers

❓ What is Server Hardening?

Server hardening is the process of reducing vulnerabilities by securing configurations, disabling unnecessary services, enforcing strong authentication, and applying security patches.

❓ Why Disable Root Login?

Disabling root login prevents direct brute-force attacks against the root account and enforces accountability through sudo usage.

❓ What is Least Privilege?

Least privilege means granting users only the permissions required to perform their tasks — nothing more.

❓ Purpose of Firewall?

A firewall controls incoming and outgoing traffic, allowing only authorized connections and blocking malicious access.

❓ Risks of Unused Services?

🔒 Conclusion

This task successfully demonstrates hands-on Linux server hardening skills, including:

SSH security configuration

Firewall implementation

Patch management

Access control

System auditing

The system is now secured against common attack vectors.
