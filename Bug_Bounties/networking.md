[Home](../README.md)

# Networking
DHCP
	How routers give IP Addresses
Network Address Translation(NAT)
	How the router maps the private IP Addresses to a single public IP address.
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

## Table of Contents
<!-- TOC -->

- [Networking](#networking)
	- [Table of Contents](#table-of-contents)
	- [IP Address](#ip-address)
		- [IP Address Classes](#ip-address-classes)
		- [Private IP Addresses](#private-ip-addresses)
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

### [Private IP Addresses](#table-of-contents)
Private IP Addresses are specific IP Addresses that aren't unique. They

127.0.0.1 - 127.255.255.255 are **loopback address**. These are used to test your network by having your device all itself.

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
