# CNS488 Security Testing and Assessment

# Lecture Notes 

## Welcome to CNS-388/488

### Definitions 

* **Threat** - A potential cause of an incident, that may result in harm of systems and organization., An actor that poses risk to your organization and its assets.
* **Vulnerability** - A weakness of an asset or group of assets that can be exploited by one or more threats. Requires (1) A existing flaw, (2) Access to the flaw, (3) Capability of an attacker to exploit the flaw. 
* **Exploit** - Software, code or computer instructions designed to rake advantage of a security flaw. 
* ```HACKER (Threat) --> BRUTE FORCE (exploit) --> WEAK PASSWORD (vulnerability)```
* **Advanced Persistent Threats (APT)** - Generally targeted attacks in which the threat has advanced capabilities.  These types of attacks involve a high level of stealth.
* **Phishing** - Sending fake emails that look to be from legitimate sources in order to gather information from a victim.
* **Trojans** - Malware that is disguised as legitimate software.
* **Botnets** - A group of attacker controlled systems used for malicious inten.t (ex: DDoS)
* **Ransomware** - Malware that encrypts a victims computer and demands payment for decryption.  
* **Distributed Denial of Service (DDoS)** - An attack that involves several systems generating enough traffic that the victim is unable to function normally.
* **Malware** - A generic term for malicious software.  
* **Worm** - A self-replicating piece of malware that actively replicates to other systems. (Ex: Wannacry)
* **Virus** - A self-replicating piece of malware that requires user intervention to propagate (Ex: USB).
* **Antivirus** - is a computer program used to prevent, detect, and remove malware.
* **Firewall** - a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules.
* **Intrusion Detection System (IDS)** - security software designed to automatically alert administrators when someone or something is trying to compromise information system through malicious activities or through security policy violations.
* **Web Gateway** - type of security solution that prevents unsecured traffic from entering an internal network of an organization.
* **Data Loss Prevention (DLP)*** - set of tools and processes used to ensure that sensitive data is not lost, misused, or accessed by unauthorized users.
* **Sandbox** - security mechanism for separating running programs, usually in an effort to mitigate system failures or software vulnerabilities from spreading.
* **Security information and event management (SIEM)** - software products and services that  combine security information management and security event management. 
* **endpoint detection and response (EDR)** - software solutions that collect, record, and store large volumes of data from endpoint activities to provide security professionals with the comprehensive visibility they need to detect, investigate, and mitigate advanced cyber threats.
* **User Behavior Analytics (UEBA)** - cybersecurity process about detection of insider threats, targeted attacks, and financial fraud.   
* **Security Orchestration and Automation (SOAR)** - refers to a method of connecting security tools and integrating disparate security systems. It is the connected layer that streamlines security processes and powers security automation.

### Protocols 

* **FTP (File Transfer Protocol)** - standard network protocol used for the transfer of computer files between a client and server on a computer network.
* **FTPS (FTP overSSL)** - adds support for the Transport Layer Security and the Secure Sockets Layer cryptographic protocols. 
* **SSH (Secure Shell)** - remote management, cryptographic network protocol for operating network services securely over an unsecured network.
* **SFTP (Secure File Transfer Protocol)** -  a network protocol used for secure file transfer over secure shell.
* **SCP (Secure Copy / copy over SSH)** -  copies files over a secure, encrypted network connection. 
* **TELENT** - old remote management protocol (precedes SSH) 
* **DNS (Domain Name System)** -  hierarchical decentralized naming system for computers, services, or other resources connected to the Internet or a private network.
* **TFTP (Trivial File Transfer Protocol)** - simple lockstep File Transfer Protocol which allows a client to get a file from or put a file onto a remote host
* **HTTP(s) (Hypertext Transfer Protocol (Secure))** - The Hypertext Transfer Protocol is an application protocol for distributed, collaborative, and hypermedia information systems. HTTP is the foundation of data communication for the World Wide Web.Secure is an extension of the Hypertext Transfer Protocol for secure communication over a computer network, and is widely used on the Internet. 
* **SNMP (Simple Network Management Protocol)** - protocol for collecting and organizing information about managed devices on IP networks and for modifying that information to change device behavior. Devices that typically support SNMP include cable modems, routers, switches, servers, workstations, printers, and more.
* **RDP Remote Desktop Protocol)** - Remote Desktop Protocol is a proprietary protocol developed by Microsoft, which provides a user with a graphical interface to connect to another computer over a network connection.
* **iSCSl ( Internet Small Computer Systems Interface)** - an Internet Protocol-based storage networking standard for linking data storage facilities.
* **IPv4** - Internet Protocol version 4 
* **IPv6** - Internet Protocol version 6
* **ICMP (Internet Control Message Protocol)** - The Internet Control Message Protocol is a supporting protocol in the Internet protocol suite.
* **NetBIOS/LLMNR** - windows name resolutions 
* **SSL/TLS** - encyption layer 
* **IPsec** - Internet Protocol Security is a secure network protocol suite of IPv4 that authenticates and encrypts the packets of data sent over an IPv4 network.

### Ethical Hacking 

**Ethical hacking** – Act in a professional manner, with authorization of the client, and “do no harm”. The purpose of ethical hacking – Use the same tools as the “bad guys” to find issues first (hopefully). 

Types of Hackers:
* Black Hat Hackers: criminals and wrongdoers
* White Hat Hackers: ethical hackers who work to protect systems and people
* Grey Hat Hackers: dabble in both black hat and white hat tinkering

**Security Assessment** – Provides an overview of the overall security posture of an organization 

**Vulnerability Assessment** - The process of identifying and quantifying security vulnerabilities in an environment.

#### Penetration Test
- An authorized simulated attack against a target to find and exploit security gaps
- Scope – A large group of IP Addresses and/or domains
- Time –  Short in length (1 – 4 weeks
- Goal – Confirm vulnerabilities, fulfill compliance requirements

#### Red Team Assessment
- An authorized simulated attack against a target to find and exploit security gaps
- Scope – Focused on a single objective
- Time – can be short or long term (months)
- Goal – Test People, Processes, and/or Technology

#### Concept of location
1. Remote - Exploits sent across the network, hacker has no access to the system prior to running the exploit
2. Local – Exploit run directly on a compromised system, from the compromised system, and with access

#### Ethical Hacking Phases
1. Reconnaissance - Goal of this phase is to identify targets of interest
2. Scanning - Goals of this phase are to determine the parameters of systems of interest 
3. Gaining Access - Utilizing exploits or targeted solutions against systems and vulnerabilities to gain access
4. Maintaining Access - Once compromised, keep access to the system for an extended period of time. Adding backdoors, remote access trojans/tools (RATs), and root kits are a means to maintain access. 
5. Covering Tracks - clean up don't leave your dirty work. 

#### Types of Attacks
1. Remote Network – i.e. from the internet
2. Remote Dial-Up Network – Phone systems, modems, SCADA systems, etc.
3. Local Network – Attacks from the local network via Ethernet or WiFi
4. Stolen Equipment – Theft of system or resource owned by employees
5. Social Engineering – Exploiting people
6. Physical Entry – Self explanatory

#### Ethical Hacking Tests

1. Black Box – No prior knowledge of the network or systems
2. White Box – Complete knowledge of the network and systems
3. Gray Box – Internal testing which simulates an internal attack against the TOE - OR In addition to active and passive we have:
    * Internal– Originate from inside the network or security perimeter, i.e. the “insider”
    * External– Originate from outside the network or security perimeter
    * Social – Testing people to defeat CIA controls
    * Physical – Testing physical security controls     
    * Wireless – Testing wireless security controls

#### Standards
* Penetration Testing Execution Standard
* Open Source Security Testing Methodology Manual (OSSTM)

#### Ethics 101
* Obtain client authorization
* Maintain and follow a non-disclosure agreement (NDA)
* Maintain confidentiality during the engagement
* Not exceed the limits of the engagement

#### Pentest Timeline

```
Initial Client Meeting -> Sign NDA -> Security Evaluation Plan -> Conduct the Test -> Report and Documentation -> Present Report Findings
```
## Footprinting, Recon, and Social Engineering

Footprinting is the initial step you will take in a pen test. The depth or amount of footprinting will depending on the type of assessment. It Consists of determining Specific domains, Network addresses or network blocks, Network devices, routers, IDS/IPS and firewalls and Email systems, name servers, web application server, and other publicly facing systems for the target. 

### Things to gather during this Footprinting: 
- Domain names
- Network blocks, services and applications
- Specific IP addresses
- Phone numbers, contact addresses, maps, email addresses
- Related organizations or companies
- Current events, employee postings, job postings, resumes
- System architecture
- IDS/IPS, filters, firewalls, etc.
- Authentication mechanisms

### Intel Gathering:
- OSINT – Open-Source Intelligence (passive) - Data collected from publicly available sources 
- HUMINT – Human Intelligence (active) - Information gathered from a human
- SIGINT – Signals Intelligence (active) - Information gathered from interception of signals

Some useful Google commands include (usage is command:term):
- **site** – searches for a specific term/phrase on a specific site
- **filetype** – searches for a specific term/phrase within a specific filetype
- **link** – searches for a specific term/phrase to identify linked pages
- **intitle** - searches for a specific term/phrase within the title of a document
- **inurl** - searches for a specific term/phrase within the URL

### DNS/IP/Email Recon

#### DNS 
- Enumerate DNS zones to find systems by name and network address
- Shows the type of internet accessible systems due to naming convention 

**DNS record types you should know**
- A – host record which maps a name to IP
- SOA – start of authority record which IDs the DNS server which owns the zone
- CNAME – alias for a record (i.e. mapping many names to a single IP)
- MX – mail exchanger record which IDs the mail server and order they should be contacted in
- SRV – services record (_service._proto.name TTL class SRV priority weight port target).  Examples are LDAP and Kerberos in MS AD
- PTR – pointer record maps IPs to names
- NS – name server record IDs the name servers responsible for resolution for the domain

### Social Engineering

What is social engineering - The use of non technical methods used to gather information about a target:
- Human-based – person to person contact and using deception and manipulation
   - Impersonating employees, end users, or someone of importance
   - Calling technical support
   - Shoulder surfing/dumpster diving
- Computer-based – Using software to retrieve the information
   - Email attachments
   - Fake websites
   - Pop-up windows (not so much anymore)
- Other social engineering
   - Insider attacks – getting hired by the target or service provider
   - Phishing attacks
   - Online scams
   - URL obfuscation
   
### Tor Networks
- Allows for anonymous internet usage though the Tor network
- Users of the network install ToR proxy services in order to access the network
- Relays communication through a series of routers which utilize multi-layer encryption (IP of sender and receiver are not both readable at any point in the network)

# Book & Supplemental Readings 

## Hacking Exposed 7: Network Security Secrets & Solutions 

### CHAPTER 1 FOOTPRINTING

The systematic and methodical footprinting of an organization enables attackers to create a near complete profile of an organization’s security posture. Using a combination of tools and techniques, coupled with a healthy dose of patience and mind-melding, attackers can take an unknown entity and reduce it to a specific range of domain names, network blocks, subnets, routers, and individual IP addresses of systems directly connected to the Internet, as well as many other details pertaining to its security posture. 

Footprinting is necessary for one basic reason: it gives you a picture of what the hacker sees. And if you know what the hacker sees, you know what potential security exposures you have in your environment.

Archived Information - Be aware that there are sites on the Internet where you can retrieve archived copies of information that may no longer be available from the original source. These archives could allow an attacker to gain access to information that has been deliberately removed for security reasons.

One of the most serious misconfigurations a system administrator can make is allowing untrusted Internet users to perform a DNS zone transfer. A zone transfer allows a secondary master server to update its zone database from the primary master. This provides for redundancy when running DNS, should the primary name server become unavailable. Generally, a DNS zone transfer needs to be performed only by secondary master DNS servers. Many DNS servers, however, are misconfigured and provide a copy of the zone to anyone who asks. This isn’t necessarily bad if the only information provided is related to systems that are connected to the Internet and have valid hostnames, although it makes it that much easier for attackers to find potential targets. The real problem occurs when an organization does not use a public/private DNS mechanism to segregate its external DNS information (which is public) from its internal, private DNS information. In this case, internal hostnames and IP addresses are disclosed to the attacker. Providing internal IP address information to an untrusted user over the Internet is akin to providing a complete blueprint, or roadmap, of an organization’s internal network.

**Traceroute** is a diagnostic tool originally written by Van Jacobson that lets you view the route that an IP packet follows from one host to the next. Traceroute uses the time-to-live (TTL) field in the IP packet to elicit an ICMP TIME_EXCEEDED message from each router. Each router that handles the packet is required to decrement the TTL field. Thus, the TTL field effectively becomes a hop counter. We can use the functionality of traceroute to determine the exact path that our packets are taking. As mentioned previously, traceroute may allow you to discover the network topology employed by the target network, in addition to identifying access control devices (such as an application-based firewall or packet-filtering routers) that may be filtering our traffic.


## Supplemental Online

### [ISACA – Planning for Security Testing](https://www.isaca.org/Journal/archives/2016/volume-5/Documents/Planning-for-Information-Security-Testing_joa_Eng_0916.pdf)

#### types of information security testing:

Vulnerability scan—This scan examines the security of individual computers, network devices or applications for known vulnerabilities. Vulnerabilities are identified by running a scanner, sniffers, reviewing configurations, etc. 

Security assessment—This builds upon thevulnerability assessment by adding manual verification of controls to confirm exposure by reviewing settings, policies and procedures

Penetration test—This happens one step ahead of a vulnerability assessment. It takes advantage of the known and unknown (e.g., zero-day attacks) vulnerabilities. It also makes use of social engineering techniques to exploit the human component of cybersecurity.

#### Strategy: Internal vs. External 

External—This is, perhaps, the most widely-used form of pen-testing. It addresses the ability of a remote attacker to get to the internal network. 

Internal—Contrary to what management usually thinks this is, it is not a strategy applicable to vulnerability assessment work only. Pen-tests can be run internally when the goal is to simulate what would happen if a company’s own employeeattempted to carry out an attack from within or if an attacker managed to gain access to a network. 

#### Pen-test Plan Template

1. BACKGROUND 
2. GOALS 
    - OBJECTIVES
        1. SCOPE
        2. STRATEGY
        3. TEAMING
        4. TYPE
        5. ANALYSIS TECHNIQUE
        6. SUCCESS FACTORS
    - OBJECTIVES
        1. SCOPE
        2. STRATEGY
        3. TEAMING
        4. TYPE
        5. ANALYSIS TECHNIQUE
        6. SUCCESS FACTORS
3. SCHEDULE - 
4. RISK AND CONTINGENCIES
5. ASSUMPTIONS
6. DELIVERABLES
7. CONTACTS
8. APPROVALS
9. ADDENDUMS
    
### http://www.pentest-standard.org/index.php/Intelligence_Gathering 

