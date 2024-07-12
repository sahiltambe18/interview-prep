
### Define Network

A **network** is a collection of computers, servers, network devices or other devices connected to one another to allow the sharing of data and resources. These connections can be wired or wireless, facilitating communication and resource sharing among the connected devices.

### Network Topology

**Network topology** refers to the arrangement of different elements (links, nodes, etc.) in a computer network. It is the geometric representation of how these devices are interconnected. 

#### Types of Network Topologies

1. **Bus Topology**
   - All devices share a single communication line or bus.
   - Easy to install, but a failure in the main cable can disable the entire network.

2. **Star Topology**
   - All devices are connected to a central hub.
   - If the hub fails, the entire network is affected.

3. **Ring Topology**
   - Each device is connected to two other devices, forming a circular data path.
   - Data travels in one direction, reducing collision chances.

4. **Mesh Topology**
   - Every device is connected to every other device.
   - Provides high redundancy and reliability but is costly and complex.

5. **Tree Topology**
   - A combination of star and bus topologies.
   - Hierarchical, with groups of star-configured devices connected to a bus.

6. **Hybrid Topology**
   - A combination of two or more different types of topologies.
   - Offers flexibility and scalability.

### Define Bandwidth, Node, and Link

- **Bandwidth:** The maximum rate of data transfer across a given path. It is usually measured in bits per second (bps).
- **Node:** Any active, physical, and electronic device attached to a network. Examples include computers, printers, switches, and routers.
- **Link:** The physical medium or logical connection that connects two nodes in a network. Examples include cables, wireless signals, and optical fibers.

### Explain TCP Model

The **TCP/IP model** is a four-layered suite of protocols designed for the internet. The layers are:

1. **Application Layer**
   - Provides protocols for specific data communication services on a process-to-process level.
   - Examples: HTTP, FTP, SMTP.

2. **Transport Layer**
   - Ensures reliable data transfer between devices.
   - Examples: TCP (Transmission Control Protocol), UDP (User Datagram Protocol).

3. **Internet Layer**
   - Routes data packets across networks.
   - Examples: IP (Internet Protocol), ICMP (Internet Control Message Protocol).

4. **Network Interface Layer**
   - Defines the physical and logical link between the data link and the physical transmission media.
   - Examples: Ethernet, Wi-Fi.

### Layers of OSI Model

1. **Physical Layer**
   - Deals with the physical connection between devices and the transmission of binary data.

2. **Data Link Layer**
   - Provides error detection and correction and manages data frames between two nodes.

3. **Network Layer**
   - Handles the routing of data packets across the network.

4. **Transport Layer**
   - Ensures end-to-end communication, error recovery, and flow control.

5. **Session Layer**
   - Manages sessions and connections between applications.

6. **Presentation Layer**
   - Ensures data is in a readable format for the application layer and handles encryption/decryption.

7. **Application Layer**
   - Provides network services directly to end-users and applications.

### Significance of Data Link Layer

The **Data Link Layer** is responsible for node-to-node data transfer, error detection and correction, and framing. It ensures that data is successfully transmitted over the physical layer and reaches its destination without errors. It also manages MAC addresses and controls how devices on the same network can access the data and media.

### Define Gateway and Difference Between Gateway and Router

A **gateway** is a network node that serves as an access point to another network, often translating data between different network protocols.

| Feature           | Gateway                                                | Router                                            |
|-------------------|--------------------------------------------------------|---------------------------------------------------|
| Function          | Translates data between different network protocols    | Routes data packets between different networks    |
| OSI Layer         | Operates on multiple layers                            | Primarily operates at Network Layer (Layer 3)     |
| Use Case          | Connecting different network architectures or protocols | Interconnecting different IP networks             |
| Complexity        | More complex due to protocol translation               | Simpler, focused on routing and traffic management|

### What Does Ping Command Do?

The **ping** command checks the connectivity between two network devices. It sends ICMP Echo Request messages to a target host and waits for ICMP Echo Reply messages, measuring the round-trip time and packet loss.

### What is DNS, DNS Forwarder, NIC?

- **DNS (Domain Name System):** A hierarchical system that translates human-readable domain names (like www.example.com) into IP addresses.
- **DNS Forwarder:** A server that forwards DNS queries to an external DNS server, often used to improve DNS query performance and reduce load on the primary DNS server.
- **NIC (Network Interface Card):** A hardware component that connects a computer to a network, allowing it to communicate with other networked devices.

### What is MAC Address?

A **MAC (Media Access Control) address** is a unique identifier assigned to network interfaces for communications at the data link layer of a network segment. It is typically a 48-bit address represented in hexadecimal format.

### What is IP Address, Private IP Address, Public IP Address, APIPA?

- **IP Address:** A numerical label assigned to each device connected to a computer network that uses the IP for communication.
- **Private IP Address:** IP addresses used within a private network, not routable on the internet (e.g., 192.168.0.0/16, 10.0.0.0/8).
- **Public IP Address:** IP addresses that are routable on the internet, assigned by ISPs.
- **APIPA (Automatic Private IP Addressing):** An address assigned automatically to a device when a DHCP server is not available, usually in the range 169.254.0.0/16.

### Difference Between IPv4 and IPv6 in Table Form

| Feature           | IPv4                          | IPv6                               |
|-------------------|-------------------------------|------------------------------------|
| Address Length    | 32-bit                        | 128-bit                            |
| Address Format    | Decimal, separated by dots    | Hexadecimal, separated by colons   |
| Address Example   | 192.168.1.1                   | 2001:0db8:85a3:0000:0000:8a2e:0370:7334 |
| Number of Addresses | Approximately 4.3 billion   | Approximately 340 undecillion      |
| Header Complexity | Less complex                  | More complex, supports extension headers |
| Security          | Optional, less integrated     | Mandatory, integrated into the protocol |

### What is Subnet?

A **subnet** is a segmented piece of a larger network. Subnetting divides an IP network into multiple smaller, more manageable segments or sub-networks. This helps in reducing network traffic, improving security, and managing IP address allocation efficiently. Subnets are created using a subnet mask, which determines the network and host portions of an IP address.