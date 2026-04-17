# SDN Broadcast Traffic Control - Orange Problem

## Project Overview
This project implements an SDN-based solution using **Mininet** and the **POX controller**.  
The objective is to manage network efficiency by detecting broadcast traffic and implementing selective forwarding to limit unnecessary flooding.

### Core Features
- **Controller-Switch Interaction:** Uses OpenFlow 1.0 to manage switch behavior  
- **Broadcast Detection:** Identifies `ff:ff:ff:ff:ff:ff` traffic and logs occurrences  
- **Selective Forwarding:** Learns MAC addresses and installs flow rules for unicast traffic to reduce switch-to-controller overhead  

---

## 1. Problem Understanding & Setup
The network utilizes a single-switch topology (`s1`) with three hosts (`h1`, `h2`, `h3`).  
The POX controller handles `packet_in` events and dynamically updates the switch flow table.

### Controller-Switch Connection
![Controller Switch Connection](./images/ss1.png)

*Shows POX starting up and "Switch 1 connected"*# SDN Broadcast Traffic Control - Orange Problem

## Project Overview
This project implements an SDN-based solution using **Mininet** and the **POX controller**.  
The objective is to manage network efficiency by detecting broadcast traffic and implementing selective forwarding to limit unnecessary flooding.

### Core Features
- **Controller-Switch Interaction:** Uses OpenFlow 1.0 to manage switch behavior  
- **Broadcast Detection:** Identifies `ff:ff:ff:ff:ff:ff` traffic and logs occurrences  
- **Selective Forwarding:** Learns MAC addresses and installs flow rules for unicast traffic to reduce switch-to-controller overhead  

---

## 1. Problem Understanding & Setup
The network utilizes a single-switch topology (`s1`) with three hosts (`h1`, `h2`, `h3`).  
The POX controller handles `packet_in` events and dynamically updates the switch flow table.

### Controller-Switch Connection
![Controller Switch Connection](./images/ss1.png)

*Shows POX starting up and "Switch 1 connected"*

---


## 2. SDN Logic & Implementation
The controller logic performs the following:

1. **Packet Parsing:** Extracts source and destination MAC addresses  
2. **MAC Learning:** Maps source MACs to ingress ports  
3. **Traffic Control:**
   - If destination is **Broadcast**, logs and floods  
   - If destination is **Known Unicast**, installs flow rule  

### Broadcast Detection
![Broadcast Detection](./images/ss4.png)

*Shows log: BROADCAST DETECTED from 00:00:00:00:00:01*

---

## 3. Flow Rule Design (Match-Action)
Using `ovs-ofctl dump-flows`, we verify that flow rules are installed in the switch.  
This reduces controller overhead and improves efficiency.

### Flow Table Entries
![Flow Rules](images/ss7.png)

*Shows entries like dl_dst=00:00:00:00:00:02*

---

## 4. Performance Observation & Analysis
Performance tested using `iperf` between `h1` and `h2`.

- **Metric:** Throughput (TCP Bandwidth)  
- **Result:** ~91.2 Gbits/sec  

### Iperf Result
![Iperf Result](./images/ss8.png)

*Shows: 106 GBytes 91.2 Gbits/sec*

---

## 5. Execution Steps
1. Clone the repository:
   ```bash
   git clone <your-repo-link>

---