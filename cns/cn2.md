
### Firewalls

A **firewall** is a network security device that monitors and filters incoming and outgoing network traffic based on an organization's previously established security policies. A firewall typically establishes a barrier between a trusted internal network and untrusted external networks, such as the internet.

### Different Types of Delays

1. **Propagation Delay**
   - Time taken for a signal to travel from the sender to the receiver.
   - Depends on the distance and the speed of the medium.

2. **Transmission Delay**
   - Time taken to push all the packet's bits into the wire.
   - Depends on the packet length and transmission rate.

3. **Processing Delay**
   - Time taken to process the packet header.
   - Involves error checking and determining the packet's destination.

4. **Queuing Delay**
   - Time a packet spends waiting in a queue before it can be transmitted.
   - Depends on the network traffic and the capacity of the router.

### 3-Way Handshaking (TCP Connection Establishment)

The **3-way handshake** is a process used in TCP/IP networks to establish a connection between a client and server. It ensures that both sides are synchronized and ready for data transfer.

1. **SYN:** The client sends a SYN (synchronize) packet to the server to initiate a connection.
2. **SYN-ACK:** The server responds with a SYN-ACK (synchronize-acknowledge) packet, indicating it is ready for communication.
3. **ACK:** The client sends an ACK (acknowledge) packet back to the server, confirming the connection is established.

### Server-Side Load Balancer

A **server-side load balancer** distributes incoming network traffic across multiple servers to ensure no single server becomes overwhelmed. This improves the availability and reliability of applications. Load balancers use various algorithms like round-robin, least connections, and IP hash to decide how to distribute traffic.

### RSA Algorithm

The **RSA algorithm** is an asymmetric cryptographic algorithm used for secure data transmission. It involves two keys: a public key for encryption and a private key for decryption.

1. **Key Generation:** Generate two large prime numbers and calculate their product.
2. **Public Key:** Consists of the modulus and the public exponent.
3. **Private Key:** Consists of the modulus and the private exponent.
4. **Encryption:** Encrypt data using the recipient's public key.
5. **Decryption:** Decrypt data using the recipient's private key.

### HTTP and HTTPS Protocol

- **HTTP (HyperText Transfer Protocol):** A protocol used for transmitting hypertext over the web. It is stateless and does not secure the data being transmitted.
- **HTTPS (HyperText Transfer Protocol Secure):** An extension of HTTP that uses SSL/TLS to encrypt the data being transmitted, ensuring data integrity and privacy.

### SMTP Protocol

**SMTP (Simple Mail Transfer Protocol)** is a protocol for sending email messages between servers. It is a push protocol used to deliver email from the sender's server to the recipient's server.

### TCP and UDP Protocols: Differences in Table Form

| Feature                | TCP (Transmission Control Protocol)            | UDP (User Datagram Protocol)                     |
|------------------------|------------------------------------------------|-------------------------------------------------|
| Connection             | Connection-oriented                            | Connectionless                                  |
| Reliability            | Ensures data delivery with error checking      | No guarantee of data delivery                   |
| Flow Control           | Provides flow control using window mechanism   | No flow control                                 |
| Overhead               | Higher overhead due to error checking and control | Lower overhead, minimal error checking          |
| Use Case               | Suitable for applications needing reliability  | Suitable for applications needing speed         |
| Examples               | HTTP, FTP, SMTP                                | DNS, VoIP, video streaming                      |

### What Happens When You Enter “google.com” (Simplified Version)

1. **DNS Resolution:** The browser checks its cache and the OS for the IP address of "google.com." If not found, it queries a DNS server.
2. **TCP Connection:** A TCP connection is established with Google's server using a 3-way handshake.
3. **HTTP Request:** The browser sends an HTTP request to Google's server.
4. **Server Response:** Google's server processes the request and sends back an HTTP response.
5. **Rendering:** The browser renders the HTML, CSS, and JavaScript from the response to display the webpage.

### Hub vs Switch

| Feature           | Hub                                           | Switch                                        |
|-------------------|-----------------------------------------------|-----------------------------------------------|
| Layer             | Physical Layer (Layer 1)                      | Data Link Layer (Layer 2)                     |
| Function          | Broadcasts data to all devices in the network | Sends data only to the destination device     |
| Efficiency        | Less efficient, more collisions               | More efficient, reduces collisions            |
| Intelligence      | No intelligence, simple data repeater         | Intelligent, learns MAC addresses             |
| Use Case          | Small, simple networks                        | Larger, more complex networks                 |

### VPN

A **VPN (Virtual Private Network)** creates a secure, encrypted connection over a less secure network, such as the internet. It ensures privacy and security by tunneling traffic through a private server.

#### Advantages:
- Enhances security and privacy.
- Allows remote access to resources.
- Bypasses geo-restrictions and censorship.

#### Disadvantages:
- Can reduce internet speed.
- May be blocked by some services.
- Requires proper configuration and maintenance.

### LAN

A **LAN (Local Area Network)** is a network that connects devices within a limited area such as a home, school, or office building. It allows connected devices to share resources and information.

