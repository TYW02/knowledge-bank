### Malware 

* Written for OS   
* Needs detailed knowledge of operations, procedures and Setup of System 

**Potential Impact** 

* **Data** \[change data in file\]   
* **Hardware** \[NOT directly, Can mess up critical software for hardware\].   
* **Time** \[Make System unusable until malware is eliminated\]   
* **Reputation** \[ Reputation can have massive impact on your business\] 

### Malware Type 

* Virus   
* Worm   
* Trojan 

### Virus 
- Malicious executable  
- Does NOT auto-replicate  
- Attaches to a "host' (program or file)  
- Insert marker to prevent re-infection  
- Will replicate when it attaches to a new host  

Mutating virus (metamorphic): Encrypt main malicious body & wrap with changing decryption key  
Encrypted virus (Polymorphic): Every new generation looks structurally unique virus 

### Anatomy  
**Concealment**: Hide itself from things like antivirus software  
**Propagation**: Find file and infect them, add markers to files which are infected  
**Payload**: Any code not related to concealment or propagation, another malware that does damage to infected System



### **Virus Triggers** 

**Logic bomb:** payload execution triggered by event 

**Time bomb:** triggered by date/time 

### **Worm** 

* **Don't need** user interaction to **spread**   
* **Don't need** "'host' document **to attach to**   
* **Auto-replicate** / **propagate** via **network** & **end point vulnerabilities**   
* Worm is **carrier**, may **carry payload** 

**How it moves** 

* Window admin share (net share)   
* Unix remote shell script (rsh)   
* Bugs in networking software   
* Password cracking 

### **Trojan** 

* **Hidden** inside **innocuous program** (may use **rootkit to hide**)   
* **Doesn't self replicate**   
* Include **backdoor** (often for command & control).   
* May include key logger, webcam control 

### **Keylogger** 

* Log all your keystroke   
* Username & password   
* Private information 

### **Malware Infection Vectors** 

* Attachment to ***e*****\-mail**   
* **Download** from Internet   
* Exploiting **vulnerabilities** in existing app   
* Exploit vulnerabilities in OS   
* Running Software on removable media   
* Social engineering 

### **Signs of Infection** 

* Program slowing down or taking longer to start   
* Sudden drop in available memory   
* Changing program length   
* Very old file recently modified   
* Computer restart for no reason   
* Unusually heavy network traffic   
* key typed does not match key displayed 

### **Attack on Computer System** 

* Hardware   
* Software  
* Hypervisor  
* OS Kernel  
* System Software 

### **System Layers**

* Application  
* System Software   
* Hardware

### **Hardware attack** 

* **Counterfeit attack**: Distribution of malicious hardware that compromised security of device (Dropping USB to capture keyboard strokes)  
* **Fault injection attack**: Alter device operation by physically tampering with hardware component (Inject voltage glitch to change CPU instructions)  
* **Micro-architectural attack**: Target implementation of system's microarchitecture (Speculative attack to read arbitrary memory or exploit DRAM for privilege escalation)

### **Software attack** 

* **Control flow attack**: Divert intended control flow of program to execute malicious Code   
* **Code Injection attack**: Input is passed to program which generates executable code to be executed by another program (executor)   
* **Command Injection attack**: Send input to modify command passed to command interpreter to execute command injected by attacker 

### **Hypervisor** 

* Baremetal Hypervisor (Type-1) Safer & faster Since its closer to hardware   
* Hosted Hypervisor (Type-2) Less Secure, if host is compromised, ALL OS vulnerable  
* OS-level OS-Level Hypervisor (container) 

### **Hypervisor Attack** 

* **Hyperjacking**: Replace hypervisor with malicious hypervisor by injecting below / above or totally replace legitimate hypervisor \[Hard to detect malicious hypervisor\]   
* **VM escape**: Allow interaction between VM & host by breaking isolation provided by hypervisor   
* **VM rootkit attack**: Installs rootkit running underneath OS \[special case of hyperjacking\] 

### **OS Attack** 

*  **Loadable kernel module attack**: uses loadable kernel module to inject malicious code into os \[Kernel module have almost unlimited access to program on monolithic kernel\] 

* **Kernel Rootkit**: Install rootkit within OS with or without privilege escalation attack \[ Hard to detect, complete re-install usually required\] 

* **Kernel privilege escalation**: Gain access to resource normally protected from user because OS kernel require higher privileges \[ Jailbreaking \]   
* **Horizontal Privilege escalation**: Gain access to another account at same privilege level   
* **Vertical escalation**: Attacker increase privilege of compromised account to gain higher level access \[ Dangerous as may grant attackers Complete control over System\] 

### **System Software attack** 

* **Dynamic Linking**: Manipulate dynamic linker to link malicious libraries for program startup time   
* **Package management**: Modify package manager to accept malicious software package   
* **Ransomware:** Permanently block access to victim's data 

### **Network architecture** 

* Client-Server   
* Peer-to-Peer 

**Vulnerability \+ threat \= Risk** 

* Vulnerability \= Weakness in system  
* Threat \= Act which has potential to damage system  
* Risk \= Probability of loss due to cyber attack

**Network Vulnerabilities**

* Router  
* Switch   
* End device   
* Wireless Access Point 

**Network Based Attack**

* **DoS & DDoS** \= Open service for TCP, UDP port  
* **MitM** \= unsecured physical Port   
* **Packet Sniffing** \= unencrypted packet that contain Credentials   
* **Port Scanning** \= Unfiltered service for TCP, UDP port   
* **ARP Spoofing** \= Unsecured physical port connected to attacker 

### **DOS** 

* **Bandwidth Flood**: Overwhelm bandwidth of target \[If Service take 100MB, flood with 150MB\]   
* **Service Request Flood**: Disrupt service by sending request, Request don't need to Succeeded, just use up resources.   
* **Distributed reflective Dos (DRDOS)**: Take down availability of assets through overwhelming responses. Send request without establish connection State   
* **Bots(Reflector)**: Send modified Source address and unsolicited traffic to victim controlled by Command & Control \[ Type of malware that allow attacker to control computer\]   
* **Zombie**: Internet connected computer infected with bot   
* **Botnet**: Collection of Zombie used to perform DDoS   
* **IoT Botnet**: IOT used as zombie 

### **MitM** 

**Access Point** 

* Wardriving: Driving around to locate APS   
* Evil twin: Fake WiFi AP to attract victim to connect   
* Access Point Hijacking Attacker jam victim's channel, victim reconnects to evil twin instead 

### **Network Sniffing** 

**Passive Sniffing**: 

* Use sniffer to monitor network packets   
* Relies on promiscuous mode of network interface controller   
* Difficult to detect, DOES NOT work well in Switched network 

**Active Sniffing**: 

* Required to bypass the segmentation of Switch   
* Inject packet to switch to cause traffic for other nodes to redirect to \[ Sends out multiple network probes to identify APS\] 

| Spoofing | Poisoning |
| :---- | :---- |
| Pretend to be someone else | Send wrong information to victim or network device |

* **Port Spoofing**: Sending SSH to port 443 instead   
* **Deep Packet Inspection**: Identify Spoofed traffic as SSH and forward to security tool for analysis packet filtering filter packet with payload that normal filtering cannot detect   
* **Address Resolution Protocol (ARP):**   
  * Translate IP to MAC address   
  * Each host maintain a table (ARP cache) of IP to MAC address 

**ARP Spoofing (ARP Poisoning)**: 

* Instead of waiting for reply to finish, attacker Sends reply with their own MAC address \[ARP cache entries NOT long-lived\] 

**Port Scanning**: Check host's port to see which are open, closed or filtered and listens to data arriving at and leaving a port.

**TCP Connect Scan**: Attempt to connect to all I/O Ports   
**Port Scan**: Focused scan on Specific Ports 

**Network Defense in-depth**: Layered defence, delay attack's progress rather than stop it 

* **1st level**: Control access to/from unauthorized network will allow / block traffic based on Security rules   
* **2nd level**: System detect against network activity, typically signature-based   
* **3rd level**: VPN provide encryption over Public IP network 

### **Firewall** 

* Hardware or Software   
* Monitor & filter network traffic  
*  Combination of Security mechanisms   
* Support VPN 

### **What does it mitigate** 

* Port Scanning \[Lockdown access to Port\]   
* Wardriving \[only allow request from Specified IP\]  
* Limited help with Dos \[stop request from unwanted source but not against complex\]  
* Cannot help bypass attack 

### **Firewall Policies & Rule set** 

Define Policy \-\> Inside Policy have rules 

(Bad Policy only look for request from Port 80 but HTTP can come from port 1024-65535)

### **Packet Filtering** 

* Test each packet that cross firewall to user-defined rules   
* Security rule block based on port, IP address, IP protocol 

**Stateless Packet filter**: Does NOT look at State of connection. Just packets 

**Stateful Packet filter**: Aware of connections that pass through it. Adds & maintains information about user's connection in state table. 

### **Network Security** 

**Intrusion Detection System (IDS)** 

**Network Intrusion Detection System** 

* Detect attack without traffic flow over it   
* Can be connected to hub in promiscuous mode or switch via port mirroring   
* Can be extended via Host IDSCHIDS) or agent for larger attack detection scope   
* Support DPI   
* Use Signature-based / Statistical anomaly detection with higher accuracy 

**Intrusion Protection System (IPS)** 

* Same as IDS \+ automated response to block intrusion.   
* Usually located inline between firewall & protected network, requires greater logging capacity

### **Network Proxy** 

* Redirect web request at application layer (No direct connection with external Server)   
* Offer deep packet inspection   
* Examines data for content that is not allowed   
* Provide private or anonymous Internet access 

### **Application proxy** 

* Extensive logging (Ability to examine content of whole packet)   
* Cache frequently accessed web page to reduce network traffic   
* Not Suited for real-time, high-bandwidth application 

### **VPN** 

Extend private network across a public one, attacker cannot read your data 

* **Authentication**: User must be authenticated before Secure tunnel is established   
* **Tunneling**: Encapsulate 1 type of protocol and maintain tunnel management protocol **Encryption**: Protect data traveling through tunnel 

**Layer 2 Tunnelling protocol**: Tunnelling with IPsec 

### **Switch Port Security** 

* **MAC flooding attack**: Make MAC address table full of fake Source MAC So authentic not found   
* **Port Security**: Restrict input to switch interface by limiting MAC address of host that are allowed to access interface   
* **Shutdown mode**: Port will move to error disabled state if violation detection 

### **AAA** 

* **Authentication**: who are you?   
* **Authorization**: what can you do   
* **Accounting**: when do you do? 

**Remote Authentication Dial In User Service (RADIUS):**   
NAS, Client/Supplicant, Radius server   
**Terminal Access Controller Access Control System (TACACS)**: Protocol between authentication Server to determine User Permission to access network 

# **Digital Forensics**

**Forensics**: Applying science to legal problems and investigation  
**Digital Forensics**: Branch of forensics involving the **recovery and investigation** of **digital evidence**   
**Digital Evidence**: Data stored or transmitted using a digital device

* Computer Forensics  
* Storage Forensics  
* Network Forensics  
* Mobile Forensics

### **Evidence Integrity**

Maintain the integrity of the data.  
**Purpose**: Demonstrate that the evidence collected **IS** the evidence analysed and presented (Has not been tempered with)  
**Use**: Hash functions (MD5, SHA1/2, SHA-256)  
Hash the evidence first to ensure that the evidence has not been tampered with

### **Process Models**

* **Acquisition** of evidence in lawful manner  
* **Identification** aims to identify and collect the digital data that can be used as evidence  
* **Evaluation** of data relevant to the case, and whether it can be used in a case  
* **Admissions** of the evidence to be presented in the court of law

**Preservation of Evidence:** There is no one standard process model for digital forensics investigations

### **Operating System Forensics**

What kind of information can you get ?

* File download  
* Program Execution  
* File opening / creation  
* Deleted files  
* Physical device location  
* USB or drive storage  
* Account usage   
* Network usage

* Forensics examination needs to investigate the **actions of a user** (real / bot)  
* **Every event** is the result of a user either **doing something** or **NOT doing something**  
* Many **events** introduce **changes to the system** state that are **supervised by the OS**  
* Forensics helps to understand **how system changes** *correlate* to **events** resulting from the actions of users

### **OS-based Evidence**

| Linux                                                                        | Windows                                    |
| :--------------------------------------------------------------------------- | :----------------------------------------- |
| Configuration Files /etc/passwd /etc/sudoers /etc/inittab /var/spool/cron/\* | Dedicated Data Structures Windows Registry |
| Log files /var/log/boot.log /var/log/auth.log                                | System Logging Service Windows Event Log   |
|                                                                              | Special Files                              |


### **Windows OS Forensics**

* Windows Registry  
* Event Logs  
* Link files  
* Recycle Bin  
* Application Metadata (MS Office)  
  * List of last 10 authors  
  * List of revision, along with who made them (If “Track changes” is on)  
  * Hidden annotations and comments  
  * Created, last written, and accessed times  
* Browser History and Cache  
* Prefetch Files: Stored in C:\\Windows\\Prefetch\\\*.p

### **Windows OS Forensics: Registry**

A lot of information can be recovered in the **Windows Registry**

* Registry can be seen as **unified file system**  
* Registry’s specific structure is divided into **key and value**  
* Main root keys represent the **root directory**, sub-keys represent the **subfolders**, and values represent the **file**

### **Windows OS Forensics: Event Viewer**

* Last login time will be stored in **registry key**: SAM\\Domains\\Account\\Users  
* Saves last time a user’s **password has been changed**  
* Successful or failed **logon** stored at: \\%systemroot\\%\\System32\\winevt\\logs\\Security.evtx

### **Linux OS Forensics**
- NO REGISTRY 
- Must gather system info from scattered sources 
- Different file system 
- No file creation dates 
- Different metadata 
- Updated when files are deleted 
- Files/data are mostly plain text 
- Good for string searching and interpreting data

- Basic user data in /etc/passwd 
- UID 0 account has admin privs 
- Password hashes in /etc/shadow (Brute force with “John the Ripper) 
- Group memberships in /etc/group 
- Login history: /var/log/wtmp 
- Show user, source, time and duration of login 
- Need to use the Linux last command to view 

Other logs that may contain useful data: 
```bash
/var/log/auth.log 
/var/log/secure 
/var/log/audit/audit.log
```



### **Network-based Evidence**

* **Wireless access points**: Easy to eavesdrop on traffic, usually management traffic is not encrypted  
* **Switches**: Contain mapping table between ports and MAC address, traffic can also be captured  
* **Routers**: Contain a mapping for ports to networks and can do packet filtering  
* **DHCP Server**: Logs contain leased IP addresses by MAC address mappings  
* **Authentication (AAA) servers**: Log successful / failed login attempts for all devices within their authentication domains  
* **Network intrusion detection / prevention system (NIDS/NIPS)**: Detect attacks in progress with tunable granular data  
* **Firewalls**: Can keep logs of the sessions, which can serve as digital evidence  
* **Web proxy**: Can store web surfing logs for the entire organization.

### **Web Server Log**

Web server logs provide extremely useful information for forensic investigators  
![[Pasted image 20261120003028.png]]

![[Pasted image 20261120003038.png]]

### **Network Trace**

Linearized **bit-copy** of **collected data** exchanged over the **network**, which can be used for **packet analysis**, **flow analysis**, and **protocol analysis**

Used for:

* **Detection** of potential and actual attack (Port Scanning, DoS attack)  
* Protocol **reverse engineering** (Analysis of botnet chatter)  
* **Inspect** the communications (Intercept message exchanges)  
* Detect **payload patterns** (Website fingerprinting)

### **Network Trace: Sniffer**

1. Connect the sniffer to a hub  
2. Connect to switch’s SPAN port  
3. Use a network tap on the ingress connection side of the switch

### **Packet Analysis**

Examination of content and/or metadata of one or more packets individually or together.

* Identify packet of interest and develop a strategy for flow analysis or content reconstruction  
* Tools for packet analysis (Wireshark, ngrep)

#### **Parsing Protocol Fields**

Extract content of protocol fields within packets of interest

#### **Packet Filtering**

Separate packets based on the **values of fields** in **protocol metadata**

#### **Pattern Matching**

Identify packets of interest by **matching specific values** within the **packet capture**  
![[Pasted image 20261120003102.png]]

![[Pasted image 20261120003112.png]]

# **IoT Security**

### **IoT**
- Physical objects that can be assigned IP addresses or unique identifiers 
- Better accuracy, efficiency, higher productivity



### **Types of IoT Application**
- **Consumer** IoT: Light fixtures, home appliances, and voice assistance for the elderly 
- **Commercial** IoT: Application of IoT in the healthcare and transport industries, such as smart pacemakers, monitoring systems, and vehicle-to-vehicle communication  
- **Industrial Internet of Things**: Digital control systems, statistical evaluation, smart agriculture, and industrial big data.  
- **Infrastructure IoT**: Enables connectivity of smart cities through the use of infrastructure sensors, management systems, user-friendly user apps.  
- **Military Things (IoMT)**: IoT in military field, such as robots for surveillance and human-wearable biometrics for combat

### **IoT Device Security Challenges**
- **Weak authentication & authorization**: Default password and rogue IoT devices 
- **Lack of Encryption**: Vulnerable to data breach or theft, especially those used for medical imaging and patient monitoring, and security cameras.  
- **Insecure Communication**: Lack of network segmentation, and adoption of Bluetooth technology, protocols like HTTP and API, allow cyber criminals to exploit the IoT device.  
- **Difficulty in Patching and Updating Devices**: IoT devices are not designed to receive regular IoT security updates, firmware updates/patches, and perform dynamic testing.

### **Vulnerability Exploit**
- **Buffer Overflow**: IoT devices have small memory, excess data easily spills over into other parts of the memory space, overwriting it. 
(Malware can end up rewriting the code of the device itself.)
- **Code Injection**: IoT running multiple commands without required interaction with system admin.  (Easily to execute malicious command)
- **Cross-Site Scripting**: IoT devices provide web-based interface, attacker is able to infect the legitimate page with malware.

### **Password Attack**

* Targets IoT devices because usually nobody monitors the events for failed password login.  
* Most people use easy passwords for IoT devices. So if an attacker gets access to one device, they get access to all devices.

### **Man-in-the-Middle Attack: Sniffing**

* Attack intercepts the Internet traffic that goes into and out of IoT devices.  
* The preferred target is the WiFi router, since it contains all traffic data sent from the network and can be used to control each device connected to it, including IoT devices.

### **Man-in-the-Middle Attack: Spoofing**
- Attacker can spoof the IoT device to trick the router into allowing it on the network. 

- Once the attacker device A can communicate with the router, it can inject malware into it. This malware then spreads to all the other devices on the network

### **Botnet Enslaving**
- IoT device are prime candidate for botnet, easier to hack and harder to diagnose if compromised. 
- Once enslaved, it can be used for wide variety of cybercriminal activities
### **Data Leakage**
- IoT devices process a lot of personal information in different industries or use cases. 
- Most of the IoT devices have access to this information such as: Medical data Location data Usage Patterns Search History Financial Information

### **Phishing**

Extract credentials by pretending to be from a legitimate organization or individual  
**What information are they looking for ?**

* Username & Password  
* Banking account number  
* Credit Card Information  
* Access to / Control of systems

Legitimate companies will not ask for **personal information** nor will they supply a link in an email. Rather they will ask you to **log into their site directly** from your browser and check your account.

Those who click on link gets directed to a site created to steal email credentials

### **Spear Phishing**

Attacker is **targeting you specifically**

* They **know a bit** about you (Online profile)  
* Know your **name**, e-mail will be **personalised**  
* Use URL shorteners to **hide actual link**  
* May contain malicious payload  
* Inconsistent message headers  
* Suspicious URLs

## **Spotting Phishing in General**

* No identifying information in the addressing (Except spear)  
* “From” address in display doesn’t match full message details of “Received from”  
* Awkward phrasing and spelling errors (Less likely from business or professional enterprise)  
* Create a sense of urgency (Mentions need for fast response)  
* Links to click on (**Hover, DO NOT CLICK**) deceptive url redirecting you somewhere else or presence of “shortened” links  
* Ask for private personal or financial info  
* Compelled to validate or confirm your account by entering your authentication information.

### **Phish Tank**

* Website which allows people to submit suspected phishing sites  
* Provide API for developers to check their site for websites which may be phishing

### **Pharming**
- Redirect website’s traffic to another fake site 
- Can be conducted either by changing the host file on the victim's computer or by exploitation of vulnerability in DNS server software. 
- URL \-\> DNS Server \-\> Translate to IP address 
- Browser then connects to IP address and loads the website

One way of pharming is to ‘**poison**’ the DNS  
(Your local DNS cache could be corrupted through a malware infection/attack

You type in the legit address but are relocated to the attackers phishing website  
**Pharming is less common than phishing**

## **Human Aspects of Security**

### **Authority**

* People respect authority  
* Pose in position of authority, provide service (Fireman and “Cable guy”)

#### **Different types of authority can be used:**
- Legal: Based upon government and law, generally applies to law / safety enforcement officers  
- Organizational: Any authority defined by means of an organization, typically refers to a supervisory hierarchy  
- Social: Social group could consist of co-workers, colleague friends or any other gathering of people 

Social Authority can be used to an advantage in a social engineering engagement by asking or pressuring the target for information.



### **Charm (Empath)**

Make people like / sympathize with you 

### **Pretext**
- Attackers focus on creating a good pretext, or fabricated scenario Prepare for expected questions 

- Used to try and steal their victims’ personal information / targeted object Advanced attacks sometimes try to trick targets into doing something that abuses an organization’s digital and/or physical weakness

(Sometimes, charm is categorized as pretext as it may not be possible to draw a definitive dividing line)

### **Baiting**
- Use a false promise to pique a victim’s greed or curiosity 
- Lure users into a trap that steals their personal information or inflicts their systems with malware 
- Use physical media to disperse malware (USB Drop) 
- Online forms of baiting, enticing ads that lead to malicious sites that encourage users to download malware-infected applications.

### **Reciprocation**
- Expectation that you will treat others the way they treat you 
- People don’t want to be indebted (Human nature to feel obliged to return a favor) 
- Manipulating somebody to feel grateful or obligated to the social engineer 
- Manipulating a victim into compliance by promising (Benefits in the future, something they want/need)
