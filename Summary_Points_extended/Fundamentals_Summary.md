## <u> OSI Model and TCP Model</u>
- **The OSI Model** we just looked at is just a reference/logical model. It was designed to describe the functions of the communication system by dividing the communication procedure into smaller and simpler components. 

- **The TCP/IP model** is a concise version of the OSI model. It contains four layers, unlike seven layers in the OSI model. 

| Layer | Device Type | OSI Layer | TCP/IP model | TCP/IP New (actual) | Protocols | PDU
--|--|--|--|--|--|--
7 | Gateway | **Application** | Application| Application | HTTP, FTP, POP, SMTP, DNS, RIP | Data
6 | -       | **Presentation**| Application| Application | HTTP, FTP, POP, SMTP, DNS, RIP, MIME | Data
5 | -       | **Session**     | Application| Application | HTTP, FTP, POP, SMTP, DNS, RIP, SCP | Data
4 | -       | **Transport**   | Transport  | Transport | TCP/UDP | Segments
3 | Router  | **Network**     | Internet   | Network | IP, ARP, ICMP, IGMP | Packets
2 | Switch/bridge | **Data Link** | Link   | Data Link | Ethernet, Token Ring | Frames
1 | Hubs/Repeater | **Physical**  | Link   | Physical | Ethernet, Token Ring | Bits

### <u>TCP Handshake</u>

<h4 align="center">The Three-way handshake</h4>
<p align="center">
<img width="77%" src="https://wiki.mikrotik.com/images/f/fc/Image2001.gif">
</p>

#### ✅ TCP Connection establishment process 
1. **Host A** sends out a **SYN** (synchronize) packet with proposed initial sequence number to Host B.
2. **Host B** receives **SYN** message, it returns a packet with both SYN and ACK flags (**SYN-ACK**) set in the [TCP header](https://www.gatevidyalay.com/transmission-control-protocol-tcp-header/).
3. **Host A** receives the **SYN-ACK**, it sends back **ACK** (Acknowledgment) packet.
4. **Host B** receives **ACK** and at this stage the connection is **ESTABLISHED.**

#### ❌ TCP Connection termination
1. **Host A** sends a **FIN** (finish) flag, indicating that is has finished sending the data.
2. **Host B** who receives the **FIN**, doest not terminate the connection but enters into a "passive close" (CLOSE_WAIT) state and sends the **ACK** for the **FIN** back to the Host A.
3. **Host A** enters into a (TIME_WAIT) state, and sends an **ACK** back to the Host B.
4. **Host B** gets the **ACK** from the Host A and **closes the connection.**

⚠️ *Sequence numbers increase on new communication.  Example is computers A and B.  A would increment B's sequence number.  A would never increment it's own sequence.*

### <u>TCP Flags</u>

| Flag | Name           | Function                                                     |
| ---- | -------------- | ------------------------------------------------------------ |
| SYN  | Synchronize    | Set during initial communication.  Negotiating of parameters and sequence numbers |
| ACK  | Acknowledgment | Set as an acknowledgement to the SYN flag.  Always set after initial SYN |
| RST  | Reset          | Forces the termination of a connection (in both directions)  |
| FIN  | Finish         | Ordered close to communications                              |
| PSH  | Push           | Forces the delivery of data without concern for buffering    |
| URG  | Urgent         | Data inside is being sent out of band.  Example is cancelling a message |

### <u>Port Numbers</u>

- **Internet Assigned Numbers Authority** (IANA) - maintains Service Name and Transport Protocol Port Number Registry which lists all port number reservations

- Ranges

  - **Well-known ports** - 0 - 1023

  - **Registered ports** - 1024 - 49,151

  - **Dynamic ports** - 49,152 - 65,535

    | Port Number | Protocol | Transport Protocol |
    | ----------- | -------- | ------------------ |
    | 20/21       | FTP      | TCP                |
    | 22          | SSH      | TCP                |
    | 23          | Telnet   | TCP                |
    | 25          | SMTP     | TCP                |
    | 53          | DNS      | TCP/UDP            |
    | 67          | DHCP     | UDP                |
    | 69          | TFTP     | UDP                |
    | 80          | HTTP     | TCP                |
    | 110         | POP3     | TCP                |
    | 135         | RPC      | TCP                |
    | 137-139     | NetBIOS  | TCP/UDP            |
    | 143         | IMAP     | TCP                |
    | 161/162     | SNMP     | UDP                |
    | 389         | LDAP     | TCP/UDP            |
    | 443         | HTTPS    | TCP                |
    | 445         | SMB      | TCP                |
    | 514         | SYSLOG   | UDP                |

  - A service is said to be **listening** for a port when it has that specific port open

  - Once a service has made a connection, the port is in an **established** state

  - **`Netstat`** command:

    - Shows open ports on computer
    - **netstat -an** displays connections in numerical form
    - **netstat -b** displays executables tied to the open port (admin only)

### <u>Subnetting</u>

- **IPv4 Main Address Types**
  - **Unicast** - acted on by a single recipient
  - **Multicast** - acted on by members of a specific group
  - **Broadcast** - acted on by everyone on the network
    - **Limited** - delivered to every system in the domain (255.255.255.255)
    - **Directed** - delivered to all devices on a subnet and use that broadcast address
- **Subnet mask** - determines how many address available on a specific subnet
  - Represented by three methods
    - **Decimal** - 255.240.0.0
    - **Binary** - 11111111.11110000.00000000.00000000
    - **CIDR** - x.x.x.x/12   (where x.x.x.x is an ip address on that range)
  - If all the bits in the host field are 1s, the address is the broadcast
  - If they are all 0s, it's the network address
  - Any other combination indicates an address in the range
 
- 
### <u>ARP</u>

- Resolves IP address to physical address

### <u>Network Security Zones</u>

- **Internet** - uncontrollable
- **Internet DMZ** - controlled buffer network
- **Production Network Zone** - very restricted; controls direct access from uncontrolled zones; has no users
- **Intranet Zone** - controlled; has little to no heavy restrictions
- **Management Network Zone** - might find VLANs and IPSEC; highly secured; strict policies

### <u>Vulnerabilities</u>

- **Common Vulnerability Scoring System** (CVSS) - places numerical score based on severity
- **National Vulnerability Database** (NVD) - US government repository of vulnerabilities

### <u>Vulnerability Categories</u>

- **Misconfiguration** - improperly configuring a service or application
- **Default installation** - failure to change settings in an application that come by default
- **Buffer overflow** - code execution flaw
- **Missing patches** -  systems that have not been patched
- **Design flaws** - flaws inherent to system design such as encryption and data validation
- **Operating System Flaws** - flaws specific to each OS
- **Default passwords** - leaving default passwords that come with system/application

### <u>Vulnerability Management Tools</u>

- Nessus
- Qualys
- GFI Languard
- Nikto
- OpenVAS
- Retina CS

### <u>Terms to Know</u>

- **Hack value** - perceived value or worth of a target as seen by the attacker
- **Zero-day attack** - attack that occurs before a vendor knows or is able to patch a flaw
- **Doxing** - searching for and publishing information about an individual usually with a malicious intent
- **Enterprise Information Security Architecture** (EISA) - process that determines how systems work within an organization
- **Incident management** - deals with specific incidents to mitigate the attack

### <u>Threat Modeling</u>

- Identify security objectives
- Application Overview
- Decompose application
- Identify threats
- Identify vulnerabilities

### <u>Risk Management</u>

- Risk identification
- Risk assessment
- Risk treatment
- Risk tracking
- Risk review

  *Uses risk analysis matrix to determine threat level

### <u>Types of  Security Controls</u>

| Description    | Examples                                      |
| -------------- | --------------------------------------------- |
| Physical       | Guards, lights, cameras                       |
| Technical      | Encryption, smart cards, access control lists |
| Administrative | Training awareness, policies                  |

| Description  | Examples                    |
| ------------ | --------------------------- |
| Preventative | authentication, alarm bells |
| Detective    | audits, backups             |
| Corrective   | restore operations          |

### <u>Business Analysis</u>

- Business Impact Analysis (BIA)

  - Maximum Tolerable Downtime (MTD)

- Business Continuity Plan (BCP)

  - Disaster Recovery Plan (DRP)

- Annualized Loss Expectancy (ALE)

  - Annual Rate of Occurrence (ARO)

  - Single Loss Expectancy (SLE)
    $$
    ALE = SLE * ARO
    $$

**User Behavior Analysis** (UBA) - tracking users and extrapolating data in light of malicious activity

### <u>CIA Triad</u>

- **Confidentiality** - passwords, encryption
- **Integrity** - hashing, digital signatures
- **Availability** - anti-dos solutions

**Bit flipping** is an example of an <u>integrity</u> attack.  The outcome is not to gain information - it is to obscure the data from the actual user.

Confidentiality != authentication - MAC address spoofing is an authentication attack

### <u>Common Criterial for Information Technology Security Evaluation</u>

- Routinely called "Common Criteria" (CC)
- **Evaluation Assurance Level** (EAL) - goes from level 1 - 7
- **Target of Evaluation** - the system that is being tested
- **Security Target** (ST) - document describing the TOE and security requirements
- **Protection Profile** (PP) - security requirements that are specific to the type of device being tested

### <u>Access Control Types</u>

- **Mandatory** (MAC) - access is set by an administrator
- **Discretionary** (DAC) - allows users to give access to resources that they own and control

### <u>Security Policies</u>

- **Access Control** - what resources are protected and who can access them
- **Information Security** - what can systems be used for
- **Information Protection** - defines data sensitivity levels
- **Password** - all things about passwords (how long, characters required, etc.)
- **E-Mail** - proper and allowable use of email systems
- **Information Audit** - defines the framework used for auditing

### <u>Policy Categorizations</u>

- **Promiscuous** - wide open
- **Permissive** - blocks only known dangerous things
- **Prudent** - blocks most and only allows things for business purposes
- **Paranoid** - locks everything down

**Standards** - mandatory rules to achieve consistency

**Baselines** - provide the minimum security necessary

**Guidelines** - flexible or recommended actions

**Procedures** - step by step instructions

**Script Kiddie** - uneducated in security methods, but uses tools that are freely available to perform malicious activities

**Phreaker** - manipulates telephone systems

### <u>The Hats</u>

- **White Hat** - ethical hackers
- **Black Hat** - hackers that seek to perform malicious activities
- **Gray Hat** - hackers that perform good or bad activities but do not have the permission of the organization they are hacking against

**Hacktivist** - someone who hacks for a cause

**Suicide Hackers** - do not case about any impunity to themselves; hack to get the job done

**Cyberterrorist** - motivated by religious or political beliefs to create fear or disruption

**State-Sponsored Hacker** - hacker that is hired by a government

### <u>Attack Types</u>

- **Operating System** (OS) - attacks targeting OS flaws or security issues inside such as guest accounts or default passwords
- **Application Level** - attacks on programming code and software logic
- **Shrink-Wrap Code** - attack takes advantage of built-in code or scripts
- **Misconfiguration** - attack takes advantage of systems that are misconfigured due to improper configuration or default configuration

**Infowar** - the use of offensive and defensive techniques to create an advantage

### <u>Hacking Phases</u>

1. **Reconnaissance**  - gathering evidence about targets
2. **Scanning & Enumeration** - obtaining more in-depth information about targets
3. **Gaining Access** - attacks are leveled in order to gain access to a system
4. **Maintaining Access** - items put in place to ensure future access
5. **Covering Tracks** - steps taken to conceal success and intrusion

### <u>Types of Reconnaissance</u>

- **Passive** - gathering information about the target without their knowledge
- **Active** - uses tools and techniques that may or may not be discovered

### <u>Security Incident and Event Management (SIEM)</u>

- Functions related to a security operations center (SOC)
  - Identifying
  - Monitoring
  - Recording
  - Auditing
  - Analyzing

**Ethical hacker** - employs tools that hackers use with a customer's permission; always obtains an agreement from the client with specific objectives <u>before</u> any testing is done

**Cracker** - uses tools for personal gain or destructive purposes

### <u>Penetration Test</u>

- Clearly defined, full scale test of security controls
- Phases
  - **Preparation** - contracts and team determined
  - **Assessment** - all hacking phases (reconnaissance, scanning, attacks, etc.)
  - **Post-Assessment** - reports & conclusions
- Types
  - **Black Box** - done without any knowledge of the system or network
  - **White Box** - complete knowledge of the system
  - **Gray Box** - has some knowledge of the system and/or network

### <u>Law Categories</u>

- **Criminal** - laws that protect public safety and usually have jail time attached
- **Civil** - private rights and remedies
- **Common** - laws that are based on societal customs


### <u>Laws and Standards</u>

- **OSSTM Compliance** - "Open Source Security Testing Methodology Manual" maintained by ISECOM , defines three types of compliance
  - **Legislative** - Deals with government regulations (Such as SOX and HIPAA)
  - **Contractual** - Deals with industry / group requirement (Such as PCI DSS)
  - **Standards based** - Deals with practices that must be followed by members of a given group/organization (Such as ITIL ,ISO and OSSTMM itself)
  
- **OSSTM Controls**
  - **OSSTM Class A - Interactive Controls**
    - *Authentication* -  Provides for identification and authorization based on credentials 
    - *Indemnification* - Provided contractual protection against loss or damages
    - *Subjugation* - Ensures that interactions occur according to processes defined by the asset owner
    - *Continuity* -  Maintains interactivity with assets if corruption of failure occurs
    - *Resilience* - Protects assets from corruption and failure
   
  
  
  - **OSSTM Class B  - Process Controls**
      - *Non-repudiation* - Prevents participants from denying its actions
      - *Confidentiality* - Ensures that only participants know of an asset
      - *Privacy* - Ensures that only participants have access to the asset
      - *Integrity* - Ensures that only participants know when assets and processes change
      - *Alarm*  - Notifies participants when interactions occur
      
- **ISO 27001** - Security standard based on the British BS7799 standard, focuses on security governance

- **NIST-800-53** -  Catalogs security and privacy controls for federal information systems, created to help implementation of FISMA

- **ISO 27002 AND 17799** - Based on BS799 but focuses on security objectives and provides security controls based on industry best practice

- **FISMA** - "Federal Information Security Modernization Ac Of 2002" A law updated in 2004 to codify the authority of the Department of Homeland Security with regard to implementation of information security policies 
  
- **FITARA** - "Federal Information Technology Acquisition Reform Act" A 2013 bill that was intended to change the framework that determines how the US GOV purchases technology 

- **HIPAA** - "Health Insurance Portability and Accountability Act" a law that set's privacy standards to protect patient medical records and health information shared between doctors, hospitals and insurance providers

- **PCI-DSS**  - "Payment Card Industry Data Security Standard" Standard for organizations handling Credit Cards, ATM cards and other POS cards

- **COBIT** - "Control Object for Information and Related Technology" IT Governance framework and toolset, created by ISACA and ITGI

- **SOX** - "Sarbanes-Oxley Act" Law that requires publicly traded companies to submit to independent audits and to properly disclose financial information

- **GLBA** - "U.S Gramm-Leach-Bliley Act" Law that protects the confidentiality and integrity of personal information that is collected by financial institutions.

- **CSIRT** - "Computer Security Incident Response Team" CSIRT provided a single point of contact when reporting computer security incidents

- **ITIL** - "Information Technology Infrastructure Library" - An operational framework developed in the '80s that standardizes IT management procedures 

### <u>Controls</u>

- **Directive** - Also known as procedural controls because they deal with company procedures such as security policies, operations plans, and guidelines. 
- **Deterrent** - Controls that are used to dissuade potential attackers, such as signs that warn possible attackers about the alarm system and monitoring in place.
- **Preventive**  - Controls used to stop potential attacks by preventing users from performing specific actions, such as encryption and authentication
- **Compensating** - Controls used to supplement directive controls, such as administrator reviewing logs files for violations of company policy
- **Detective** -  Controls used to monitor and alert on malicious or unauthorized activity, such as IDS's and CCTV feeds monitored in real life
- **Corrective** - Controls used to repair damage caused by malicious events. Such as AntiVirus software and IPS (IPS being both a detective and corrective control) 
- **Recovery**
