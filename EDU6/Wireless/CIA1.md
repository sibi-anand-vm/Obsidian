### Introduction to Wireless Local Area Networks (WLAN)

Wireless Local Area Networks (WLANs) allow devices to connect to a network without the need for physical cables. They use various wireless communication technologies to transmit data over the air. Below are some key technologies and concepts related to WLANs:

#### 1. **Infrared (IR)**

- **Infrared** communication uses infrared light waves to transmit data between devices.
    
- It is typically used for short-range communication (e.g., remote controls, IrDA).
    
- **Advantages**: Low cost, simple implementation, and no interference with radio frequencies.
    
- **Disadvantages**: Requires line-of-sight, limited range, and low data rates.
    

#### 2. **Radio Wave**

- **Radio wave** communication uses radio frequencies (RF) to transmit data.
    
- It is the most common technology used in WLANs (e.g., Wi-Fi).
    
- **Advantages**: Longer range, no line-of-sight required, and higher data rates.
    
- **Disadvantages**: Susceptible to interference and security concerns.
    

#### 3. **Spread Spectrum**

- **Spread spectrum** is a technique where the signal is spread over a wider frequency band to reduce interference and improve security.
    
- Two common types:
    
    - **Frequency Hopping Spread Spectrum (FHSS)**: The signal hops between different frequencies in a predefined pattern.
        
    - **Direct Sequence Spread Spectrum (DSSS)**: The signal is spread by multiplying it with a pseudo-random noise code.
        
- **Advantages**: Resistance to interference and eavesdropping.
    
- **Disadvantages**: More complex implementation.
    

#### 4. **UHF Narrowband**

- **Ultra High Frequency (UHF) Narrowband** communication uses a narrow range of frequencies within the UHF band.
    
- It is often used for long-range communication with low data rates.
    
- **Advantages**: Long range and low power consumption.
    
- **Disadvantages**: Limited data rates and susceptibility to interference.
    

---

### IEEE 802.11 (Wi-Fi)
The IEEE standard 802.11 is the most famous family of WLANs in which many products are available.
The primary goal of the standard was the specification of a simple and robust WLAN which offers time-bounded and asynchronous services. Additional features of the WLAN should include the support of power management to save battery power, the handling of hidden nodes, and the ability to operate worldwide.
IEEE 802.11 is a set of standards for implementing WLANs, commonly known as Wi-Fi. It defines the architecture, physical layer, and MAC layer for wireless communication.

#### 1. **Architecture**

- **Basic Service Set (BSS)**: A group of devices connected to a single access point (AP).
    
- **Extended Service Set (ESS)**: Multiple BSSs connected through a distribution system (DS) to form a larger network.
    
- **Access Point (AP)**: A device that connects wireless devices to a wired network.
    
- **Station (STA)**: Any device that connects to the WLAN (e.g., laptops, smartphones).
    
![[Pasted image 20250225160719.png]]
The architecture of the distribution system consists of bridged IEEE LANs, wireless links, or any other networks. The APs support roaming (i.e., changing access points), the distribution system handles data transfer between the different APs. APs provide synchronization within a BSS, support power management, and can control medium access to support time-bounded service.
#### 2. **Physical Layer (PHY)**
	The PHY layer is responsible for the transmission and reception of raw data bits over the wireless medium.
### DSSS (Direct Sequence Spread Spectrum)

- **How it works**: Spreads the signal over a wide frequency band using a pseudo-random code.
    
- **Key features**: High resistance to interference, high data rates, complex hardware.
    
- **Applications**: IEEE 802.11b (Wi-Fi), GPS, cellular networks.
    
![[Pasted image 20250226112732.png]]
### FHSS (Frequency Hopping Spread Spectrum)

- **How it works**: Transmits by hopping between multiple frequencies in a predefined pattern.
    
- **Key features**: High resistance to interference, lower data rates, simpler implementation.
    
- **Applications**: Bluetooth, early IEEE 802.11, military communications.
    
![[Pasted image 20250226112707.png]]
### Comparison:

| Feature               | DSSS         | FHSS                         |
| --------------------- | ------------ | ---------------------------- |
| **Bandwidth**         | Wideband     | Multiple narrowband channels |
| **Data Rates**        | Higher       | Lower                        |
| **Complexity**        | More complex | Simpler                      |
| **Power Consumption** | Higher       | Lower                        |

### Summary:

- **DSSS**: Better for high-data-rate applications.
    
- **FHSS**: Better for low-power, interference-resistant communication.
- **Modulation Techniques**:
    
    - **DSSS (Direct Sequence Spread Spectrum)**: Used in 802.11b.
        
    - **OFDM (Orthogonal Frequency Division Multiplexing)**: Used in 802.11a, 802.11g, 802.11n, 802.11ac, and 802.11ax.
        
    - **MIMO (Multiple Input Multiple Output)**: Used in 802.11n, 802.11ac, and 802.11ax to improve data rates and reliability.
- The physical layer defines how data is transmitted over the air.
    
- It includes various technologies such as:
    
    - **802.11a**: Operates in the 5 GHz band with a maximum data rate of 54 Mbps.
        
    - **802.11b**: Operates in the 2.4 GHz band with a maximum data rate of 11 Mbps.
        
    - **802.11g**: Operates in the 2.4 GHz band with a maximum data rate of 54 Mbps.
        
    - **802.11n**: Operates in both 2.4 GHz and 5 GHz bands with a maximum data rate of 600 Mbps (MIMO technology).
        
    - **802.11ac**: Operates in t he 5 GHz band with a maximum data rate of several Gbps (MU-MIMO technology).
        
    - **802.11ax (Wi-Fi 6)**: Improved efficiency and higher data rates, especially in dense environments.
        

#### 3. **MAC Layer**
The **Media Access Control (MAC)** layer manages how devices access the shared wireless medium. Key features include:

- **CSMA/CA (Carrier Sense Multiple Access with Collision Avoidance)**:
    
    - Devices listen to the channel before transmitting to avoid collisions.
        
    - If the channel is busy, the device waits for a random backoff period.
        
- **Frame Types**:
    
    - **Data Frames**: Carry user data.
        
    - **Control Frames**: Manage access to the medium (e.g., RTS/CTS).
        
    - **Management Frames**: Handle association, authentication, and beaconing.
        
- **MAC Address**:
    
    - A unique identifier for each device on the network.
#### 4. **MAC Management**

- **Power Management**:
    
    - Allows devices to enter sleep mode to conserve power.
        
    - The AP buffers packets for sleeping devices and delivers them when the device wakes up.
        
- **Roaming**:
    
    - Enables devices to switch between APs while maintaining connectivity.
        
    - Essential for mobility in large networks (e.g., ESS).
        
- **Security**:
    
    - **WEP (Wired Equivalent Privacy)**: Early security protocol (now considered insecure).
        
    - **WPA (Wi-Fi Protected Access)**: Improved security with TKIP (Temporal Key Integrity Protocol).
        
    - **WPA2/WPA3**: Uses AES (Advanced Encryption Standard) for stronger security.
        
- **Beaconing**:
    
    - APs periodically send beacon frames to announce their presence and network parameters.
    

---

### HiperLAN (High-Performance Radio LAN)

- **HiperLAN** is a set of wireless communication standards developed by the European Telecommunications Standards Institute (ETSI).
    
- It operates in the 5 GHz band and provides high data rates (up to 54 Mbps).
    
- **HiperLAN/1**: Focused on ad-hoc networking.
    
- **HiperLAN/2**: Designed for QoS support and integration with wired networks (e.g., Ethernet, ATM).
    

---

### Wireless ATM (WATM)

- **Wireless ATM** extends ATM (Asynchronous Transfer Mode) technology to wireless networks.
    
- It provides high-speed, low-latency communication with QoS support.
    
- **Applications**: Multimedia streaming, video conferencing, and real-time communication.
    

---

### **1.7.1 Bluetooth**

Bluetooth is a **wireless communication technology** designed for short-range device connectivity. It operates under the **IEEE 802.15.1 standard**, enabling data exchange over distances of up to **10 meters (30 feet)**. It functions in the **2.45GHz ISM (Industrial, Scientific, and Medical) band** and supports data transfer speeds of up to **721 Kbps** along with three voice channels.

Each Bluetooth device is assigned a **unique 48-bit address** based on the IEEE 802 standard and can connect up to **eight devices** simultaneously. Connections can be **point-to-point** (one-to-one) or **multipoint** (one-to-many). Bluetooth technology allows wireless communication between various devices such as **mobile phones, laptops, desktops, printers, cameras, and even smart appliances like coffee makers**.

One of the key advantages of Bluetooth is that it does not require a **fixed network infrastructure**. Instead, it establishes connections dynamically, forming what is known as an **ad hoc network**. These dynamic networks can be classified as **piconets** and **scatternets**.

---

### **1.7.2 Architecture**
![[Pasted image 20250226113721.png]]
Bluetooth technology consists of **two types of networks**:

#### **(i) Piconet**

A **piconet** is the basic Bluetooth network, consisting of a **primary (master) device** and up to **seven active secondary (slave) devices**. The master device controls communication, while slaves synchronize their clocks and frequency hopping with it.

- Communication can be **one-to-one** (between master and one slave) or **one-to-many** (master with multiple slaves).
- Slaves **cannot communicate directly** with each other; they must relay data through the master.
- Apart from the **eight active devices**, a piconet can include up to **255 parked (inactive) devices**, which can be activated when required.

#### **(ii) Scatternet**

A **scatternet** is a more complex network formed by multiple **interconnected piconets**. A **single device can be part of multiple piconets**, acting as a **slave in one** and a **master in another**, thus allowing communication between different networks.

Scatternets enable a **broader range of connectivity**, allowing Bluetooth devices to form **larger, more flexible networks** while reducing interference.

---

### **Applications of Bluetooth Technology**

Bluetooth technology has revolutionized wireless communication in various fields:

1. **Headsets**
    
    - Bluetooth headsets enable **hands-free** communication for phone calls.
    - Many models support **voice recognition**, allowing users to **dial and talk without touching the phone**.
2. **Stereo Headsets**
    
    - Works similarly to regular headsets but supports **wireless music streaming**.
    - Can be paired with **smartphones, tablets, and Bluetooth-enabled music players**.
3. **Bluetooth In-Car Systems**
    
    - Integrates with a car’s **audio system** to enable hands-free calling.
    - Calls can be **answered or dialed** using the car’s speaker system without holding the phone.
4. **Bluetooth Printers**
    
    - Allows wireless printing from devices like **smartphones, tablets, and laptops**.
    - Eliminates the need for **cables**, enhancing convenience.
5. **Bluetooth Webcams**
    
    - Functions like regular webcams but with **wireless mobility**.
    - Ideal for **remote work, online meetings, and video conferencing**.

---

### **Bluetooth Specifications**

#### **1. Core Specifications**

These define the **Bluetooth protocol stack** and outline the necessary **testing and qualification** standards for Bluetooth devices.

#### **2. Profiles Specification**

- Defines **usage models** and specific applications of Bluetooth technology.
- Ensures **compatibility between different Bluetooth-enabled devices**.

---

### **Bluetooth Stack and Layers**

Bluetooth technology operates through a **five-layer protocol stack**:

1. **Radio Layer**
    
    - Specifies **frequency range, modulation, and power levels** for Bluetooth transmission.
    - Operates in the **2.4GHz ISM band** using **frequency hopping** to reduce interference.
2. **Baseband Layer**
    
    - Defines **physical and logical channels** for data transfer.
    - Supports both **synchronous (voice) and asynchronous (data) transmissions**.
    - Manages **frequency hopping** and assigns **unique device addresses**.
3. **LMP (Link Manager Protocol)**
    
    - Handles **link establishment, authentication, and security**.
    - Manages **power control and encryption** between devices.
4. **L2CAP (Logical Link Control & Adaptation Protocol)**
    
    - Adapts **higher-layer protocols** to work with the Bluetooth baseband.
    - Supports **data segmentation and reassembly** for efficient communication.
5. **SDP (Service Discovery Protocol)**
    
    - Enables devices to **discover and query services** available on other Bluetooth devices.
    - Helps applications **detect compatible devices** for seamless interaction.

---

### **Conclusion**

Bluetooth technology enables **short-range wireless communication**, connecting various devices effortlessly. Its **piconet and scatternet architectures** provide flexible networking options. With continuous advancements, Bluetooth has become a crucial component of **wireless accessories, smart devices, and IoT applications**, making everyday tasks more convenient and efficient.
---

### Zigbee

- **Zigbee** is a low-power, low-data-rate wireless technology designed for IoT and home automation.
    
- It operates in the 2.4 GHz band and uses DSSS for communication.
    
- **Applications**: Smart home devices, industrial automation, and sensor networks.
    

---

### IEEE 802.16 (WiMAX)

- **WiMAX (Worldwide Interoperability for Microwave Access)** is a wireless broadband standard based on IEEE 802.16.
    
- It provides high-speed internet access over long distances (up to 50 km).
    
- **Frequency Bands**: 2.3 GHz, 2.5 GHz, 3.5 GHz, and 5.8 GHz.
    
- **Applications**: Last-mile broadband access, backhaul for cellular networks, and rural internet connectivity.
    

---

### Summary

- **WLAN Technologies**: Infrared, Radio Wave, Spread Spectrum, UHF Narrowband.
    
- **IEEE 802.11 (Wi-Fi)**: Architecture, Physical Layer, MAC Layer, MAC Management.
    
- **HiperLAN**: European alternative to Wi-Fi.
    
- **WATM**: Wireless extension of ATM.
    
- **Bluetooth**: Short-range communication for personal devices.
    
- **Zigbee**: Low-power IoT communication.
    
- **IEEE 802.16 (WiMAX)**: Long-range wireless broadband.


### **Introduction to Mobile IP**

Mobile IP is a **communication protocol** that allows devices to **maintain the same IP address** while moving across different networks. This ensures **continuous internet connectivity** even when the device changes its point of attachment to the network.

### **1. IP Packet Delivery**

In traditional IP networks, packets are routed based on the **destination IP address**, which is tied to a specific network. However, when a mobile device moves to a new network, its **IP address may no longer be valid**, causing packet loss and disruption.

#### **1.1 Problem in Traditional IP Networks**

- The IP address is **tied to a specific subnet**.
- When a device moves to a new network, it needs a **new IP address**, breaking ongoing connections.
- Standard IP routing does not support **seamless mobility**.

#### **1.2 Solution: Mobile IP**

Mobile IP enables a device to **retain its original IP address** (home address) while moving, ensuring **seamless packet delivery** by:

- **Using a home agent (HA) and foreign agent (FA)** to manage mobility.
- **Providing a care-of address (CoA)** for routing packets to the current location.
- **Utilizing tunneling and encapsulation** to forward packets transparently.

### **2. Agent Discovery**

Mobile IP relies on **agents** to facilitate communication between the mobile device and the network. These agents help the mobile device discover its location and manage IP address changes.

#### **2.1 Components of Agent Discovery**

- **Home Agent (HA)**: A router on the **home network** that maintains the mobile device's home address and forwards packets.
- **Foreign Agent (FA)**: A router on the **foreign network** (where the mobile device is currently located) that helps in packet delivery.

#### **2.2 Agent Communication**

- **Agent Advertisement**: Home and foreign agents periodically **broadcast advertisements** to inform mobile devices of their presence.
- **Agent Solicitation**: If a mobile device does not receive an advertisement, it can send a **solicitation message** to discover agents.

### **3. Tunneling and Encapsulation**

Mobile IP uses **tunneling** to forward packets from the home agent to the mobile device's **care-of address (CoA)**.

#### **3.1 Process of Tunneling**

1. The **home agent intercepts packets** destined for the mobile device’s home address.
2. The **home agent encapsulates the packets** and forwards them to the mobile device’s CoA.
3. The **foreign agent (or mobile device) decapsulates the packets** and delivers them to the device.

#### **3.2 Types of Encapsulation**

- **IP-in-IP Encapsulation**: Wraps the original IP packet inside a new IP packet.
- **Minimal Encapsulation**: Adds a smaller header to reduce overhead.
- **GRE (Generic Routing Encapsulation)**: Provides flexible tunneling for different protocols.

### **4. IPv6 and Mobile IP**

IPv6, the next-generation Internet Protocol, provides several **enhancements** for Mobile IP.

#### **4.1 Advantages of IPv6 for Mobile IP**

- **Larger Address Space**: IPv6 provides **128-bit addresses**, removing the need for NAT (Network Address Translation).
- **Built-in Mobility Support**: IPv6 includes **Mobile IPv6 (MIPv6)**, eliminating the need for separate home and foreign agents.
- **Route Optimization**: MIPv6 allows **direct communication** between the mobile device and the correspondent node, reducing latency.

#### **4.2 Key Features of Mobile IPv6 (MIPv6)**

- **Eliminates Foreign Agents**: Mobile devices can configure their own **CoA** dynamically.
- **Better Security**: Uses **IPsec** for authentication and encryption.
- **Optimized Handoff**: Reduces packet loss and delays when switching networks.

---

## **Mobile Ad-Hoc Networks (MANETs)**

A **Mobile Ad-Hoc Network (MANET)** is a **self-configuring, decentralized** network of mobile devices connected wirelessly. Unlike traditional networks, MANETs **do not rely on fixed infrastructure** like routers or access points.

### **1. Characteristics of MANETs**

- **Dynamic Topology**: Devices move freely, causing **frequent network topology changes**.
- **Multi-hop Communication**: Devices **relay data** for others when direct communication is not possible.
- **Decentralized Operation**: No central authority; **nodes cooperate** to route packets.
- **Self-healing**: The network can **automatically reconfigure itself** when nodes join or leave.
- **Limited Bandwidth & Power**: Devices operate on **battery power** and use **wireless links** with lower bandwidth than wired networks.

### **2. Routing in MANETs**

Routing in MANETs is challenging due to frequent **node mobility** and **network topology changes**. Several protocols address these challenges:

#### **2.1 Proactive (Table-Driven) Routing Protocols**

- Maintain **up-to-date routing tables** for all nodes in the network.
- Suitable for networks with **highly stable connections**.
- **Example**: **Optimized Link State Routing (OLSR)**.
- **Advantages**:
    - Low latency for route discovery.
    - Immediate access to routing information.
- **Disadvantages**:
    - High overhead due to frequent updates.

#### **2.2 Reactive (On-Demand) Routing Protocols**

- Discover routes **only when needed**, reducing overhead.
- Suitable for **highly dynamic networks**.
- **Examples**:
    - **Ad-Hoc On-Demand Distance Vector (AODV)**
    - **Dynamic Source Routing (DSR)**
- **Advantages**:
    - Lower overhead compared to proactive protocols.
- **Disadvantages**:
    - Higher latency for route discovery.

#### **2.3 Hybrid Routing Protocols**

- Combine **proactive and reactive approaches**.
- Suitable for **large and scalable networks**.
- **Example**: **Zone Routing Protocol (ZRP)**.
- **Advantages**:
    - Balances overhead and latency.

#### **2.4 Geographic Routing Protocols**

- Use **location-based** information to forward packets.
- Ideal for **large-scale MANETs**.
- **Example**: **Greedy Perimeter Stateless Routing (GPSR)**.
- **Advantages**:
    - Reduces routing overhead.
    - Efficient for geographically dispersed networks.

---

## **Applications of Mobile IP and MANETs**

### **1. Applications of Mobile IP**

- **Seamless Internet Connectivity**: Enables **uninterrupted communication** when moving across different networks.
- **Enterprise Networks**: Supports **remote work** by allowing employees to connect to their home network.
- **Military and Defense**: Ensures **secure communication** for mobile units in different locations.
- **Emergency Services**: Facilitates **real-time communication** during natural disasters.

### **2. Applications of MANETs**

- **Military Operations**: Provides **secure, decentralized** communication for soldiers in battlefields.
- **Disaster Recovery**: Enables communication when **traditional networks fail** during disasters.
- **Vehicular Ad-Hoc Networks (VANETs)**: Used in **self-driving cars** to share traffic updates.
- **IoT and Smart Cities**: Supports **sensor networks** for monitoring environmental conditions.

---

## **Conclusion**

Mobile IP and MANETs **revolutionize mobility and wireless communication**.

- **Mobile IP** ensures **seamless internet connectivity** while changing networks.
- **MANETs** provide **decentralized, infrastructure-less** networks for **dynamic environments**.

With advancements in **IPv6, 5G, and AI-driven networking**, these technologies will continue to **evolve and enhance connectivity worldwide**. 🚀

---

### Summary

- **Mobile IP**: Enables seamless IP packet delivery for mobile devices using agent discovery, tunneling, and encapsulation.
    
- **IPv6**: Provides built-in support for mobile IP with features like larger address space and route optimization.
    
- **MANETs**: Decentralized, self-configuring networks with dynamic topologies and multi-hop communication.
    
- **Routing in MANETs**: Proactive, reactive, hybrid, and geographic routing protocols address the challenges of dynamic networks.


1. **Define Wireless LAN (K1)**
    
    - A Wireless Local Area Network (WLAN) allows communication without physical cables.
    - Uses radio waves for data transmission.
    - Operates within a limited range (e.g., home, office, campus).
    - Supports multiple devices like laptops, smartphones, and tablets.
    - Follows IEEE 802.11 standards (Wi-Fi).
2. **Interpret the Problems while Deploying Wireless Networks (K2)**
    
    - **Interference** from other devices like microwaves and Bluetooth.
    - **Security risks**, such as unauthorized access and hacking.
    - **Limited range**, especially in large buildings with obstacles.
    - **Network congestion** due to multiple connected devices.
    - **Signal degradation** caused by walls and electronic devices.
3. **Identify the Limitations of Piconet (K3)**
    
    - Limited to a **maximum of 7 active slave devices**.
    - Short communication **range** (typically up to 10 meters).
    - Lower **data transfer rate** compared to Wi-Fi.
    - Higher **power consumption** for continuous connections.
    - **Complex network management** in larger setups.
4. **Illustrate the Scatternet (K2)**
    
    - A **scatternet** is formed when multiple Bluetooth **piconets** interconnect.
    - A device can act as a **master in one piconet and a slave in another**.
    - Allows **larger network coverage** than a single piconet.
    - Used in **IoT applications, wireless sensor networks**.
    - Helps in **multi-device communication** without a central hub.
5. **Explain the Different Types of Services Offered by Bluetooth (K2)**
    
    - **File transfer** between Bluetooth-enabled devices.
    - **Wireless audio streaming** (e.g., headphones, speakers).
    - **Device pairing** for data synchronization (e.g., smartwatch to phone).
    - **Hands-free communication** in vehicles.
    - **IoT device communication** (e.g., smart home appliances).
6. **Summarize the Different Types of Services Offered by WLAN (K2)**
    
    - **Internet access** without wired connections.
    - **Wireless file sharing** between devices.
    - **VoIP services** for wireless voice communication.
    - **Streaming multimedia content** over Wi-Fi.
    - **Remote access** to network resources (e.g., printers, storage).
7. **Compare Wi-Fi and WiMAX (K2)**
    
    - **Wi-Fi** is for **short-range**, whereas **WiMAX** covers **long distances**.
    - **Wi-Fi** operates in **2.4 GHz & 5 GHz**, **WiMAX** in **2.3, 2.5, 3.5 GHz**.
    - **Wi-Fi** is commonly used for **home and office networks**, **WiMAX** for **broadband access**.
    - **Wi-Fi** supports **higher speeds (up to 9.6 Gbps in Wi-Fi 6E)**, **WiMAX** is slower.
    - **Wi-Fi** is widely available, **WiMAX** has limited global adoption.
8. **List the Design Goals of WLANs (K1)**
    
    - **Easy deployment** without wired infrastructure.
    - **High-speed connectivity** for multiple devices.
    - **Secure communication** using encryption (WPA, WPA2).
    - **Energy efficiency** for mobile devices.
    - **Seamless roaming** between access points.
9. **What is Wireless Networking? (K1)**
    
    - A network that allows devices to communicate **without physical cables**.
    - Uses **radio waves, infrared, or satellite signals**.
    - Common technologies include **Wi-Fi, Bluetooth, Zigbee**.
    - Supports **mobile and remote access**.
    - Used in **home, office, and public networks**.
10. **What are the Different Features of MAC Protocols? (K1)**
    

- **Channel access control** (CSMA/CA in Wi-Fi).
- **Data packet framing** and addressing.
- **Error detection and correction**.
- **Collision avoidance mechanisms**.
- **QoS (Quality of Service) support** for prioritizing traffic.

11. **What is Meant by Spread Spectrum? (K1)**

- A technique to **spread a signal over a wide bandwidth**.
- Improves **resistance to interference and jamming**.
- Used in **Wi-Fi, Bluetooth, and military communication**.
- Includes **FHSS (Frequency Hopping Spread Spectrum)** and **DSSS (Direct Sequence Spread Spectrum)**.
- Enhances **security and reliability** of wireless networks.

12. **What is Frequency Hopped Spread Spectrum (FHSS)? (K1)**

- A technique where the **signal frequency changes rapidly** over time.
- Reduces **interference** by hopping across multiple frequencies.
- Used in **Bluetooth and early Wi-Fi versions**.
- Improves **security** by making eavesdropping difficult.
- Suitable for **low-bandwidth applications**.

13. **What is Direct Sequence Spread Spectrum (DSSS)? (K1)**

- A method where data is **spread over a wider frequency band**.
- Uses a **chipping sequence** for encoding data.
- Reduces **interference and improves reliability**.
- Used in **Wi-Fi (802.11b) and military communication**.
- Supports **higher data rates than FHSS**.

14. **List the Applications of Infrared (K1)**

- **Remote controls** (TV, AC, projectors).
- **Data transfer** (e.g., old mobile phones with infrared ports).
- **Night vision and thermal imaging** in security.
- **Medical applications** (e.g., infrared thermometers).
- **Wireless sensors** in industrial automation.

15. **List the Various Frequency Bands of Radio Wave (K1)**

- **Very Low Frequency (VLF)** – 3 kHz to 30 kHz.
- **Low Frequency (LF)** – 30 kHz to 300 kHz.
- **Medium Frequency (MF)** – 300 kHz to 3 MHz (AM Radio).
- **High Frequency (HF)** – 3 MHz to 30 MHz (Shortwave radio).
- **Ultra High Frequency (UHF)** – 300 MHz to 3 GHz (Wi-Fi, TV signals).

16. **Define UHF Narrowband (K1)**

- UHF Narrowband operates in **Ultra High Frequency (300 MHz – 3 GHz)**.
- Uses a **narrow channel width (e.g., 12.5 kHz, 25 kHz)**.
- Provides **long-range communication with minimal interference**.
- Used in **public safety, military, and radio broadcasting**.
- Suitable for **low-data-rate applications**.

17. **Draw the Frame Format of IEEE 802.11 Phy Frame using DSSS & FHSS (K2)**  
    _(Diagram required – IEEE 802.11 PHY frame consists of a preamble, header, payload, and CRC.)_
    
18. **Define WATM (K1)**
- **Wireless ATM (WATM)** extends **Asynchronous Transfer Mode (ATM)** over wireless networks.
- Supports **high-speed data, voice, and multimedia services**.
- Uses **fixed-size cells (53 bytes)** for transmission.
- Provides **Quality of Service (QoS)** for real-time applications.
- Used in **early broadband and mobile networks**, now largely obsolete.

19. **List the Applications of LoWPAN (K1)**

- **Smart home automation**.
- **Industrial IoT (IIoT) applications**.
- **Environmental monitoring** (e.g., weather stations).
- **Smart agriculture** (e.g., soil moisture sensors).
- **Healthcare monitoring** (e.g., wearable health sensors).

20. **What are the Characteristics of Zigbee? (K1)**

- **Low power consumption**, ideal for battery-powered devices.
- **Operates in 2.4 GHz, 900 MHz, and 868 MHz** bands.
- **Supports mesh, star, and tree topologies**.
- **Short-range communication (10-100m)**.
- **Used in IoT, smart homes, and industrial automation**.
