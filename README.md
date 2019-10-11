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
    - [6to4](#6to4)
    - [Teredo tunneling](#teredo-tunneling)
    - [Multicast IP:](#multicast-ip)
    - [Loopback IP:](#loopback-ip)
    - [Private IPs:](#private-ips)
    - [IP Classes:](#ip-classes)
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
    - [VTP(VLAN Tunneling Protocol)](#vtpvlan-tunneling-protocol)
    - [IKE(Internet Key exchange)](#ikeinternet-key-exchange)
    - [NTP(Network Time Protocol)](#ntpnetwork-time-protocol)
    - [TTL(Time to Live)](#ttltime-to-live)
    - [FQDN(Fully) Qualified Domain Name)](#fqdnfully-qualified-domain-name)
    - [NetBIOS](#netbios)
      - [NBT/NetBT/NBNS(NetBIOS over TCP/IP)](#nbtnetbtnbnsnetbios-over-tcpip)
      - [WINS(Windows Internet Name Service)](#winswindows-internet-name-service)
    - [Contention](#contention)
    - [DNS](#dns)
      - [DNS Zones](#dns-zones)
    - [LDAPU(Lightweight Directory Access Protocol)](#ldapulightweight-directory-access-protocol)
  - [Ports](#ports)
    - [Well Known Ports](#well-known-ports)
    - [Registered Ports](#registered-ports)
  - [Network Topologies](#network-topologies)

---
### BaseT cable
Ethernet over twisted pair
Range from Cat3 to Cat8
Uses 8P8C (8 Position 8 Contact) modular connector, generally called $RJ45$

## Cat cables frequency/speed:
(All compatible)


### Cat5:
    100 MHz
    100 Mbps
    10/100 Eth/FastEth
    100 meters (90m Recommended)

### Cat5e(Extended):
    350 MHz
    1 Gbps
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
- **Length Limit**: Max 100$m$, 90$m$ Recommended for [Cat5](#cat5), [Cat5e](#cat5eextended), [Cat6](#cat6)
- Corsstalk reduces with each iteration

---
## IP:

### IP bit size:
    v4 -> 32 bit
    v6 -> 128 bit

### 6to4
Allows IPv6 packets to be transmitted over an IPv4 network
Unlike [Turedo tunneling](#teredo-tunneling)

### Teredo tunneling
Gives full IPv6 connectivity for capable hosts on an IPv4 network.
Unlike [6to4](#6to4) it can perform it's functions through NAT
Note that it increases the attack surface

### Multicast IP:
```haskell
v4 = [224.0.0.0 .. 239.255.255.255]
```

### Loopback IP:
- v4 -> 127.0.0.1
- v6 .> ::1

Think $Localhost$

### Private IPs:
    10.*
    192.168.*
    172.[16..31].*

### IP Classes:
```haskell
typeA: [1..126]
typeB: [128..191]
typeC: [192..223]
```

---

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
- Frequency has to do with where in $"space"$ does the network communicate
  - Thus this defines what networks can talk with each other
  - The slowest speed will always be the defined one
- Bandwidth tells you the distance between $"lanes"$ in the frequency highway
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

This means that the protocol $802.11n$ is the most incompatible since it operates at both frequencies.

###### Protocol Compatibility Table

| Compatibility |      802.11a       |      802.11b       |      802.11g       |      802.11n       |      802.11ac      |
| :-----------: | :----------------: | :----------------: | :----------------: | :----------------: | :----------------: |
|    802.11a    | :white_check_mark: |        :x:         |        :x:         | :heavy_check_mark: | :heavy_check_mark: |
|    802.11b    |        :x:         | :white_check_mark: | :heavy_check_mark: | :heavy_check_mark: |        :x:         |
|    802.11g    |        :x:         | :heavy_check_mark: | :white_check_mark: | :heavy_check_mark: |        :x:         |
|    802.11n    | :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: | :white_check_mark: | :heavy_check_mark: |
|   802.11ac    | :heavy_check_mark: |        :x:         |        :x:         | :heavy_check_mark: | :white_check_mark: |

- $802.11n$ is compatible with **Everything!**
- $802.11a$, $802.11ac$ are compatible with each other (and $802.11n$)
- $802.11b$, $802.11g$ are compatible with each other (and $802.11n$)

Thus the compatibility of $802.11b$ and $802.11g$ (with the exclusion of the $802.11n$ rule) are the logical negative of the $802.11a$ and $802.11ac$ compatibility.
$$
compatibility[802.11a, 802.11ac] \neg compatibility[802.11g, 802.11b]
$$

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

---


## IEEE 802.1X
- Port based NAC(Network Access Control)(PNAC)
- Deals with the connection security of networks 

---

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

### VTP(VLAN Tunneling Protocol)
Cisco proprietary protocol that allows the configuration of multiple switches to a single VLAN without having to configure each switch manually one at a time.

### IKE(Internet Key exchange)
A protocol used in the SA(Security Association) in IPsec

### NTP(Network Time Protocol)
Protocol for time synchronization between packet switched connected systems.

### TTL(Time to Live)
Also known as hib limit, it limits the lifetime of data in a computer or network.
Used in:
- IP Packets
- DNS Records
- HTTP (Header responses)

### FQDN(Fully) Qualified Domain Name)
Also refereed as Absolute Domain Name.
It's a Domain Name that specifies it's exact location in the tree hierarchy of the DNS.
Think:
  myhost in the domain example.com
  the fully qualified name is -> [myhost.example.com](http://example.com/)

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

#### DNS Zones
![DnsZones](https://www.cloudflare.com/img/learning/dns/glossary/dns-zone/dns-zone.png)

### LDAPU(Lightweight Directory Access Protocol)



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
| 179  | Border Gateway Protocol    |
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
| $8080$, $8008$ | Alternative to HTTP                                 |
| [9001, 9030]   | Tor Network :                                       |
| 9150           | Tor Browser :computer:                              |
| [27000..27009] | Steam Game Client                                   |
| [27015..27030] | Steam Matchmaking/Downloads                          |
| 27017          | MongoDB                                             |
| 33434          | traceroute                                          |
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

---

## Network Topologies
![NetworkTopologies](https://upload.wikimedia.org/wikipedia/commons/9/97/NetworkTopologies.svg)

---