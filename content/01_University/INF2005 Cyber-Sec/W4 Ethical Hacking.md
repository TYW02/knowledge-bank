---
title: W4 Ethical Hacking
---
# Hacking
- **Malicious** Intent: Causing severe damage to reputation and assets, steal information, exploit weakness
- **Professional** Intent: Finding weaknesses (vulnerabilities) and improving security posture
- Personal, Military or Professional Goals

## Unethical Hacking is against the Law
1. Unauthorised **access** to computer material
2. Unauthorised access with **intent to commit or facilitate** a crime
3. Unauthorised **modification** of computer material

#### Offences (Chapter 50A Part II - Offences)
- Unauthorized access to computer material
- Access with intent to commit or facilitate commission of offence
- Unauthorized modification of computer material
- Unauthorized use or interception of computer service
- Unauthorized obstruction of use of computer
- Unauthorized disclosure of use access code
- Enhanced punishment for offences involving protected computers
- Abetments and attempts punishable as offences

# International Collaborations

## International agreement to foster international cooperation
- Offences against CIA of computer data and systems
- Copyright-related offences
- Computer-related offences
- Content-related offences

> Sets common standards or ways to resolve international cases


# Ethics in Information Security

- Protect society, commonwealth and the infrastructure
- Act **honourably**, honestly, justly, responsibly, and legally
- Provide diligent and **competent service** to principals
- **Advance** and **protect** the profession

# White Hat
- Legally authorised to conduct hacking
- The computer security professional who uses skills to **help**
- Hacking as job to **help secure systems** and **provides insight** into policies and procedures

# Black Hat
- The guy who hacks **illegally** / without authorisation
- The computer security expert who uses skills to steal, damage and destroy
- Hacking for **personal gain** or motive

# Gray Hat
- Sometimes **good** guy, sometimes **bad**
- The skilled hacker whose methods **may cross** legal and ethical boundaries
- May **transfer vulnerability** knowledge to either systems owner or black hat


# Hackers' Language

## Leet Speak

> - Invented for coded communication.
> - Hiding websites, newsgroup
> - To avoid detection by search filters
> - Create stronger passwords

![[Pasted image 20260919225823.png]]

![[Pasted image 20260919230001.png]]


# What is Ethical Hacking
- Process of breaking into systems with professional intent
- It is **Legal** - permission is obtained from the target's owner
- Conforms to accepted professional standards of conduct 
- Techniques used sometimes called **Penetration Testing**


## Type of Pen Testing

### Black Box
- Hackers will attack in "**Stealth**" mode ("Covert")
- In this approach typically the attacker have **minimal** or **no pre-knowledge** of the target system
- Employees may be tested

### White Box
- Tester is aiming to be **thorough** within the permitted scope
- **Detailed info** regarding target is **known**
- Tests all known aspects of a system / network and doesn't try to cover their tracks ("**Overt**")

![[Pasted image 20260919230538.png]]

![[Pasted image 20260919230554.png]]


# Hacking Stages
1. **Reconnaissance** - Information gathering on target
2. **Scanning** - Use information gathered in Stage 1 to examine target's security posture more closely
3. **Enumeration** - Identify user / admin accounts for use, running services etc. when attempting to gain access (Sniffing)
4. **Gaining Access** - Exploit (System, Network, Web) Vulnerabilities and information from Stage 2 & 3 (Lateral Movement / Privilege Escalation)
5. **Keeping or Maintaining Access** - For future exploitation (Backdoor Trojan)
6. **Covering Tracks** - Avoid detection (Cleanup footprints for Ethical Hacking)


# Stage 1 - Reconnaissance

## Objective
Hacking into Company Z to (Steal info, Damage reputation)

## How do you event start ?
- What is the **most publicized** reputable asset ?
- Where is it located ? Is the location found, exact ?
- What technologies are used to host it ?

> [!Note]
> - Gain as **much information** about target before attacking - Profiling
> - Can **determine attack** techniques and tools to use
> - How best to launch attack successfully **without raising alerts** ?

## Find out all you can about target
- Location, neighbours
- Technologies
- People
- Scope - overlaps with next phase
- Collect as much info about targets (Techniques & tools)
- Identification of Targets (Company websites, mail servers, OS, extranets, user info)
- War Driving - look for SSIDs of wireless networks in the vicinity

## Reconnaissance techniques and tools
- Whois databases
- Netcraft
- Shoulder Surfing
- Dumpster Diving
- Social Engineering
- Google Hacking

### Shoulder Surfing

> [!Definition]
> Physical method of gaining private information based on stealth

- Observational attack - **with** or **without** technology support
- Used anywhere - office, airport lounges, hotel lobbies
- Many people are **completely unaware** of being spied upon 
- Information you can gather:
	- **Private email sessions**, classified documents, corporate secrets, user names or passwords
	- Even classified documents over the shoulder of an **unwary** government employee
	- Credit card numbers and passwords over phone


### Dumpster Diving
- Discarded records of important info
- Originated by phone phreaks
	- Precursor to hackers

##### Target
Discarded and damaged copies of important information


### Social Engineering
![[Pasted image 20260919232245.png]]

- Range of malicious activities designed to psychologically manipulate users into making mistakes concerning security
- Can work with or without technology
- It works because it exploits human vulnerabilities
	- Desire to help or tendency to trust
	- Hope for a reward
	- Fear of making a mistake or getting into trouble
	- Fear of getting someone else in trouble

### Google Hacking

#### Main benefits
- Low profile and passive - little or no exposure for attacker
- Ranked google results

- Search to be reasonably precise - specific keywords <= 10
- Use search operators 

#### Google group operators include
- allintitle: Restricts results to those containing all the query terms you specify in the title
- group: Allows you to find specific groups related to a given topic
- related: Allows you to find web pages similar to the specified web pages
- intext: Restricts results to documents containing specified term in the text
- inurl: Restricts results to those containing term in URL
- filetype: Restricts results to those containing file type specified


# Stage 2 Scanning (and Enumeration)

> [!Note]
> **Search** for and locate **weaknesses** for **exploitation**
> - Focus on **specific targets** determined
> - Identification of **port status**, **running services**
> - Identify **vulnerabilities** 
> - Enumeration of **accounts** (user, admin), **operating system**
> - Enumeration of NetBIOS and Windows

![[Pasted image 20260919233909.png]]

- After recon you should have a list of IP addresses which you are authorised to hack
- Then scan ports on each of these IP addresses
- This allows you to identify open ports and the services running on the targets, these could be used for exploits

## Passive vs Active Scanning

- Passive - Gathering info **without** the **target's knowledge**, i.e. no packets are sent to the target systems
- Active - Interacting **directly** with the **target** who may log our IP address and activity (May be illegal if unauthorised)


## Scanning Techniques

- Determining if the **system is alive**
	- Probing sweeps
		- **Ping** sweeps
		- **TCP** and **UDP** sweeps

- Determining which **ports** are open / closed / filtered
	- Basic Port Scanning
	- Advanced Port Scanning

- Detecting **reachable** systems
	- Route Tracing
	- APT - advance worms


## Ping
![[Pasted image 20260919234417.png]]

- Used to determine if a system is "alive"
- A special type of Internet Control Message Protocol (ICMP) packet

### Ping Sweeps
- Pings are good for host discovery
- Manually completing individual pings is time consuming
- Ping sweeps can be completed using tools such as `Zenmap`, `Angry IP Scanner`


## Nmap
- Nmap (Network Mapper) is a free and open-source network scanner 
- Included lots of useful tools, like nc, netcat

## TCP Sweep

> [!Note]
> Sometimes, a more security-conscious site will block **ICMP** at the border router or firewall

- Both **TCP** and **UDP** provides alternative approaches to perform ping sweeps to find if a host is alive on the network
- TCP is connection-oriented protocol that **guarantees packet delivery** in sequence but may be less efficient (slower) than ICMP, a control-oriented (network layer) protocol
- UDP, however, **may be less reliable** than TCP but may be used to **confirm closed port**


## Port Scanning

> [!Definition]
> Identify specific ports and services running on a particular host
> e.g. TCP connect scan, SYN scan

### Advance Scanning Techniques

##### Random Scan
> [!Definition]
> Randomizing the sequence of targets and ports probed as well as scanning intervals may prevent detection.

##### Slow Scan
> [!Definition]
> Some hackers are very patient and can use network scanners that spread out the scan over a long period of time. 
> 
> The scan rate can be, for example, as low as 2 packets per day per target site. Can bypass several IDS: eg. Snort, Bro

##### Fragmentation Scan
> [!Definition]
> In case of TCP the 8 bytes of data (minimum fragment size) are enough to contain the source and destination port numbers. This will force the TCP flags field into the second fragment. May hide scan from some firewall and IDSs.

##### Decoy Scan
> [!Definition]
> Some network scanners include options for **decoys** or spoofed addresses in their attacks. If many decoys are used, determining who the real attackers is, will be nearly impossible

##### Coordinated Scan
> [!Definition]
> Group scanning based on a **strategy** or **plan**


## Trace Route
- List routers and hops between the client and a remote host
- The IP Address and domain name (if there is one) of each router is returned to the client
- May also calculate and display the hop time
- Info may be useful to locate new potential attack vectors
- Popular trace routing tool
	- traceroute
	- tracert


## Enumeration

- Port-based enumeration (in-depth scanning)
	- Determine OS and Services

- Enumeration extracts information about
	- Shared resources (or shares) on the network
	- User account information (rarely, user authentication)

- Enumeration is more intrusive
	- Gathered by queries via active connections to target system

- Enumeration Tools
	- NBTScanner, NBTScan, Net View, Reaper, nmap, netcat


### TCP / IP Stack Fingerprinting
- Send specific TCP packets to the target IP to collect configuration info
- Compare response with nmap database of known OS fingerprints
- OS details displayed if there is match

### Fingerprint Techniques - Banner Grabbing
- Acquire networked system info and port services info

## Scanning for Vulnerabilities
- Locating and identifying known weaknesses in the services and software
- Can be completed using a vulnerability scanner


# Vulnerability Scanning vs Pen Testing

## Pen Testing
> [!Pen Testing]
> Pen testing performs exploitation and proof of concept attacks to show **actual vulnerabilities**


## Vulnerability Scanning
> [!Vulnerability Scanning]
> Vulnerability scanning review systems for **potential security issues**


# Stage 3 - Exploitation / Gain Access
- Know what **exploits** can be run against the **known vulnerabilities**
- Exploit with **suitable technique** and tool
- Ultimate goal is to get **admin access**
- Edge Computing - Side Channel Attacks

## Exploit Tools
"A way to exploit a security flaw to circumvent security controls"

- Different targets = different exploits
- inurl: login.php (Look for unencrypted logins)
- Use Wireshark to sniff
- Password Cracking

![[Pasted image 20260920001613.png]]



# Stage 4 - Post Exploitation (Maintaining Access)
![[Pasted image 20260920001648.png]]

- Creating User Accounts
	- A simple method is to create a **new**, hidden, or less-obvious **user account** with **elevated** privileges
- Modifying Startup Services
	- **Malicious scripts or programs** can be **added** to the **system's startup** process to launch automatically
- Installing Backdoors and RATs
	- Tools like Netcat can be used to set up a **backdoor listener** on the target machine, which the attacker can **connect to later** to execute commands
- Installing Rootkits
	- A rootkit is a type of malware that installs at the **kernel level** of a system, giving the attacker **deep control** and making it difficult to detect.


## Make it Hidden - Explorer
- Explorer -> Computer -> Organize -> Folder and search options
- Folder Options -> View tab -> Don't show hidden...
- Can be applied to files, folders as well as drives

## Make it Hidden - CMD
- attrib +s +a +h  \<folder/filename>
- Change folder attributes to system, archive and hidden
- Can be applied to files and folder


# Stage 5: Covering Tracks (Cleanup)
- After an attacker compromises a machine and completes the attack or creates a back door, he has to **ensure that his presence is removed or remains hidden**
- Similarly, when an ethical hacker completes work, the target machine has to be restored
	- Hiding files, folders and accounts
	- Clean up log files, Trojans
	- Restore target machine - uninstalling apps, deleting temporary accounts

> [!Checklist]
> - Clear History
> - Clear temporary internet files
> - Clear cookies
> - Clear Recent Documents list
> - Password protected
> - Run at Start-up
> - Schedule to run when you want

## Penetration Test Report
- Pentest **Scope and Objectives**
- Record of findings during pentest
- Specific advice on how to **close the vulnerabilities**
- Steps to be followed by clients in **future**
- Delivered **directly to an authorized officer** of the client organization






























































