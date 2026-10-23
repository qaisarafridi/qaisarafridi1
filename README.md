<div align="center">

# 🔴 Muhammad Qaisar Afridi
### ⚡ Ethical Hacker | Penetration Tester | Red Teamer ⚡

[![GitHub followers](https://img.shields.io/github/followers/qaisarafridi?label=Follow&style=for-the-badge&color=dc2626)](https://github.com/qaisarafridi)
[![Repositories](https://img.shields.io/badge/Repos-46-111111?style=for-the-badge&logo=github&logoColor=red)](https://github.com/qaisarafridi?tab=repositories)

---

</div>

## 🛡️ Active Directory Enumeration Cheat Sheet

> **Quick commands & methodology for Internal Penetration Testing & Red Teaming**

<table>
<tr>
<td width="50%" valign="top">

### 1️⃣ Network Enumeration
```bash
# Find live hosts
nmap -sn 192.168.1.0/24

# Detailed port scan
nmap -sC -sV -p- 192.168.1.10

# Scan common AD ports
nmap -p 53,88,135,139,389,445,636,3268,3389 192.168.1.10

# UDP scan (DNS, Kerberos)
nmap -sU -p 53,88,123 192.168.1.10
