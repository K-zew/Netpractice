# Netpractice

## Intoduction

This project is a general practical exercise to let you discover networking.
You will have to configure small-scale networks. To do so, it will be necessary to understand this concepts.

*  [Important concepts](#important-concepts)
    *    [TCP](#tcp)  
    *    [IP address](#ip-address)
    *    [TCP/IP model](#tcp/ip-model)
    *    [Subnet mask](#subnet-mask)
    *    [Switch](#switch)
    *    [Router](#router)

You will have to complete 10 levels :   [Levels](#levels)

## Important Concepts

### TCP

   <br>
      <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/tcp-vs-udp-communications.png?raw=true" alt="TCP">
   <br>

TCP stands for Transmission Control Protocol a communications standard that enables application programs and computing devices to exchange messages over a network. It is designed to send packets across the internet and ensure the successful delivery of data and messages over networks.

TCP organizes data so that it can be transmitted between a server and a client. It guarantees the integrity of the data being communicated over a network. Before it transmits data, TCP establishes a connection between a source and its destination, which it ensures remains live until communication begins. It then breaks large amounts of data into smaller packets, while ensuring data integrity is in place throughout the process, toensures end-to-end data delivery without loss any of data.

HOW send data :
As we know in TCP protocol, for the first time, it tries to sent one packet to the destination, and check if the packet is well received by ensuring the connection remains live. Each time, it adds a packet to be sent, meaning that for the second time, it sends the double of packets sent before, and checks if the connection remains good. For the third time, it adds the double of the previous number of packets of the previous one, until a problem occurred in this connection. At this moment, it goes back the previous number of packets sent in order to keep this connection for an end-to-end data delivery of data, to Increase the transmitter speed and maintain accuracy. We can clarify this process with a simple mathematical formulate, which is: `2^(n)`. Where n is the number of times to send the packet in this connection correctly.

As a result, high-level protocols that need to transmit data all use TCP Protocol.Examples include peer-to-peer sharing methods like File Transfer Protocol (FTP), Secure Shell (SSH)...

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### IP Address

   <br>
      <p align="center">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/IP_addressing.jpeg?raw=true" alt="IP">
      </p>
   </br>

IP is part of an internet protocol suite, which also includes the transmission control protocol. Together, these two are known as TCP/IP. The internet protocol suite governs rules for packetizing, addressing, transmitting, routing, and receiving data over networks.

IP addressing is a logical means of assigning addresses to devices on a network. Each device connected to the internet requires a unique IP address.

An IP address has two parts; one part identifies the host such as a computer or other device, and the other part identifies the network it belongs to. TCP/IP uses a [subnet mask](#subnet-mask) to separate them.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### TCP/IP model

   <br>
      <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/tcp_ip_model.png?raw=true" alt="tcp_ip_model">
   </br>
   
   * Explained :
   
   <br>
      <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/tcp_ip.png?raw=true" alt="tcp_ip">
   </br>

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### IPv4 vs IPv6

IP addresses come in 2 versions--IPv4 and IPv6:

   <br>
      <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/IPv4-vs-IPv6-FR.png?raw=true" alt="IPv4 vs IPv6">
   </br>

Internet Protocol version 4 (IPv4) defines an IP address as a 32-bit number. However, because of the growth of the Internet and the depletion of available IPv4 addresses, a new version of IP (IPv6), using 128 bits for the IP address, was standardized in 1998. However, only IPv4 addresses are used in NetPractice.


- Public Address vs. Private Address
A public IP address is an IP address that can be accessed directly over the internet and is assigned to your network router by your internet service provider (ISP). A public (or external) IP address helps you connect to the internet from inside your network, to outside your network.

A private IP address is the address your network router assigns to your device. Each device within the same network is assigned a unique private IP address (sometimes called a private network address) — this is how devices on the same internal network talk to each other.

When a network is connected to the internet, it cannot use an IP address from the reserved private IP addresses. The following ranges are reserved for private IP addresses:

```
192.168.0.0 – 192.168.255.255 (65,536 IP addresses)
172.16.0.0 – 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 – 10.255.255.255     (16,777,216 IP addresses)
```
<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

# Subnet Mask

   <br>
      <p align="center">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/subent_mask.png?raw=true" alt="subnet mask">
      </p>   
   </br>

A subnet mask is a 32 bits (4 bytes) address used to distinguish between a network address and a host address in the IP address. It defines the range of IP addresses that can be used within a network or a subnet.


- Finding the network address
The Interface A1 above has the following properties:
```
IP address | 104.198.241.125
Mask       | 255.255.255.128  
```
To determine which portion of the IP address is the network address, we need to apply the mask to the IP address. Let's first convert the mask to its binary form:
```
Mask | 11111111.11111111.11111111.10000000
```
The bits of a mask that are 1 represent the network address, while the remaining bits of a mask that are 0 represent the host address. Let's now convert the IP address to its binary form:
```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```
We can now apply the mask to the IP address through a bitwise AND to find the network address of the IP:
```
Network address | 01101000.11000110.11110001.00000000
```
Which translates to a network address of `104.198.241.0`.


- Finding the range of host addresses
To determine what host addresses we can use on our network, we have to use the bits of our IP address dedicated to the host address. Let's use our previous IP address and mask:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```
The possible range of our host addresses are expressed through the last 7 bits of the mask which are all 0. Therefore, the range of host addresses is:
```
BINARY  | 0000000 - 1111111
DECIMAL | 0 - 127
```
To get the range of possible IP addresses for our network, we add the range of host address to the network address. Our range of possible IP addresses becomes `104.198.241.0 - 104.198.241.127`.

HOWEVER, the extremities of the range are reserved for specific uses and cannot be given to an interface:
```
104.198.241.0   | Reserved to represent the network address.
104.198.241.127 | Reserved as the broadcast address; used to send packets to all hosts of a network.
```
Therefore, our real IP range becomes `104.198.241.1 - 104.198.241.126`, which could have been found using an IP calculator.

* CIDR Notation (/24)
The mask can also be represented with the Classless Inter-Domain Routing (CIDR). This form represents the mask as a slash "/", followed by the number of bits that serve as the network address.

Therefore, the mask in the example above of `255.255.255.128`, is equivalent to a mask of /25 using the CIDR notation, since 25 bits out of 32 bits represent the network address.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### Switch

   <br>
      <p align="left">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/switch real.webp?raw=true" alt="switch">
      </p>
      <p align="right">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/switch.webp?raw=true" alt="switch">
      </p>
   <br>

A switch connects multiple devices together in a single network. Unlike a router, the switch does not have any interfaces since it only distibutes packets to its local network, and cannot talk directly to a network outside of its own.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### Router

   <br>
      <p align="left">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/router.jpg?raw=true" alt="router">
      </p>
   <br>

Just as the switch connects multiple devices on a single network, the router connects multiple networks together. The router has an interface for each network it connects to.

Since the router separates different networks, the range of possible IP addresses on one of its interface must not overlap with the range of its other interfaces. An overlap in the IP address range would imply that the interfaces are on the same network.
 <br>
      <p align="right">
         <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/router.png?raw=true" alt="router">
      </p>
</br>

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

### Routing Table

   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/Imgs/routing_table.png?raw=true" alt="routing_table">
   <br>
   
A routing table is a data table stored in a router or a network host that lists the routes to particular network destinations. In NetPractice, the routing table consists of 2 elements:

Destination: The destination specifies a network address on which a host is the end target of the packets. The route of default or 0.0.0.0/0, is the route that takes effect when no other route is available for an IP destination address. The default route will use the next-hop address to send the packets on their way without giving a specific destination. The default route will match any network.

Next hop: The next hop refers to the next closest router a packet can go through. It is the IP address of the next router on the packet's way. Every single router maintains its routing table with a next hop address.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>

## Levels

<details>
 <summary>Level 1</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level1/level1.png?raw=true" alt="level1">
   <br>
   <br>
   
   **Interface A1.** Since *Client A* and *Client B* are on the same network, their IP address must represent the same network in accordance to the subnet mask.
<br>
The subnet mask is `255.255.255.0`, which means that the first 3 bytes of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
<br>
The solution will be anything in the range of **104.96.23.0 - 104.96.23.255** excluding the following 3:
* **104.96.23.0:** The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
* **104.96.23.255:** The last number in the range of hosts (255 in this case) represents the broadcast address.
* **104.96.23.12:** This address is already used by the host *Client B*.

**Inreface D1.** Same reasoning as *1.*, however the subnet mask is *255.255.0.0* in this case. The first 2 bytes of the IP address will represent the network; and the last 2 bytes, the host address.
<br>
The solution will be anything in the range of **211.191.0.0 - 211.191.255.255**, excluding:
* **211.191.0.0:** Represents the network address.
* **211.191.255.255:** Represents the broadcast address.
* **211.191.89.75:** Already taken by host *Client C*.
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 2</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level2/level2.png?raw=true" alt="level2">
   <br>
   <br>
   
   **Interface B1.** Since *Client B* is on the same private network as *Client A*, they should have the exact same subnet mask.
<br>
The solution can only be `255.255.255.224`.

**Interface A1.** To understand the subnet mask of `255.255.255.224`, let's look at it in binary form, along with the IP `192.168.56.222` of *Client B*:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000110.00010000.00111000.11011110
```
</center>
As we can see, the first 27 bits represent the IP address, while only the last 5 bits represent the host address.
<br>
All these 27 bits representing the network must stay the same in the IP addresses of hosts on the same network. To get the answer, we can only change the last (5 bits = 32 | 32-2 =  30).
<br>
<br>
The answer is in the range of:

```
BIN:  11000000.10101000.00111000.11000000 - 11000000.10101000.00111000.11011111
or
DEC:  192.168.56.192 - 192.168.56.223
```
because `192.168.56.222` in the range .

Excluding:
<br>
* **11000000.10101000.00111000.11000000:** Represents the network address (notice all 0 in the last 5 bits).
* **11000000.10101000.00111000.11011111:** Represents the broadcast address (notice all 1 in the last 5 bits).
* **11000000.10101000.00111000.11011110:** *Client B* already has that address.

**Inreface D1/C1.** Here we are introduced to the slash "/" notation for the subnet mask on *Interface D1*. A subnet mask of */30* means that the first 30 bits of the IP address represent the network address, and the remaining 2 bits represent the host address:
<center>

```
Mask /30: 11111111.11111111.11111111.11111100
```
</center>

We can see that this binary number corresponds to the decimal `255.255.255.252`, therefore it is identical to the mask found on *Interface C1*.
<br>
<br>
The answers can then be any addresses, as long as they meet the following conditions:
* The network address (first 30 bits) must be identical for *Client D* and *Client C*.
* The host bits (last 2 bits) cannot be all 1, nor all 0.
* *Client D* and *Client C* do not have identical IP addresses.
   
```
like 1.1.0.1 and 1.1.0.2
 or  1.1.0.253 and 1.1.0.254 ..... 
```
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 3</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level3/level3.png?raw=true" alt="level3">
   <br>
   <br>
   
   
  This exercise introduces the use of the **switch** (*Switch S* in this example). The switch links multiple hosts of the same network together.
  <br>
  <br>

 *Client A*, *Client B*, and *Client C* are all on the same network. Therefore, they must all have the same subnet mask. Since *Client C* already has the mask *255.255.255.128*, the mask for *Interface B1* and for *Interface A1* will also be `255.255.255.128` (or in slash notation: `/25`).
  <br>
  <br>
  The IP address of *Interface B1* and *Interface C1* must be on the same network range as the IP of *Client A*. This range is:
  <center>

  ```
  104.198.52.0 - 104.198.52.128
  because of Interface 104.198.52.125 in tehe range .
  ```
  </center>
  Excluding of course the network address and the broadcast address.

   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 4</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level4/level4.png?raw=true" alt="level4">
   <br>
   <br>
   
  This exercise introduces the **router**. The router is used to link multiple networks together. It does so with the use of multiple interfaces (*Interface R1*, *Interface R2*, and *Interface R3* in this example).
  <br>
  <br>

   Since none of the masks on *Interface B1*, *Interface A1*, and *Interface R1* are entered, we are free to chose our own subnet mask. A mask of **/24** is ideal as it leaves us with the entire 8th byte for the host address, and does not require binary calculations to find the range of possible host addresses.
  <br>
  <br>
  The IP address of *Interface B1* and *Interface R1* must have the same network address as the IP address of *Interface A1*. With a subnet of */24*, the possible range is:
  <center>

  ```
  85.17.5.0 - 85.17.5.255
  ```
  </center>
  Excluding the network address and the broadcast address.
  <br>
  <br>

  Note that we did not interact with the router *Interface R2* and *Interface R3*, since none of our communications had to reach these sides of the router.

  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 5</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level5/level5.png?raw=true" alt="level5">
   <br>
   <br>
   
   This level introduces **routes**. A route contains 2 fields, the first one is the **destination** of outbound packets, the second one is the **next hop** of the packets.
  The **destination** `default` is equivalent to `0.0.0.0/0`, which will send the packets undiscriminately to the first network address it encounters
  The **next hop** is the IP address of the next  router (or internet) interface to which the interface of the current machine must send its packets. 

    *Client A* only has 1 route through which it can send its packets. There is no use specifying a numbered destination. The destination *default* will send the packets to the only path available.
  <br>
  <br>
  The next hop address must be the IP address of the next router's interface on the packets' way. The next interface is *Interface R1*, with the IP address of `71.199.10.126`. Note that the next interface is not *Interface A1*, since this is the sender's own interface.
   
  *Client B* only has 1 route through which it can send its packets. There is no use specifying a numbered destination. The destination *default* will send the packets to the only path available.
  <br>
  <br>
  The next hop address must be the IP address of the next router's interface on the packets' way. The next interface is *Interface R2*, with the IP address of `133.185.132.254`. Note that the next interface is not *Interface A1*, since this is the sender's own interface.
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 6</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level6/level6.png?raw=true" alt="level6">
   <br>
   <br>
   This level introduces the **internet**. The internet behaves like a router. However, if an interface is connected directly or indirectly to the internet, it **cannot** have an IP address in the following reserved private IP ranges:


  ```
  192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
  172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
  10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
  ```
  **Internet.** The **next hop** of the internet is already entered, and matches the IP address of the *Interface R2*. Therefore we only need to bother with the destination of the internet.
  <br>
  <br>
  The internet must send its packets to *Client A*. To do so, the internet's destination must match the network address of *Client A*. Let's find the network address of *Client A*:
  <br>
  *Client A*'s mask is `255.255.255.128`, which is equivalent to `/25`. This means that the first 25 bits of its IP address is its network address. We know then that the first 3 bytes (24 bits) of its IP address makes part of its network address:
  <center>
 If we convert the number 227 to binary, we get ``11100011``. The first digit, which corresponds to the 25th bit, is a 1. Since only the 25th bit is part of the network address and not the remaining 7 bits, we get ``10000000`` for the last byte of the network address, which is 128 in decimal.
  <br>
  <br>
  The full network address is:
  <center>

  ```
  104.124.215.128
  ```
  </center>

  With a range of ``104.124.215.129 - 104.124.255`` or its host addresses.
  <br>
  <br>
  We can now put this address of `104.124.215.128`in the Internet destination. The `25` following the destination address represents the mask applied to its address.
  <br>
  <br>
  A destination of `104.124.215.227/25` is equivalent to the destination address *104.124.215.128/25*, since the mask of */25* will turn all the bits after the 25th to 0 to get the destination's network address.

  ```
  104.124.215.?
  ```
  </center>

  We now only need to find out if the 25th bit is a 1 or a 0.
  <br>
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 7</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level7/level7.png?raw=true" alt="level7">
   <br>
   <br>
   
   This level introduces the concept of **overlaps**. The range of IP addresses of a network must not overlap the range of IP addresses of a separate network. Networks are separated by routers.
  <br>
  <br>

 We have 3 separate networks:
  <br>

  1. Between *Client A* and *Router R1* (Interface R11).
  2. Between *Router R1* (Interface R12) and *Router R2* (Interface R21).
  3. Between *Router R2* (Interface R22) and *Client C*.

  For *Interface A1*, we cannot chose our IP address freely since the IP of *Interface R11* is already entered. Also, if we give it a mask of */24*, the IP address range will overlap with the range of *Interface R12*, which is already entered. They would both be in the range of ``90.198.14.0 - 90.198.14.255``.
  <br>
  <br>
  Since we need addresses for 3 separate networks, it is convenient to split the last bytes of the address in 4 or more address ranges. We do this by using the mask of `/26` or higher. The mask of */28* for example will give us 16 ranges, from which we use the following 3:
  ```
  90.198.14.1 - 90.198.14.14    (Client A to Router R1)
  90.198.14.65 - 90.198.14.78   (Router R1 to Router R2)
  90.198.14.241 - 90.198.14.254 (Router R2 to Client C)
  ```

  To calculate the possible ranges of a mask:
  <br>
  [https://www.calculator.net/bandwidth-calculator.html](https://www.calculator.net/ip-subnet-calculator.html?c6subnet=64&c6ip=2001%3Adb8%3A85a3%3A%3A8a2e%3A370%3A7334&ctype=ipv6&printit=0&x=69&y=28#ipv6)
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 8</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level8/level8.png?raw=true" alt="level8">
   <br>
   <br>
   
   
  **Internet.** The hosts *Client C* and *Client D* will send packets to the internet, then the internet will respond by sending packets all the way back to the initial sender. To send these packets, the internet uses the destination *139.84.118.0/26* to send the packets to the networks in the range of ``139.84.118.17.1 - 139.84.118.17.63``.
  <br>
  <br>
  All the receiving networks must be in this range, without overlapping each other.
  <br>
  <br>

  **Router R2.** On *Interface R23* and *Interface R22* we use the mask `255.255.255.240` (or */28*), to conveniently split the range of */26* from the destination address, into 4 separate ranges. This separation of 4 is necessary since we have the following 3 networks that must not overlap:
  <br>

  1. *Router R1* (router R13) to *Router R2* (router R21).
  2. *Router R2* (router R22) to *Client C*.
  3. *Router R2* (router R23) to *Client D*.

  Each of these networks can then be attributed one of the following IP range with a mask of */28*:
  ```
  139.84.118.0 - 139.84.118.15
  139.84.118.16 - 139.84.118.31
  139.84.118.32 - 139.84.118.47
  139.84.118.48 - 139.84.118.63
  ```
  Note that the network address (first) and the broadcast address (last) must be excluded from each range.
  <br>
  <br>

**Router R1** The destination and next hop for the internet is already entered. We only need to enter the next hop for the *Router R2*, which is the IP on the *Interface R21*.
   ```
   139.84.118.61
   ```
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 9</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level9/level9.png?raw=true" alt="level9">
   <br>
   <br>
   
    This level is quite straight-forward since the internet does not initially send its packets to a specific network. Therefore, the separate networks do not need to share a common address range. I would suggest to simply follow the 6 goals of the level one by one until the level is completed.
  <br>
  <br>
  Remember not to use the network addresses from the reserved private IP ranges.
  <br>
  <br>

  **1** **Goal 3** states that we must connect *meson* with the *internet*. The *internet* will then have to respond to *meson*, so we enter *meson's* network address in the *internet's* destination.
  <br>
  <br>
  **Goal 6** states that we must connect *cation* with the *internet*, so we enter *cation's* network address in the *internet's* destination.
  <br>
  <br>
  It is normal to have an empty field for the 3rd destination of the *internet*, and in *Router R1's* destination. Not all fields of the routing tables need to be filled.]
   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>

---

<details>
 <summary>Level 10</summary>
   <br>
   <img src="https://github.com/K-zew/Netpractice/blob/main/level10/level10.png?raw=true" alt="level10">
   <br>
   <br>
   In this level, there are 4 different networks:
  <br>

  1. *Router R1* (router R11) to *Switch S1*
  2. *Router R1* (router R13) to *Router R2* (router R21)
  3. *Router R2* (router R23) to *Client H4*
  4. *Router R2* (router R22) to *Client H3*
  <br>

  **Internet.** The internet must be able to send its packets to all the hosts, so its destination must cover the range of networks of all the hosts.
  <br>
  <br>
  *Interface R11* and *Interface R13* already have an IP adress entered. This IP address only differs in its last byte. *Interface R11* has for last byte **1**, and *Interface R13* has for last byte **254**. To cover this wide range to IP addresses, we take a mask of **/24** for the *internet's* destination. This destination will cover a range of ``170.235.26.0 - 170.235.26.255``.
  <br>
  <br>

  **Important.** When chosing the IP addresses, we must make sure of 2 things:
  <br>

  1. The IP address is covered by the *internet* destination.
  2. The IP address range of the various networks do not overlap.
  <br>
  
  With the IP addresses already entered (greyed out), let's examine the ranges covered by the various networks:
  <br>

  1. *Router R1* (router R11) to *Switch S1* - Covers the range ``170.235.26.0 - 170.235.26.127`` (mask /25).
  2. *Router R2* (router R23) to *Client H4* - Covers the range ``170.235.26.128 - 170.235.26.191`` (mask /26).
  3. *Router R1* (router R13) to *Router R2* (router R21) - Covers the range ``170.235.26.252 - 170.235.26.255`` (mask /30).
  4. *Router R2* (router R22) to *Client H3* - ??? (mask ???).

  The only IP addresses left for the network "Router R2 to Client H3" are ``170.235.26.192 - 170.235.26.251``. We can pick any mask that will let us take 2 IP addresses from that range to put in *Interface R22* and *Interface R31*.

   
  <div align="right">
   <b><a href="#top">↥ back to top</a></b>
</div>
</br>
</details>
