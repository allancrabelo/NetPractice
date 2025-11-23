# NetPractice: The Ultimate Guide to IPv4 Networking 

NetPractice is a hands-on networking simulator from 42 designed to turn absolute beginners into mini-network engineers.
If you can make all the green checks appear here, you can configure real networks without blinking.

This project forces you to truly understand IPv4, subnetting, switching, routing, gateways, and basic network logic, not by memorizing theory, but by building actual networks.

---
## 1. IPv4: The Address System of the Internet

IPv4 is the `32-bit` address that identifies a device on a network.
It's composed of four octets `(e.g., 192.168.0.1)¹`

NetPractice focuses exclusively on IPv4 (not IPv6) because it’s still the backbone of most LANs and corporate networks².

## 2. Subnet Masks: Splitting Network and Host Bits

The subnet mask defines which part of an IP is the network and which part identifies the host.
The `/n` notation tells you how many bits belong to the network.

Example:
/24 → first 24 bits are network bits³.

Every subnet generates three critical values:

    - Network Address → first IP of the block
    - Broadcast Address → last IP of the block
    - Usable Hosts → everything in the middle
    - First and last it`s reserved


	0 0 0 0 0 0 0 0 ->	0 
	1 0 0 0 0 0 0 0 ->	128
	1 1 0 0 0 0 0 0 ->	192
	1 1 1 0 0 0 0 0 ->	224
	1 1 1 1 0 0 0 0 ->	240
	1 1 1 1 1 0 0 0 ->	248
	1 1 1 1 1 1 0 0 ->	252
	1 1 1 1 1 1 1 0 ->	254
	1 1 1 1 1 1 1 1 ->	255

| CIDR | SUBNET MASK | WILDCARD MASK | # OF IP ADDRESSES | # OF USABLE IP ADDRESSES |
|------|-------------|---------------|-------------------|-------------------|
| /32 |	255.255.255.255 |	0.0.0.0 |	1	| 1
| /31 |	255.255.255.254 |	0.0.0.1 |	2	| 2
| /30 |	255.255.255.252 |	0.0.0.3 |	4	| 2
| /29 |	255.255.255.248 |	0.0.0.7 |	8	| 6
| /28 |	255.255.255.240 |	0.0.0.15 |	16	| 14
| /27 |	255.255.255.224 |	0.0.0.31 |	32	| 30
| /26 |	255.255.255.192 |	0.0.0.63 |	64 	| 62
| /25 |	255.255.255.128 |	0.0.0.127 |	128 | 126
| /24 |	255.255.255.0 |	0.0.0.255 |	256	| 254
| /23 |	255.255.254.0 |	0.0.1.255 |	512	| 510
| /22 |	255.255.252.0 |	0.0.3.255 |	1,024 |	1,022
| /21 |	255.255.248.0 |	0.0.7.255 |	2,048 |	2,046
| /20 |	255.255.240.0 |	0.0.15.255 |	4,096	| 4,094
| /19 |	255.255.224.0 |	0.0.31.255 |	8,192	| 8,190
| /18 |	255.255.192.0 |	0.0.63.255 |	16,384	| 16,382
| /17 |	255.255.128.0 |	0.0.127.255 |	32,768	| 32,766
| /16 |	255.255.0.0 |	0.0.255.255 |	65,536	| 65,534
| /15 |	255.254.0.0 |	0.1.255.255 |	131,072	| 131,070
| /14 |	255.252.0.0 |	0.3.255.255 |	262,144	| 262,142
| /13 |	255.248.0.0 |	0.7.255.255 |	524,288	| 524,286
| /12 |	255.240.0.0 |	0.15.255.255 |	1,048,576 |	1,048,574
| /11 |	255.224.0.0 |	0.31.255.255 |	2,097,152 |	2,097,150
| /10 |	255.192.0.0 |	0.63.255.255 |	4,194,304 |	4,194,302
| /9 |	255.128.0.0 |	0.127.255.255 |	8,388,608 |	8,388,606
| /8 |	255.0.0.0 |	0.255.255.255 |	16,777,216	|16,777,214
| /7 |	254.0.0.0 |	1.255.255.255 |	33,554,432	|33,554,430
| /6 |	252.0.0.0 |	3.255.255.255 |	67,108,864	|67,108,862
| /5 |	248.0.0.0 |	7.255.255.255 |	134,217,728	|134,217,726
| /4 |	240.0.0.0 |	15.255.255.255 |	268,435,456 |	268,435,454
| /3 |	224.0.0.0 |	31.255.255.255 |	536,870,912 |	536,870,910
| /2 |	192.0.0.0 |	63.255.255.255 |	1,073,741,824 |	1,073,741,822
| /1 |	128.0.0.0 |	127.255.255.255 |	2,147,483,648 |	2,147,483,646
| /0 |	0.0.0.0 |	255.255.255.255 |	4,294,967,296 |	4,294,967,294

These rules are the foundation of NetPractice.

## 3. Subnetting: The Ninja Art of Slicing Networks

`Subnetting` is the process of dividing a large network into smaller logical sub-networks.
This improves:

    - traffic segmentation
    - security
    - scalability
    - routing performance⁴

NetPractice heavily depends on your ability to compute these subnets correctly.

## 4. Switches: Layer 2 Traffic Champions

A `switch` connects devices inside the same network.
It works using `MAC` addresses, not IP addresses⁵.

In NetPractice, any devices connected to the same switch must be in the same `subnet`,
using  `compatible masks`, and have `valid IPs`.

## 5. Routers: The GPS of the Network

A router connects `different networks`.
It examines IPs and decides the next hop using its routing table⁶.

If a router lacks a route to a destination network, packets get dropped\

## 6. Gateways: Your Exit Door

The default gateway is the IP your device uses to leave its own network.
It must:

    - be in the same subnet as the device
    - be the router’s interface that leads to other networks⁷
    
If the gateway is wrong, unreachable, or mismatched → the device is isolated.

## 7. Routing: The Pathfinding Brain of the Network

Routing rules define:

`“To reach network X, send packets to Y.”`

```10.0.2.0/24 → via 10.0.1.1```

NetPractice uses static routing, requiring you to manually configure routes such as:

## 8. Broadcast Address: The “Everyone Listen!” Address

The broadcast address is the final IP of a network block⁸.
Sending packets to this address means all hosts on that subnet receive them.

NetPractice forces you to identify which IPs are broadcasts to avoid invalid assignments.

## 9. Valid vs Invalid IPv4 Addresses

Some IPv4 ranges cannot be assigned to hosts:

🚫 Reserved or Invalid for Hosts

    0.0.0.0 → unspecified
    127.x.x.x → loopback
    224.0.0.0 – 239.x.x.x → multicast
    255.255.255.255 → limited broadcast¹⁰

🔒 Private IP Ranges (Not Routable to the Internet)

As defined by RFC1918⁹:

    10.0.0.0/8
    172.16.0.0/12
    192.168.0.0/16

In NetPractice, these are the most common IP ranges.

## 10. Connecting to the “Internet” in NetPractice

To simulate an internet connection, a device must have:

    A valid IP inside its LAN
    A subnet mask matching its network
    A valid gateway (router’s address)
    A correct routing path out of the LAN

In real life, NAT would be used to map private addresses to a public one, but the NetPractice environment abstracts this. Focusing strictly on IP logic and routing.

# WALKTHROUGH

<details>
  <summary>Level 1</summary>
  <br>
  
<img width="1907" height="941" alt="Level01" src="https://github.com/user-attachments/assets/5ac9826f-23e7-4c50-b19b-34ab5b6c0ae8" />
This is a simple exercise involving a connection using only cables, meaning the devices are on different networks. The subnet masks are already defined, so there is no need to change them. You only need to copy the blocked IP address to the other device and increase the last number by +1.

</details>


<details>
  <summary>Level 2</summary>
  <br>
  
<img width="1907" height="941" alt="Level02" src="https://github.com/user-attachments/assets/25f10e1d-2fab-4675-9592-5932f669f32a" />

On the A–B side, you only need to keep the same subnet mask. Then, copy the blocked IP address to the other device and decrease the last number by –1.

On the C–D side, the subnet mask is /30 (meaning there are very few usable IPs). The IP that was originally configured is not allowed, so I changed it to 42.42.42.254 to use an available IP within a valid subnet. After that, I copied it to the other device and decreased the last number by –1.

</details>

<details>
  <summary>Level 3</summary>
  <br>
  
<img width="1907" height="941" alt="Level03" src="https://github.com/user-attachments/assets/c2ecc151-ffb9-4c0d-b86c-3aebf4e8a633" />

This is a switch exercise, so you need to connect all three PCs. First, look for the blocked subnet mask and apply the same mask to every PC.

Next, check the blocked IP address. Since it uses a /25 mask, there are plenty of available subnets. Simply assign the IP to the first PC, then decrease the last number by –1 for each of the remaining PCs.

</details>

<details>
  <summary>Level 4</summary>
  <br>
  
<img width="1907" height="941" alt="image" src="https://github.com/user-attachments/assets/af0eb219-ffd9-4cac-9742-fefa4858cc1e" />

You need to connect two PCs to a switch, and then connect the switch to the router. Start with the PCs: ignore interface R2, and work only with R1.

Since R1’s subnet mask is blocked, simply copy that same mask to all connections. Because Host A’s IP address is also blocked, take that IP, apply it to each interface, and increase the last number by +1 for each device.

</details>

<details>
  <summary>Level 5</summary>
  <br>
  
<img width="1904" height="952" alt="image" src="https://github.com/user-attachments/assets/cc25e56c-acdb-48e3-aab5-35564a92cef5" />

We are now being introduced to a gateway. Here, we need to make sure that the default gateways point to their correct interfaces.

Start by copying the router’s subnet masks to the corresponding hosts. Then, take the blocked IP addresses, apply them to the appropriate PCs, and reduce the last number by –1 to place each device correctly within the subnet.

</details>


<details>
  <summary>Level 6</summary>
  <br>
  
<img width="1904" height="952" alt="image" src="https://github.com/user-attachments/assets/d0705f34-673a-44d2-8d5e-a4527fcf93f1" />

In this exercise, we need to connect a PC to a switch, the switch to the host, and then connect the entire system to the internet, remembering to set the gateways correctly.

Since the router’s subnet mask was blocked, I copied it to the PC. Then, I took the PC’s IP address, copied it to the router, and decreased the last number by –1 to create the router’s subnet address. This adjusted IP was then assigned as the PC’s gateway.

Next, to connect the system to the internet, we simply copy the system’s IP address and change the subnet to .0/0, which is required for internet connectivity. Finally, we set the gateway to the default.

</details>

<details>
  <summary>Level 7</summary>
  <br>
  
<img width="1904" height="952" alt="Level07" src="https://github.com/user-attachments/assets/7d284ecf-ea4c-49f3-97c8-b0b84429700e" />

We need to connect all the devices, starting from the top where the IP is blocked and moving down. First, copy the blocked IP address to the PC and increase the last octet by 1, then set the gateway. Next, move from one router to the other: copy the blocked IP address to the other router, this time decreasing the last octet by 1, and set the gateway. Finally, assign the last two devices the IP addresses ending in .66 and .67. Set the subnet mask to /26 for all devices so that each one is on a separate network.

</details>

<details>
  <summary>Level 8</summary>
  <br>
  
<img width="1904" height="952" alt="Level8" src="https://github.com/user-attachments/assets/f7cbf732-9be9-4e55-8faf-d0d13e131ad9" />

At the bottom of the connection, there is a blocked subnet mask, which is the same as the one at the top. Set all devices to use the same mask. There is a blocked mask on the gateway, so we copy it to the left and set the subnet to 1, then increase the last octet by 1 for the next device. On the other side, we do the same, but assign .17 and .18 since the mask increments by 16. The next IPs are blocked, so I simply copied the others and set .61, increasing by 1 for the following device. Finally, copy the router’s IP to the internet connection and take the internet IP, keeping only the first octet followed by 0.0.0/8.

</details>

---

### REFERENCES

    ¹ TANENBAUM, Andrew. Computer Networks. 5. ed. Pearson, 2011.
    ² HUSTON, Geoff. “IPv6 – The Hard Parts”. APNIC Blog, 2020.
    ³ RFC 950 — Internet Standard Subnetting Procedure.
    ⁴ STALLINGS, William. Data and Computer Communications. 10. ed.
    ⁵ IEEE. 802.1D – MAC Bridges.
    ⁶ RFC 1812 — Requirements for IP Version 4 Routers.
    ⁷ CISCO Systems. IP Routing Fundamentals, 2016.
    ⁸ RFC 919 — Broadcasting Internet Datagrams.
    ⁹ RFC 1918 — Address Allocation for Private Internets.
    ¹⁰ IANA. Special-Purpose Address Registry.
