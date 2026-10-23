<div align="center">

# 💀 Muhammad Qaisar Afridi
### 🛡️ Ethical Hacker | Penetration Tester | Red Teamer | Security Researcher

```text
[+] Target   : Active Directory Infrastructure & Enterprise Networks
[+] Status   : Enumerating & Exploiting
[+] Objective: Securing Systems through Offensive Security
```

<p align="center">
  <a href="https://github.com/qaisarafridi"><img src="https://img.shields.io/github/followers/qaisarafridi?label=Followers&style=for-the-badge&logo=github&color=dc2626&logoColor=white" /></a>
  <a href="https://github.com/qaisarafridi?tab=repositories"><img src="https://img.shields.io/badge/Repositories-46-111111?style=for-the-badge&logo=git&color=161b22&logoColor=dc2626" /></a>
  <a href="#"><img src="https://img.shields.io/badge/Focus-Active_Directory_%26_Red_Teaming-dc2626?style=for-the-badge&logo=hackthebox&logoColor=white" /></a>
</p>

---

</div>

## 👨‍💻 About Me

- 🎯 **Specialization:** Active Directory Penetration Testing, Internal Network VAPT, and Red Team Operations.
- 🔍 **Methodology:** Systematic enumeration, privilege escalation, Kerberos exploitation, and lateral movement.
- 🛠️ **Author of:**
  - **`OSNIT-Tools`** — Curated toolkit for OSINT and reconnaissance.
  - **`-Network-Security-VAPT-Checklist-Methodology`** — Comprehensive checklists for security audits.
  - **`Red-Teaming-`** — Adversary simulation frameworks and notes.
  - **`MY-Nuclei-Templates`** — Custom automated vulnerability scanner templates.

---

## 🛠️ Security Arsenal & Skills

<p align="left">
  <img src="https://img.shields.io/badge/Kali_Linux-557C94?style=for-the-badge&logo=kali-linux&logoColor=white" />
  <img src="https://img.shields.io/badge/Windows_Server-0078D6?style=for-the-badge&logo=windows&logoColor=white" />
  <img src="https://img.shields.io/badge/Active_Directory-FF1616?style=for-the-badge&logo=microsoft&logoColor=white" />
  <img src="https://img.shields.io/badge/BloodHound-E50914?style=for-the-badge&logo=neo4j&logoColor=white" />
  <img src="https://img.shields.io/badge/Nmap-004080?style=for-the-badge&logo=wireshark&logoColor=white" />
  <img src="https://img.shields.io/badge/Burp_Suite-FF6633?style=for-the-badge&logo=portswigger&logoColor=white" />
  <img src="https://img.shields.io/badge/Metasploit-136C9E?style=for-the-badge&logo=metasploit&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white" />
  <img src="https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white" />
</p>

---

# 📑 ACTIVE DIRECTORY ENUMERATION CHEAT SHEET
### *Commands for AD Reconnaissance, Internal Auditing & Penetration Testing*

<table>
<tr>
<td width="50%" valign="top">

### 1️⃣ Network Enumeration
*Find live hosts, open ports, and domain controllers.*

```bash
# Find live hosts
nmap -sn 192.168.1.0/24

# Detailed port scan
nmap -sC -sV -p- 192.168.1.10

# Common AD ports scan
nmap -p 53,88,135,139,389,445,636,3268,3389 192.168.1.10

# UDP scan (DNS, Kerberos)
nmap -sU -p 53,88,123 192.168.1.10
```

---

### 3️⃣ SMB Enumeration
*Enumerate shares, users, and security policies.*

```bash
# List SMB shares (anonymous)
smbclient -L //192.168.1.10 -N

# List SMB shares (with credentials)
smbclient -L //192.168.1.10 -U user%pass

# Enumerate users with enum4linux
enum4linux -a 192.168.1.10

# Using smbmap
smbmap -H 192.168.1.10

# Using crackmapexec
crackmapexec smb 192.168.1.0/24
```

---

### 5️⃣ LDAP Enumeration
*Query AD objects, users, groups, and policies.*

```bash
# Anonymous LDAP query
ldapsearch -x -H ldap://192.168.1.10 \
  -b "DC=domain,DC=local"

# Find domain users
ldapsearch -x -H ldap://192.168.1.10 \
  -b "DC=domain,DC=local" \
  "(objectClass=user)" sAMAccountName

# Dump AD objects with ldapdomaindump
ldapdomaindump -u user -p pass 192.168.1.10

# Extract data using bloodhound-python
bloodhound-python -d domain.local \
  -u user -p pass -c all -ns 192.168.1.10
```

---

### 7️⃣ Domain & Trust Enumeration
*Find domain details, trusts, and forest architecture.*

```bash
# Domain information (net command)
net view /domain

# Query domain with nltest
nltest /dclist:domain.local
nltest /domain_trusts

# Enumerate domain with CrackMapExec
crackmapexec smb 192.168.1.0/24 --domain

# Domain trusts (PowerView)
Get-DomainTrust

# Forest information (PowerView)
Get-Forest | fl
```

</td>
<td width="50%" valign="top">

### 2️⃣ DNS Enumeration
*Get domain information and Active Directory DNS records.*

```bash
# DNS zone transfer (AXFR)
dig axfr domain.local @192.168.1.10

# Query Domain Controllers (SRV records)
dig srv _ldap._tcp.domain.local
dig srv _kerberos._tcp.domain.local

# Enumerate all records with dnsenum
dnsenum --dnsserver 192.168.1.10 domain.local

# Using nslookup interactively
nslookup
> set type=all
> domain.local
```

---

### 4️⃣ User & Group Enumeration
*Find domain users, privileged groups, and account policies.*

```bash
# Using net commands (Windows)
net user /domain
net group /domain

# Using rpcclient (Linux)
rpcclient -U "" 192.168.1.10
> enumdomusers
> enumdomgroups

# Enumerate users with CrackMapExec
crackmapexec smb 192.168.1.0/24 --users

# Using ldapsearch
ldapsearch -x -H ldap://192.168.1.10 \
  -b "DC=domain,DC=local"
```

---

### 6️⃣ Kerberos Enumeration
*Enumerate SPNs, users, and Kerberos tickets.*

```bash
# User enumeration without credentials (Kerbrute)
kerbrute userenum -d domain.local \
  --dc 192.168.1.10 users.txt

# Password spraying (be careful with lockouts!)
kerbrute passwordspray -d domain.local \
  --dc 192.168.1.10 users.txt password

# Get SPNs (GetUserSPNs.py)
GetUserSPNs.py -dc-ip 192.168.1.10 \
  domain.local/user:pass

# View cached Kerberos tickets
klist

# Kerberoasting (Request TGS hash)
GetUserSPNs.py -request -dc-ip 192.168.1.10 \
  domain.local/user:pass
```

---

### 8️⃣ BloodHound Enumeration
*Collect AD relationship data for attack path analysis.*

```bash
# Collect all data via python ingestor
bloodhound-python -d domain.local \
  -u user -p pass -c all -ns 192.168.1.10

# Collect specific data (DCOnly)
bloodhound-python -d domain.local \
  -u user -p pass -c DCOnly -ns 192.168.1.10

# Start BloodHound interface
bloodhound

# Key Cypher Queries to run in GUI:
# - Shortest Path to Domain Admins
# - Find Kerberoastable Users
# - Find AS-REP Roastable Users
# - Find ACL Misconfigurations (GenericAll, WriteDacl)
```

</td>
</tr>
</table>

---

### 🛠️ Useful AD Pentesting Tools Reference

| Tool | Category | Primary Use Case |
| :--- | :--- | :--- |
| **Nmap** | Reconnaissance | Network discovery & Port scanning |
| **Enum4linux** | SMB / RPC | Comprehensive Windows & Samba enumeration |
| **SMBMap** | SMB | Share permissions & file listing |
| **CrackMapExec / NetExec** | Post-Exploitation | Mass network authentication & dumping |
| **LDAPSearch** | LDAP | Raw command-line LDAP querying |
| **Ldapdomaindump** | LDAP | Complete offline Active Directory object dump |
| **Kerbrute** | Kerberos | Fast user enumeration via Kerberos pre-auth |
| **GetUserSPNs.py** | Kerberos | Kerberoasting service account SPN discovery |
| **BloodHound** | Graph Analysis | Mapping attack paths and privilege escalation |
| **PowerView** | PowerShell | Advanced situational awareness on Windows hosts |
| **Rubeus** | Kerberos | Kerberoasting, AS-REP Roasting, Ticket Granting |
| **Impacket Suite** | Protocol Exploitation | SMB, WMI, Kerberos, and DCOM execution |

---

### 🔌 Important Active Directory Ports

| Port | Service | Protocol | Key Red Team Interest |
| :---: | :---: | :---: | :--- |
| **53** | DNS | TCP / UDP | Zone transfers (AXFR), DC identification |
| **88** | Kerberos | TCP / UDP | AS-REP Roasting, Kerberoasting, Ticket forgery |
| **135** | RPC | TCP | Endpoint Mapper, RPC calls, null sessions |
| **139** | NetBIOS | TCP | NetBIOS over TCP/IP, name resolution |
| **389** | LDAP | TCP / UDP | Directory queries, null/anonymous binds |
| **445** | SMB | TCP | PSExec, share enumeration, relay attacks |
| **636** | LDAPS | TCP | Encrypted LDAP over SSL/TLS |
| **3268**| Global Catalog | TCP | Forest-wide Active Directory searches |
| **3389**| RDP | TCP | Remote Desktop GUI sessions |

---

### 💡 Red Team Methodology & Pro Tips

- 🚀 **Start with Network & DNS**: Always begin with passive/active host discovery and identify Domain Controllers via DNS SRV records.
- 🔓 **Check for Null & Anonymous Sessions**: Test for unauthenticated access on SMB (`IPC$`, `SYSVOL`, `NETLOGON`) and LDAP before using credentials.
- 🩸 **Leverage BloodHound Early**: Once you obtain domain credentials, run BloodHound ingestors to discover non-obvious delegation or ACL misconfigurations.
- 📝 **Watch Account Lockout Thresholds**: Always verify domain lockout policies (`net accounts`) before running Kerbrute or password spray attacks.
- 📁 **Document Everything**: Maintain clear command logs and timestamps for every enumeration phase during client engagements.

---

## 📊 GitHub Analytics

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=qaisarafridi&show_icons=true&theme=radical&hide_border=true&title_color=dc2626&icon_color=dc2626" alt="Qaisar's GitHub Stats" width="48%" />
<img src="https://github-readme-streak-stats.herokuapp.com/?user=qaisarafridi&theme=radical&hide_border=true&stroke=dc2626&ring=dc2626&fire=dc2626" alt="Qaisar's GitHub Streak" width="48%" />

</div>

---

<div align="center">

### ⚠️ Legal Disclaimer
*This cheat sheet and documentation are provided strictly for educational purposes and authorized penetration testing engagements. Do not test systems without proper written permission.*

```
"Victorious warriors win first and then go to war, while defeated warriors go to war first and then seek to win."
- Sun Tzu, The Art of War
```

</div>
