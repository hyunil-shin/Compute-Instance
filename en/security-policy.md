## NHN Cloud > Security Policy

NHN Cloud provides information on security products, security policies, and vulnerability information to offer a more secure environment.
To protect customer assets from various new attack techniques and security vulnerabilities, we provide the following security policies to help prepare for security incidents and threats that frequently occur in cloud environments.

## Password Policy
When setting passwords for user accounts (both root and general accounts), if an easily guessable password is set, unauthorized users may gain access to the system by obtaining general account or root privileges through brute-force attacks. This can lead to the exposure of important data stored on the server or the server being exploited as a staging point for hacking, so passwords must be set and managed securely.

### What Is a Secure Password
A secure password consists of a combination of letters, numbers, and special characters with a minimum length of 8 characters. Avoid using predictable passwords such as the following:

- Null passwords
- Consisting only of letters or numbers
- Passwords identical to the user ID
- Four or more consecutive characters or numbers (e.g., 1111, 1234, abcd, etc.)
- Periodically reusing passwords
- Easily guessable passwords such as phone numbers, birthdays, account names, or host names

### Password Policy
NHN Cloud applies the following password policy by default to protect customers' valuable assets and services.

- Combination of three types: letters, numbers, and special characters
- Minimum of 8 characters

## DRDoS Attack Blocking Policy
If an instance exposed to an external network is exploited as a DRDoS attack relay point, an abnormal increase in outbound traffic may cause service failures and unintended traffic charges.
NHN Cloud applies a blocking policy for UDP ports that are frequently exploited as DRDoS attack relay points to protect customers' valuable assets and services.

### What Is DRDoS (Distributed Reflect DoS)?
DRDoS occurs due to vulnerable configurations of applications such as DNS, NTP, SSDP, and Memcached. It is a bandwidth-consuming attack technique that is widely used in recent hacking attacks because it can concentrate traffic on a target server by generating large response packets from small request packets using numerous zombie PCs.

### Blocked Port List
| Service Name | Blocked Port | Blocking Method | Note |
| ---- | ---- | ---- | ---- |
| Chargen | UDP / 19 | Network ACL blocking applied | Inaccessible from outside |
| SSDP | UDP / 1900 | Network ACL blocking applied | Inaccessible from outside |
| Memcached | UDP / 11211 | Network ACL blocking applied | Inaccessible from outside |

## Internet Port Blocking Policy (Inbound)
To protect customer services, in addition to the Security Group feature that customers can manage directly, important service ports are blocked using an intrusion prevention system.

### NHN Cloud Blocked Port List
| Applied Region | Service Name | Blocked Port | Blocking Method | Note |
| ---- | ---- | ---- | ---- | ---- |
| Korea (Pangyo/Pyeongchon/Gwangju) <br> Japan (Tokyo) | System Terminal Port | TCP/23 | Network ACL blocking applied | Inaccessible from outside |

### NHN Cloud (for Public Institutions) Blocked Port List
| Service Name | Blocked Port | Blocking Method | Note |
| ---- | ---- | ---- | ---- |
| System Terminal Port | TCP/22, 23, 3389 | Network ACL blocking applied | Inaccessible from outside |
| DBMS Port | TCP, UDP/1433(MS-SQL), 1521(Oracle), 3306(MySQL) | Network ACL blocking applied | Inaccessible from outside |
| Netbios-related Port | TCP, UDP/135, 137, 138, 139, 445 | Network ACL blocking applied | Inaccessible from outside |
| Others | TCP/21(FTP), TCP / 5900(VNC) | Network ACL blocking applied | Inaccessible from outside |

### Procedure for Requesting Port Addition/Allowance
- Download and fill out the Excel file below.

[![](images/fileicon_download_excel.png)](https://static.toastoven.net/prod_gov_security/NHN%20Cloud%20%EB%B0%A9%ED%99%94%EB%B2%BD%20%EB%B0%8F%20SSL%20VPN%20%EC%A0%95%EC%B1%85%20%EC%8B%A0%EC%B2%AD%EC%84%9C.xlsx)

- Save the file as "NHN Cloud Firewall and SSL VPN Policy Request Form-Organization Name.xlsx".
- Submit the file by attaching it to NHN Cloud [1:1 Inquiry](https://www.nhncloud.com/kr/support/inquiry?alias=tab3_08). (Processed and responded to within 3 days from the date of receipt)