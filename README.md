# Cheat Sheet

- [Cheat Sheet](#cheat-sheet)
    - [BaseT cable](#baset-cable)
  - [Cat cables frequency/speed:](#cat-cables-frequencyspeed)
    - [Cat5:](#cat5)
    - [Cat5e(Extended):](#cat5eextended)
    - [Cat6:](#cat6)
      - [Pattern:](#pattern)
  - [IP:](#ip)
    - [IP bit size:](#ip-bit-size)
    - [Private IPs:](#private-ips)
    - [IP Classes:](#ip-classes)
    - [Loopback IP:](#loopback-ip)
    - [Multicast IP:](#multicast-ip)
    - [IPv6](#ipv6)
      - [Structure](#structure)
      - [Conventions](#conventions)
    - [IPv6 -> IPv4 Transition Mechanisms](#ipv6---ipv4-transition-mechanisms)
    - [LLA(Link-Local Address)/AIPA(Automatic Private IP Adressing)](#llalink-local-addressaipaautomatic-private-ip-adressing)
    - [Subneting Masks](#subneting-masks)
      - [Takewaways](#takewaways)
      - [Calculating subnet](#calculating-subnet)
        - [CIDR(Classles Inter-Domain Routing)](#cidrclassles-inter-domain-routing)
  - [IEEE 802.11 Wireless Standard](#ieee-80211-wireless-standard)
    - [WEP(Wired Equivalent Privacy)](#wepwired-equivalent-privacy)
    - [WEP2](#wep2)
    - [WPA(Wi-Fi Protected Access)](#wpawi-fi-protected-access)
      - [WPA Encryption Protocols](#wpa-encryption-protocols)
      - [TKIP(Temporary Key Integrity Protocol)](#tkiptemporary-key-integrity-protocol)
      - [CCMP(CTRmode with CBC-MAC Protocol)](#ccmpctrmode-with-cbc-mac-protocol)
    - [802.11](#80211)
      - [Protocol Table](#protocol-table)
        - [Notes](#notes)
      - [Takeaways:](#takeaways)
        - [Protocol Compatibility](#protocol-compatibility)
          - [Protocol Compatibility Table](#protocol-compatibility-table)
        - [Maximum Throughput](#maximum-throughput)
  - [IEEE 802.1X](#ieee-8021x)
  - [Network Protocols](#network-protocols)
    - [OSI Protocols](#osi-protocols)
      - [Mnemonic:](#mnemonic)
    - [VPN(Virtual Private Network)](#vpnvirtual-private-network)
    - [VTP(VLAN Tunneling Protocol)](#vtpvlan-tunneling-protocol)
      - [Trunk port](#trunk-port)
    - [IKE(Internet Key exchange)](#ikeinternet-key-exchange)
    - [NTP(Network Time Protocol)](#ntpnetwork-time-protocol)
    - [TTL(Time to Live)](#ttltime-to-live)
    - [NetBIOS](#netbios)
      - [NBT/NetBT/NBNS(NetBIOS over TCP/IP)](#nbtnetbtnbnsnetbios-over-tcpip)
      - [WINS(Windows Internet Name Service)](#winswindows-internet-name-service)
    - [Contention](#contention)
    - [DNS](#dns)
      - [Records](#records)
      - [DNS Zones](#dns-zones)
      - [FQDN(Fully) Qualified Domain Name)](#fqdnfully-qualified-domain-name)
      - [DNSSEC(DNS Security Extencion)](#dnssecdns-security-extencion)
      - [DNS Cache](#dns-cache)
    - [LDAP(Lightweight Directory Access Protocol)](#ldaplightweight-directory-access-protocol)
  - [Ports](#ports)
    - [Well Known Ports](#well-known-ports)
    - [Registered Ports](#registered-ports)
  - [Network Topologies](#network-topologies)

---
### BaseT cable
Ethernet over twisted pair
Range from Cat3 to Cat8
Uses 8P8C (8 Position 8 Contact) modular connector, generally called *RJ45*

## Cat cables frequency/speed:
(All compatible)


### Cat5:
    100 MHz
    100 Mbps
    10/100 Eth/FastEth
    100 meters (90m Recommended)

### Cat5e(Extended):
    350 MHz
    1 Gbp/s @ 30m 
    300 Mbit/s @ 100m
    10/100/1000 Eth/FastEth/GbEth
    100 meters (90m Recommended)

### Cat6:
    550 MHz
    10 Gbps
    10/100/1000 Eth/FastEth/GbEth
    100 meters (90m Recommended)

#### Pattern: 
- **Frequency:** 100 - + 250 - 350+ 200 - 550
- **Ethernet:** 10(eth)/100(FastEth) - .add(1000(GbEth))
- **Bandwidth:** 
```haskell
c5 = 100
c5e = c5*10 --1000
c6 = c5e*10 --10 000
```
- **Length Limit**: Max 100*m*, 90*m* Recommended for [Cat5](#cat5), [Cat5e](#cat5eextended), [Cat6](#cat6)
- Corsstalk reduces with each iteration


## IP:

### IP bit size:
    v4 -> 32 bit
    v6 -> 128 bit

### Private IPs:
    Class A: 10.*
    Class B: 172.[16..31].*
    Class C: 192.168.*   

### IP Classes:
```haskell
typeA: [1..126]
-- 1 to loopback - 1
typeB: [128..191]
-- From looback + 1 to "the classic" 192 - 1
typeC: [192..223]
-- 192 (Classic) to multicast - 1
```

### Loopback IP:
- v4 -> 127.0.0.1
- v6 -> ::1

Think *Localhost* <br>
**Note:** Loopback IPv4 address stands in the A class range and its a good anchor point for the limit of the Type A

### Multicast IP:
```haskell
v4 = [224.0.0.0 .. 239.255.255.255]
```

### IPv6

#### Structure
Eight groups of 4 hexadecimal numbers, each quartet has the capability of 16 bit for a total of 128 bit.
First 64 bits (4 quartets) identify the network, the last 64 bits identify the host.

You can configure it in two ways:
1. Sequencialy **e.g ->** *2001:bce4::2*,*2001:bce4::3*
2. Using the MAC addresses to identify the hosts, it is the default for automatic IPv4 Addressing

#### Conventions
Since it's size is defined, anything that is not put is assumed to be zero **e.g** *8::1* -> 0008:0000:0000:0000:0000:0000:0000:0001
Thus the example of the [Loopback Address](#loopback-ip) *::1* = *0000:0000:0000:0000:0000:0000:0000:0001*

### IPv6 -> IPv4 Transition Mechanisms

* #### 6to4
  Allows IPv6 packets to be transmitted over an IPv4 network
Unlike [Turedo tunneling](#teredo-tunneling)

* #### Teredo tunneling
  Gives full IPv6 connectivity for capable hosts on an IPv4 network.
Unlike [6to4](#6to4) it can perform it's functions through NAT
Note that it increases the attack surface


### LLA(Link-Local Address)/AIPA(Automatic Private IP Adressing)
These are IP's given to systems when they can't access the DHCP Server
In Microsoft Platforms this system has the name of APIPA and the adresses given are:

- IPv4 -> 169.254.*
- IPv6 -> fe80::/10

### Subneting Masks

|            Netmask             |     | Hosts | Addresses |
| :----------------------------: | --- | :---: | :-------: |
|          255.255.0.0           | /16 | 35534 |   35536   |
|         255.255.128.0          | /17 | 32764 |   32768   |
|         255.255.192.0          | /18 | 10382 |   16384   |
|         255.255.224.0          | /29 | 8190  |   8192    |
|         255.255.240.0          | /20 | 4094  |   4096    |
|         255.255.248.0          | /21 | 2046  |   2048    |
|         255.255.252.0          | /22 | 1022  |   1024    |
|         255.255.254.0          | /23 |  510  |    512    |
| :arrow_forward:  255.255.255.0 | /24 |  254  |    256    |
|        255.255.255.128         | /25 |  126  |    128    |
|        255.255.255.192         | /26 |  62   |    64     |
|        255.255.255.224         | /27 |  30   |    32     |
|        255.255.255.240         | /28 |  14   |    16     |
|        255.255.255.248         | /29 |   6   |     8     |
|        255.255.255.252         | /30 |   2   |     4     |
|        255.255.255.254         | /31 |   1   |     2     |

#### Takewaways
  
  1. They never end in [32, 64]
  2. They always end in even numbers with the exception of:
     1. 0
     2. 255
  3. Pattern: [0,128,192,224,240,248,252,254,255]
     1. **NOTE**: *255.255.255.255* Is **NOT** a valid sequence
    
#### Calculating subnet

##### CIDR(Classles Inter-Domain Routing)
For the netmask  255.255.255.128 what is the CIDR?
**R:** The *CIDR = 8+8+8+1 = 24* therefore 192.168.1.1 /25

| 182 | 64 | 32 | 16 | 8 | 4 | 2 | 1 | Sum | Total 1 |
|-----|----|----|----|---|---|---|---|-----|---------|
| 1   | 1  | 1  | 1  | 1 | 1 | 1 | 1 | 255 | 8       |
| 1   | 1  | 1  | 1  | 1 | 1 | 1 | 1 | 255 | 8       |
| 1   | 1  | 1  | 1  | 1 | 1 | 1 | 1 | 255 | 8       |
| 1   | 0  | 0  | 0  | 0 | 0 | 0 | 0 | 128 | 1       |

**Therefore**
The CIDR value = Sum the number of 1's in the netmask
The min ip value is: 192.168.1.1
The max ip value is: 192.168.1.125 (127-2)

**Example Exercise:**
IP: 192.198.0.0 /22

binary Netmask: 11111111.11111111.11111100.000000 -> There is a total of 22 (up)bits
decimal Netmask: 255.255. :arrow_down_small: 

                        182 | 64 | 32 | 16 | 8 | 4 | 2 | 1 |
                        1     1     1   1    1   1   0   0
                        182 + 64 + 32 + 16 + 8 + 4 + 0 + 0 = 252
      or sum the zeros  ---------------------------- 2  +1  = 3
      then subtract from 255 -> 255 - 3 = 252
netmask: 255.255.252.0


**Total number of Hosts:**
 *min*: 192.168.0.1
 *max:*  192.168.3.254
 `You have 2 available bits (for a total of 0 to 3 in decimal) free in the 3rd group of the mask`

## IEEE 802.11 Wireless Standard

### WEP(Wired Equivalent Privacy)
Key size of: 10 or 26 Hex Digits (40/104 bits)
Replaced by [WPA](#wpawi-fi-protected-access)
Now considered a Weak form of network protection
### WEP2
Key size of: 128 bits

### WPA(Wi-Fi Protected Access)
Composed of 3 version:
  - WPA
  - WPA2
  - WPA3
#### WPA Encryption Protocols
Far more secure and advanced than [WEP](#wepwired-equivalent-privacy)
- [TKIP](#tkiptemporary-key-integrety-protocol)
- [CCMP](#ccmpctrmode-with-cbc-mac-protocol)

#### TKIP(Temporary Key Integrity Protocol)
128 bit per packet key
Dynamicly generates a new key for each packet

#### CCMP(CTRmode with CBC-MAC Protocol)
Based on AES, a cryptographic algorithm

### 802.11

#### Protocol Table
##### Notes
- Frequency has to do with where in *"space"* does the network communicate
  - Thus this defines what networks can talk with each other
  - The slowest speed will always be the defined one
- Bandwidth tells you the distance between *"lanes"* in the frequency highway
  - This is what creates the channels and there are generally 14 of them
 
| Protocol | Frequency (Ghz) | Bandwidth(Mhz) |    Max DataRate(Mbit/s)     | Indoor Range(m) | Outdoor Range (m) |
| :------: | :-------------: | :------------: | :-------------------------: | :-------------: | :---------------: |
| 802.11a  |        5        |    5/10/20     |             54              |       35        |        120        |
| 802.11b  |       2.4       |       22       |             11              |       35        |        140        |
| 802.11g  |       2.4       |    5/10/20     |             54              |       38        |        140        |
| 802.11n  |      2.4/5      |     20/40      |          288.8/600          |       70        |        250        |
| 802.11ac |        5        |  20/40/60/160  | [346.8, 800, 1733.2 3466.8] |       35        |         ?         |

#### Takeaways:
##### Protocol Compatibility
- 5 Ghz
  - 802.11a
  - 802.11n
  - 802.11ac
- 2.4 Ghz
  - 802.11b
  - 802.11g
  - 802.11n

This means that the protocol *802.11n* is the most incompatible since it operates at both frequencies.

###### Protocol Compatibility Table

| Compatibility |      802.11a       |      802.11b       |      802.11g       |      802.11n       |      802.11ac      |
| :-----------: | :----------------: | :----------------: | :----------------: | :----------------: | :----------------: |
|    802.11a    | :white_check_mark: |        :x:         |        :x:         | :heavy_check_mark: | :heavy_check_mark: |
|    802.11b    |        :x:         | :white_check_mark: | :heavy_check_mark: | :heavy_check_mark: |        :x:         |
|    802.11g    |        :x:         | :heavy_check_mark: | :white_check_mark: | :heavy_check_mark: |        :x:         |
|    802.11n    | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: | :heavy_check_mark: |
|   802.11ac    | :heavy_check_mark: |        :x:         |        :x:         | :heavy_check_mark: | :white_check_mark: |

- *802.11n* is compatible with **Everything!**
- *802.11a*, *802.11ac* are compatible with each other (and *802.11n*)
- *802.11b*, *802.11g* are compatible with each other (and *802.11n*)

Thus the compatibility of *802.11b* and *802.11g* (with the exclusion of the *802.11n* rule) are the logical negative of the *802.11a* and *802.11ac* compatibility.

```haskell
compatibility[802.11a, 802.11ac] /= compatibility[802.11g, 802.11b]
```


##### Maximum Throughput
- 54 Mbit/s
  - 802.11a
  - 802.11g
- 11 Mbit/s
  - 802.11b
- 600 Mbit/s
  - 802.11n
- 3466.8 Mbit/s
  - 802.11ac 




## IEEE 802.1X
- Port based NAC(Network Access Control)(PNAC)
- Deals with the connection security of networks 



## Network Protocols

### OSI Protocols
1. Physical
   - [IEEE 802.11](#ieee-80211-wireless-standard)
   - USB
   - Bluetooth
   - L2TP (Layer 2 Tunneling Protocol)
2. Data Link
   - Frame Relay
   - MAC
   - VLAN
3. Network
   - [IP](#ip)
   - IPsec ([Sa](#ikeinternet-key-exchange))
4. Transport
   - TCP
   - UDP
5. Session
   - [NetBIOS](#netbios)
6. Presentation
   - XDR
7. Application
   - HTTP
   - [NTP](#ntpnetwork-time-protocol)
   - DHCP
   - Telnet
   - [DNS](#dns)
   - SSH
   - etc.

#### Mnemonic:
**A***ll* **P***eople* **S***eem* **T***o* **N***eed* **D***ata* **P***rocessing*

### VPN(Virtual Private Network)
Extends a VLAN across a public network, forming an encrypted connection across the internet to resources in a private network.

### VTP(VLAN Tunneling Protocol)
Cisco proprietary protocol that allows the configuration of multiple switches to a single VLAN without having to configure each switch manually one at a time.
#### Trunk port
A Trunk port is a port that supports VLAN traffic between two switches.

### IKE(Internet Key exchange)
A protocol used in the SA(Security Association) in IPsec

### NTP(Network Time Protocol)
Protocol for time synchronization between packet switched connected systems.

### TTL(Time to Live)
Also known as hib limit, it limits the lifetime of data in a computer or network.
Used in:
- IP Packets
- [DNS Records](#records)
- [DNS Cache](#dns-cache)
- HTTP (Header responses)



### NetBIOS
Provides services related to the session layer of the OSI model.
Normally runs over TCP/IP via the NBT(NetBIOS over TCP/IP) Protocol, which results in the network having both an IP address and a NetBIOS name corresponding to a possibly different host name.

#### NBT/NetBT/NBNS(NetBIOS over TCP/IP)
Allows legacy systems reliant on the NetBIOS API to use modern TCP/IP networks

#### WINS(Windows Internet Name Service)
Microsoft's implementation of the [NBNS](#nbtnetbtnbnsnetbios-over-tcpip).
It's to NetBIOS what DNS is to Domain Names.

### Contention
A *"Listen before talk"* approach to communication to avoid collisions.

### DNS

#### Records

| Record                   | Description                                                      |
| ------------------------ | ---------------------------------------------------------------- |
| A                        | Maps Domain Names to IPv4 Addresses (DN -> IPv4)                 |
| AAAA ("A4")              | Maps Domain Names to IPv6 Addresses (DN -> IPv6                  |
| CNAME(Canonical Name)    | Redirects Domain Names to other Domain Names (DN -> DN           |
| MX (Maill Exchanger)     | Points to e-mail Services (e.g @outlook.com)                     |
| NS (Name Server)         | Points to another DNS Server                                     |
| PTR (Pointer)            | Maps IP Adresses to Domain Names (IP -> DN)                      |
| SRV (Service)            | Points to services within a domain                               |
| SOA (Start of Authority) | Indicates the beginning of a Zone, therefore each Zone has a SOA |
| TXT                      | Basically just comments                                          |

#### DNS Zones
![DnsZones](https://www.cloudflare.com/img/learning/dns/glossary/dns-zone/dns-zone.png)

#### FQDN(Fully) Qualified Domain Name)
Also refereed as Absolute Domain Name.
It's a Domain Name that specifies it's exact location in the tree hierarchy of the DNS.
Think:
  myhost in the domain example.com
  the fully qualified name is -> [myhost.example.com](http://example.com/)
Extension

#### DNSSEC(DNS Security Extencion)
A specification that adds security resources to the DNS Server.
It provides authentication and integrity but no DoS.
It's a scheme of public and private keys, and with the digital certificates one can be sure of the DNS Server's Identity

#### DNS Cache
This is a cache of DNS results stored in the client so that the next time that the user asks for the site it won't call on the DNS server but instead it will go directly to the address.
This value has a [TTL](#ttltime-to-live).

### LDAP(Lightweight Directory Access Protocol)
A lightweight protocol to scan for the network's resources :grey_question:

## Ports

### Well Known Ports

| Port | Protocol                  |
| ---- | ------------------------- |
| 9    | Wake-on-LAN               |
| 20   | FTP Data                  |
| 21   | FTP Control               |
| 22   | SSH                       |
| 23   | Telnet                    |
| 25   | SMT                       |
| 37   | Time                      |
| 42   | Host name Server          |
| 43   | Whois                     |
| 53   | DNS                       |
| 69   | TFTP                      |
| 80   | HTTP                      |
| 109  | POP2                      |
| 110  | POP3                      |
| 115  | SFTP                      |
| 118  | SQL Services              |
| 137  | NetBIOS Name Service      |
| 139  | NetBIOS Datagram Service  |
| 150  | NetBIOS Sessing Service   |
| 156  | SQL Server                |
| 161  | SNMP                      |
| 179  | Border Gateway Protocol   |
| 190  | Gateway Access Protocol   |
| 194  | Internet Chat Relay (IRC) |
| 443  | HTTPS                     |
| 444  | SNPP                      |
| 445  | Microsoft-DS              |
| 458  | Apple QuickTime           |
| 546  | DHCP Client               |
| 547  | DHCP Server               |
| 569  | MSN                       |
| 1080 | Socks                     |

### Registered Ports

| Port           | Protocol                                            |
| -------------- | --------------------------------------------------- |
| 1119           | Battle.net chat/game :video_game:                   |
| 1194           | OpenVPN                                             |
| 1293           | IPsec                                               |
| 1433           | MSSQL Server                                        |
| 1434           | MSSQL Monitor                                       |
| 1512           | [WINS](#winswindows-internet-name-service)          |
| 1723           | PPTP                                                |
| 1812           | RADIUS Authentication                               |
| 1813           | RADIUS Accounting                                   |
| 2010           | Artemis: Spaceship Bridge Simulator :space_invader: |
| 3306           | MySQL                                               |
| 3389           | Microsoft RDP (WBT)                                 |
| 3960/3962      | Warframe                                            |
| [5000, 5500]   | League of Legends                                   |
| 5432           | PostgreSQL                                          |
| 5984           | CouchDB                                             |
| [6000..6063]   | X11 over Network                                    |
| 6379           | Redis                                               |
| [6463..6472]   | Discord                                             |
| *8080*, *8008* | Alternative to HTTP                                 |
| [9001, 9030]   | Tor Network :                                       |
| 9150           | Tor Browser :computer:                              |
| [27000..27009] | Steam Game Client                                   |
| [27015..27030] | Steam Matchmaking/Downloads                         |
| 27017          | MongoDB                                             |
| 33434          | traceroute                                          |


## Network Topologies
![NetworkTopologies](https://upload.wikimedia.org/wikipedia/commons/9/97/NetworkTopologies.svg)

