This section documents my methodology for discovering the attack surface of a target.

-------------------------------------------------
**TOOLS USED:**

_**Spiderfoot:**_ Used it to carryout passive recon and obtain subdomains, contact information, ip addresses, web servers and so on

_**Recon-ng:**_ Used to carry out sundomain enumeration

_**Netcraft:**_ A passive recon tool used to obtain website information (Date website was created, IP address etc)

_**Shodan:**_ Used to identify open ports and potential vulnerability

---------------------------------------------------------

**Methodology**

**_Passive Recon:_** No direct contact with the target

----------------------------------------------------------------------------------------

Firstly, I identified my target. In this documentation, i'll be using **scanme.nmap.org** 

**_Phase 1:_** Passive Reconnaisance with Netcraft

This is to identify the underlying infrastructure, hosting provider, and SSL/TLS history without sending a single packet to the target's network.

_**Process:**_ Navigated to https://sitereport.netcraft.com/ domain to pull the site report

<img width="1365" height="630" alt="Screenshot 2026-02-03 102102" src="https://github.com/user-attachments/assets/c0d2fa9b-70a6-436f-836a-185c920148c5" />
<img width="1364" height="631" alt="Screenshot 2026-02-03 102128" src="https://github.com/user-attachments/assets/6d77f25f-76b0-4780-b1dd-d8f591365865" />
<img width="1365" height="636" alt="Screenshot 2026-02-03 102309" src="https://github.com/user-attachments/assets/358af219-35e7-488d-9a6c-a37c4e69e7ec" />
<img width="1360" height="620" alt="Screenshot 2026-02-03 130423" src="https://github.com/user-attachments/assets/0c9a6e20-ccb9-48d2-8bdf-5ac3dad14bb4" />

**_**Key findings:**_**

Cloud Hosting Provider: _Linode_ - Passive reconnaissance via Netcraft confirmed the target is hosted on Linode, LLC. This narrowed the scope to cloud-based Linux vulnerabilities and indicated that any discovered vulnerabilities would likely be due to user-level misconfigurations rather than provider-level flaws

Web Server: _Apache_ - i fingerprinted the web server to identify the underlying technology stack and potential software-specific vulnerabilities

ipv4: _45.33.32.156_

ipv6: _2600:3c01:0:0:f03c:91ff:fe18:bb2f_

--------------------------------------------------------
_Phase 2:_ After performing footprinting via netcraft i looked up the IP on shodan

This is to identify vulnerability and open ports without directly interacting with the target

_**Process:**_ Navigted to shodan.io and look up the ip, which appeared in my Netcraft findings

<img width="1364" height="648" alt="Screenshot 2026-02-03 102609" src="https://github.com/user-attachments/assets/3c311846-97bb-4ada-9d29-7ce78bab1820" />
<img width="709" height="310" alt="Screenshot 2026-02-03 102620" src="https://github.com/user-attachments/assets/343c1ded-4c7f-4af6-86fd-cf40b8b5c5e7" />


_**Findings:**_

Service identified: _Apache HTTP_

Version: _2.4.7_

OS: _Ubuntu_

Open Ports: _80(HTTP), 22(SSH), 123(NTP), 9929, 31337_

---------------------------------------------------------------

_Phase 3:_ Performing recon with recon-ng 

This is to map the target's extended infrastructure(sub-domains) and identify potential employee emails for social engineering tests

Process: Open my terminal on Kali linux and using recon-ng cmd to perform this enumeration

<img width="1366" height="657" alt="reconng nmap" src="https://github.com/user-attachments/assets/ae9808f4-b0ae-42ef-85de-d42801e1f7d9" />

_**In this aspect, i created a new workspace in order to perform the enumeration**_

<img width="1366" height="657" alt="reconng subdomain enumeration" src="https://github.com/user-attachments/assets/f62ffe09-9d98-4784-a911-fd2273cf6255" />

_**Now, i load a module so that recon-ng will enumerate all the subdomains of my target (scanme.nmap.org)**_

<img width="1366" height="657" alt="reconng enumeartion" src="https://github.com/user-attachments/assets/52cb4ff5-3694-4f11-81a8-664128070ad5" />

_**The enumeration process**_

<img width="1366" height="657" alt="recon ng show hosts" src="https://github.com/user-attachments/assets/ad8bfb55-7817-4c42-9d4f-a9dfef2a4a84" />

_**After the enumeration process i used the "show hosts" cmd so that it'll tabularize all the subdomain findings after enumeration, but it appears it found no hosts. Assuming it did find hosts i'd have used html modules to save the enumeration findings so that it will look much more presentable**_

I have used recon-ng to map the target subdomains and identify potential employee emails for social engineering tests but i got no results, now i'll use another tool and see if i'll get what i want

----------------------------------------------------------------------------

_Phase 4:_ In this phase i'll use spiderfoot which can be used for active and passive recon. But in this case, i dont want to interact directly with the target yet so i'll use the pasive recon feature of spiderfoot

To ensure a comprehensive mapping of the attack surface, I utilized SpiderFoot to automate the collection of intelligence. By running a Passive Scan, I gathered data from various sources without interacting with the target's infrastructure, maintaining a stealthy profile

Process: I used the spiderfoot cmd on my Kali terminal and performed the scan on the Web thereafter

<img width="1366" height="657" alt="Screenshot_2026-02-03_04_41_06" src="https://github.com/user-attachments/assets/bbdf0ee8-8e5d-4765-a21b-afe438cd570c" />

<img width="1366" height="657" alt="Screenshot_2026-02-03_04_43_09" src="https://github.com/user-attachments/assets/46c55849-3529-435d-b89c-8d79717acfb4" />

<img width="1366" height="657" alt="now_now" src="https://github.com/user-attachments/assets/f9932976-ebf0-4871-8e69-6d638582d589" />

**_In this jpeg above, i am able to get the subdomain and their ip addresses which i was unable to obtain while using recon-ng_**


<img width="1366" height="657" alt="web_server" src="https://github.com/user-attachments/assets/1c29fd72-8bea-499a-84a7-300f5196f0bf" />

<img width="1366" height="657" alt="confirmation of linode" src="https://github.com/user-attachments/assets/7e665096-785c-4e28-bbec-1c8f1e12b72a" />

_**Key findings:**_
scanme.nmap.org subdomain 

Confirmation of the webserver Apache HTTP 2.4.7 which was discovered when i used netcraft and shodan

Confimation of the hosting provider (Linode) which i discovered earlier using netcraft











