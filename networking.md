[Home](../README.md)

# Networking
Explaining how the internet works.

## Table of Contents
<!-- TOC -->

- [Networking](#networking)
	- [Table of Contents](#table-of-contents)
	- [IP Address](#ip-address)
		- [IP Address Classes](#ip-address-classes)
		- [RFC1918](#rfc1918)
			- [Private IP Addresses](#private-ip-addresses)
			- [NAT](#nat)
		- [IPv6](#ipv6)
	- [Ports](#ports)
	- [TCP and UDP](#tcp-and-udp)
	- [Modem, Router, Switch, and Repeater](#modem-router-switch-and-repeater)
	- [MAC Address](#mac-address)
	- [Forward proxy, reverse proxy, and VPNs](#forward-proxy-reverse-proxy-and-vpns)

<!-- /TOC -->

## [IP Address](#table-of-contents)
IP Addresses are unique address that allow a device to communicate using Internet Protocol.

IP Addresses are composed of 4 octets which are separated by periods. Each octet can range from a value of 0 to 255.

The **Subnet Mask/Netmask/Mask** is used to identify which IP Addresses are part of the same network or not.

Ex:
 IP Address: 192.168.1.204
Subnet Mask: 255.255.255.0

This means that any IP Addresses starting with 192.168.1 are part of your local network. If an IP Address isn't part of your local network then you have to talk to your router in order to connect to that IP Address.

The **Default gateway/Router/Default Router** is the IP Address of your router. Your device communicates with this IP Address in order to access IP Addresses that aren't in your local network.

In your local network there are always 2 IP Addresses that have custom purposes.
**Network Address** which is the first IP Address in your network. This is used to help other devices identify the network.
Ex: 192.168.1.0
**Broadcast Address** which is the last IP Address in your network. When this IP Address gets something it tells every other IP Address on its local network.
Ex: 192.168.1.255

### [IP Address Classes](#table-of-contents)

| Class | Range                       | Default Subnet Mask | CIDR | Description                    |
|-------|-----------------------------|---------------------|------|--------------------------------|
| A     | 1.0.0.0 - 126.255.255.255   | 255.0.0.0           | /8   | Large companies                |
| B     | 128.0.0.0 - 191.255.0.0     | 255.255.0.0         | /16  | Medium companies               |
| C     | 192.0.0.0 - 223.255.255.0   | 255.255.255.0       | /24  | ISP and most people            |
| D     | 224.0.0.0 - 239.255.255.255 |                     |      | Used for multicasting          |
| E     | 240.0.0.0 - 255.255.255.255 |                     |      | Used for experimental features |
- **CIDR notation** is just a different notation for different subnet masks

Local networks with class A IP Addresses can have 2^(8*3) different devices with their own IP Addresses. These are often reserved for large companies.
- These companies often change the default subnet mask into a smaller one to allow for more local networks. These are called **classless networks**. Ex: 255.0.0.0 could be changed to 255.255.255.0
- **Classful networks** are networks that keep the default subnet mask.

127.0.0.1 - 127.255.255.255 are **loopback address**. These are used to test your network by having your device call itself.
- 127.0.0.1 is often used to refer to your local devices

- Domain Name Server(**DNS**) is the server which converts URLs to IP Addresses.
- Dynamic Host Configuration Protocol(**DHCP**) is how a router assigns it's devices an IP Address, Subnet mask, default gateway, and DNS IP address.

### [RFC1918](#table-of-contents)
RFC1918 was a standard in order to not run out of IP Addresses. It introduced Private IP Addresses and NAT.

#### [Private IP Addresses](#table-of-contents)
Private IP Addresses are specific IP Addresses that aren't unique. They can be used by multiple devices, but because of that they cannot communicate directly with public IP Addresses(cannot directly connect to the internet).

| Class | IP Range                      | Default subnet mask | CIDR |
|-------|-------------------------------|---------------------|------|
| A     | 10.0.0.0 - 10.255.255.255     | 255.0.0.0           | /8   |
| B     | 172.16.0.0 - 172.31.255.255   | 255.255.0.0         | /16  |
| C     | 192.168.0.0 - 192.168.255.255 | 255.255.255.0       | /24  |

#### [NAT](#table-of-contents)
Network Address Translation(NAT) is used by the router to convert your device's private IP Address to a public IP Address which can be used on the internet.

Your router is given a public IP Address by your ISP.

### [IPv6](#table-of-contents)
2^128 different addresses.

Often mobile devices, not connected to wifi, have IPv6 addresses.

## Ports
The IP Address determines the device while the port determines which service or program on that server is to be used.

Each IP Address can have a port from 0 to 65535

| Port Number | Description                               |
|-------------|-------------------------------------------|
| 21          | File transfer protocol(FTP)               |
| 22          | Secure Shell(SSH)                         |
| 25          | Simple Mail Transfer Protocol(SMTP)       |
| 53          | Domain name system(DNS)                   |
| 80          | Hypertext transfer protocol(HTTP)         |
| 443         | Hypertext transfer protocol Secure(HTTPS) |
| 1102        | Adobe Server                              |
| 1416        | Microsoft SQL Server                      |
| 1527        | Oracle Server                             |
| 3306        | MySQL                                     |
| 5432        | PostgreSQL                                |
| 27017       | MongoDB                                   |

| Port range    | Description                                                                 | Used by server or client |
|---------------|-----------------------------------------------------------------------------|--------------------------|
| 0 - 1023      | System or well-known ports                                                  | Server                   |
| 1024 - 49151  | User or Registered ports. These can be registered for a particular service. | Server                   |
| 49152 - 65535 | Dynamic or Private ports.                                                   | Client                   |

Your computer temporarily assigns itself a private port during a session like when browsing the web.

A **socket** is a program that handles incoming and outgoing request on a specific IP address and port.

**Port forwarding** allows public access to sockets on a local network. It redirects network traffic from a port on a router's public IP address ot a corresponding port on a device withing the local network.
- If you want to host a website on your local computer you need to port forward ports 80 and 443 to your server's port.

## [TCP and UDP](#table-of-contents)
Transmission control protocol(**TCP**) is used when the communication between 2 computers needs to guarantee
- the data is in order
- all the data is received

TCP establishes a connection first with a 3 way handshake.

```
Computer 1                    Computer 2
           -> SYN     ->
					 <- SYN ACK <-
					 -> ACK Received ->
```

User Datagram Protocol(**UDP**)
- doesn't establish a connection
- doesn't guarantee data delivery. Some data maybe lost.
- doesn't guarantee the order of the data received
- Is faster than TCP

## [Modem, Router, Switch, and Repeater](#table-of-contents)
**Modem** Converts digital signals(used by computer and router) to analog signals(sometimes used to connect to your ISP) and vice versa	.
- If you don't have any other devices in your local network you can often connect your one device to the modem.

**Router** given a public IP Address by your ISP and assigns private IP Addresses to each device in your local network.
- Not all routers have a separate modem.

A **Switch** is used for communication on a local network. It knows each devices mac address and moves any communication it gets to its corresponding mac address.

## [MAC Address](#table-of-contents)
All devices which connect to the internet(has a network interface card) have a unique Media Access Control(MAC) Address.

An IP Address is used to local a device while a MAC address is used to identify a device.
- IP Address can change for the device, but the MAC address cannot.

## [Forward proxy, reverse proxy, and VPNs](#table-of-contents)

A **forward proxy server** regulates traffic going out of a network. It is used to protect clients.
- Privacy and change location
	- Instead of using the device's IP Address all traffic is routed through the proxy server's IP Address. If the proxy server's IP Address is located in a different area, when you access sites they may think you are in that different area.
- Speed and saves internet bandwidth
	- Proxy servers can cache static assets and static websites.
- Activity logging and blocking certain websites
	- Proxy servers can be set up to document what websites the clients are going to and block certain websites.

A Virtual Private Network(**VPN**) is like a forward proxy server, but it encrypts data that is sent over the internet and often has some guarantees of no activity logging.

A **reverse proxy server** regulates traffic going into a network. It is used to protect servers. A reverse proxy server is often used as a single point of entry for websites.
- Balance traffic to different servers.
- Can cache images and static sites to prevent too many unnecessary request to the servers.
- Defend against DDOS attacks by handling a lot of requests and filter out non legitimate users before they request anything from the server.