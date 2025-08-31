# Explore Google hacking and enumeration 

# AIM:

To use Google for gathering information and perform enumeration of targets

## STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various Google hacking keywords and enumeration tools as follows:


### Step 3:
Open terminal and try execute some kali linux commands

## Pen Test Tools Categories:  

| Operator    | Description                        | Example Usage           |
| ----------- | ---------------------------------- | ----------------------- |
| `site:`     | Search within a specific domain    | `site:example.com`      |
| `inurl:`    | Search in URL                      | `inurl:admin`           |
| `intitle:`  | Search in page title               | `intitle:"index of"`    |
| `filetype:` | Search by file type                | `filetype:pdf`          |
| `intext:`   | Search inside page text            | `intext:"confidential"` |
| `link:`     | Pages that link to a specific site | `link:example.com`      |
| `cache:`    | View cached version of a site      | `cache:example.com`     |
| `ext:`      | Same as filetype                   | `ext:xls`               |

 ## Architecture 
 ```
+----------------------+
|   Attacker / Hacker  |
|   (Browser & Google) |
+----------+-----------+
           |
           | Google Dork Queries
           v
+---------------------------+
|       Google Search       |
+---------------------------+
           |
           | Indexed Public Content
           v
+---------------------------+
|   Target Websites / Data  |
| - Leaked files            |
| - Open directories        |
| - Sensitive info          |
+---------------------------+

```

# Output:
site:
<img width="1900" height="1068" alt="Screenshot 2025-08-30 193022" src="https://github.com/user-attachments/assets/a208dc9a-6b0f-433c-8238-6c11695d7c2b" />
inurl:
<img width="1910" height="1073" alt="Screenshot 2025-08-30 193455" src="https://github.com/user-attachments/assets/87e56538-90ea-4fd2-b45e-9a9b3a728c61" />
inurl index of:
<img width="1910" height="1073" alt="Screenshot 2025-08-30 193455" src="https://github.com/user-attachments/assets/3ea97eb3-c9f2-4987-a366-9473bce86074" />
filetype:pdf
<img width="1917" height="1074" alt="Screenshot 2025-08-30 193929" src="https://github.com/user-attachments/assets/cc9c3ae6-e41e-465e-a91b-7a186153591f" />
intext:password:
<img width="1917" height="1074" alt="Screenshot 2025-08-30 193929" src="https://github.com/user-attachments/assets/927ecc75-d8c9-4433-be9b-d2a2438a5733" />
link:
<img width="1917" height="1074" alt="Screenshot 2025-08-30 193929" src="https://github.com/user-attachments/assets/b8250477-3617-475b-8dad-8aa002b6e3a3" />
cache:
<img width="1389" height="1097" alt="image" src="https://github.com/user-attachments/assets/3ed2b212-f4a2-4f70-b925-531332bdf86a" />
ext:
<img width="1906" height="1080" alt="image" src="https://github.com/user-attachments/assets/da2fea90-6b08-404a-8d62-8c82a77e5cdb" />







# DNS Enumeration



## DNS Recon
<img width="1010" height="853" alt="image" src="https://github.com/user-attachments/assets/9c0b1b84-b7c7-4ee1-b355-56c15490f42f" />


| Record Type | Meaning                        | Example Output                   |
| ----------- | ------------------------------ | -------------------------------- |
| A           | Host to IPv4 address           | `example.com -> 93.184.216.34`   |
| AAAA        | Host to IPv6 address           | `example.com -> ::1`             |
| MX          | Mail server info               | `mail.example.com`               |
| NS          | Name servers                   | `ns1.example.com`                |
| TXT         | Misc data (SPF, verifications) | `v=spf1 include:_spf.google.com` |
| CNAME       | Canonical names (aliases)      | `www -> example.com`             |

## Common Tools Used (Kali Linux)

| Tool           | Description                                | Usage Example                           |
| -------------- | ------------------------------------------ | --------------------------------------- |
| `nslookup`     | DNS lookup tool (simple queries)           | `nslookup example.com`                  |
| `dig`          | DNS lookup utility (detailed)              | `dig example.com any`                   |
| `host`         | Simple DNS querying tool                   | `host example.com`                      |
| `dnsenum`      | Perl script to enumerate DNS info          | `dnsenum example.com`                   |
| `fierce`       | DNS scanner to locate non-contiguous IPs   | `fierce -dns example.com`               |
| `dnsrecon`     | Powerful DNS enumeration script            | `dnsrecon -d example.com -a`            |
| `theHarvester` | Subdomain enumeration using search engines | `theHarvester -d example.com -b google` |


## OUTPUT:
nslookup:
<img width="552" height="171" alt="image" src="https://github.com/user-attachments/assets/b0193159-0d35-48a4-a76c-553495dc0102" />
dig:
<img width="695" height="331" alt="image" src="https://github.com/user-attachments/assets/d34b6599-3a66-4ae8-8eb9-78ad898d54f6" />
host:
<img width="596" height="131" alt="image" src="https://github.com/user-attachments/assets/bf7606f2-07bc-4369-a8cb-c70151d81854" />
dnsenum:
<img width="874" height="936" alt="image" src="https://github.com/user-attachments/assets/922121c1-cb05-4519-bad7-552a23cb32e8" />
theHarvester -d:
<img width="617" height="317" alt="image" src="https://github.com/user-attachments/assets/9b0c6a79-3444-43dd-80b4-14bfc2dc9284" />



## Architecture Diagram 
```
+-------------------+        +------------------+       +------------------+
|                   |        |                  |       |                  |
|   Attacker (You)  +------->|   Target Server   +<----->+    DNS Server    |
| Kali Linux / Parrot|       | (Mail / DNS Host) |       |  (Authoritative) |
+---------+---------+        +---------+--------+       +---------+--------+
          |                            ^                          ^
          |                            |                          |
          |                            |                          |
          |           +-----------------------------+            |
          |           |      Information Tools      |            |
          |           |-----------------------------|            |
          |           | smtp-user-enum              |            |
          |           | nmap --script smtp-enum-*   |            |
          |           | dnsenum                     |<-----------+
          |           +-----------------------------+
          |
          v
+-----------------------------+
|   Output/Report             |
|  - Usernames Found          |
|  - MX Records / Zones       |
|  - Subdomains / IPs         |
+-----------------------------+

```

## dnsenum
**Purpose:** A multithreaded Perl script to enumerate information from DNS servers.

**Use case:** Performs DNS zone transfers, brute force subdomains, and gather host IPs.

```
dnsenum example.com
```

## Output:
<img width="1022" height="926" alt="image" src="https://github.com/user-attachments/assets/6aa55852-2b42-42b8-9970-3426424d0e1e" />




## smtp-user-enum
**Purpose:** Standalone tool used to enumerate valid users by using the VRFY, EXPN, or RCPT TO commands.

**Use case:** Brute-forces SMTP to find users.

```
smtp-user-enum -M VRFY -U users.txt -t <target-ip>
```
  
 ## Output
  <img width="810" height="362" alt="image" src="https://github.com/user-attachments/assets/bb732f45-c85a-4ec2-9f64-381c1813c8ad" />



## nmap –script smtp-enum-users.nse <hostname>

**Purpose:** Uses smtp-enum-users NSE script to enumerate valid users on an SMTP server.

**Use case:** Helps identify email accounts on mail servers.

```
nmap -p 25 --script smtp-enum-users.nse <target-ip>
```
## OUTPUT:
<img width="761" height="181" alt="image" src="https://github.com/user-attachments/assets/f224acff-180f-4587-9101-eb73f9a083c8" />



## RESULT:
The Google hacking keywords and enumeration tools were identified and executed successfully
