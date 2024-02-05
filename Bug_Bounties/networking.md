[Home](../README.md)

# Networking
DHCP
	How routers give IP Addresses
Ports
Networks
Router
Switcher
Repeater
Firewall
Hosts
TCP/UDP
	- TCP is a 3 way handshake
How is location information tied to your ip address?
How can you get incoming up addresses from a node server?
127.0.0.1
10.0.0.31
192.168.1.1
proxy and VPNs

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
	- [Internet Protocol](#internet-protocol)
	- [Network](#network)
	- [Ports](#ports)

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

## Internet Protocol
## Network

## Ports
| Port Number | Description                               |
|-------------|-------------------------------------------|
| 21          | File transfer protocol(FTP)               |
| 22          | Secure Shell(SSH)                         |
| 25          | Simple Mail Transfer Protocol(SMTP)       |
| 53          | Domain name system(DNS)                   |
| 80          | Hypertext transfer protocol(HTTP)         |
| 443         | Hypertext transfer protocol Secure(HTTPS) |
| 3306        | MySQL                                     |
| 5432        | PostgreSQL                                |
| 27017       | MongoDB                                   |
