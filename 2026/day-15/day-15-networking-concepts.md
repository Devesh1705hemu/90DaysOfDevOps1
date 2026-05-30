# Day 15 – Networking Concepts: DNS, IP, Subnets & Ports

## 🎯 Objective

Build a strong foundation in networking concepts that every DevOps engineer must understand, including DNS, IP addressing, subnetting, CIDR notation, and network ports.

---

# Task 1: DNS – How Names Become IPs

## What Happens When You Type `google.com` in a Browser?

1. The browser asks the DNS resolver for the IP address of `google.com`.
2. DNS servers translate the domain name into an IP address.
3. The browser connects to that IP address using TCP/IP.
4. The web server responds with the requested webpage.

---

## DNS Record Types

### A Record

Maps a domain name to an IPv4 address.

### AAAA Record

Maps a domain name to an IPv6 address.

### CNAME Record

Creates an alias from one domain name to another.

### MX Record

Specifies the mail server responsible for receiving emails.

### NS Record

Identifies the authoritative DNS servers for a domain.

---

## Command

```bash
dig google.com
```

### Sample Output

```bash
;; ANSWER SECTION:
google.com.      300     IN      A       142.250.193.78
```

### Identification

| Field    | Value          |
| -------- | -------------- |
| A Record | 142.250.193.78 |
| TTL      | 300 seconds    |

> Note: Your IP address and TTL may differ depending on location and DNS server.

---

# Task 2: IP Addressing

## What is an IPv4 Address?

An IPv4 address is a 32-bit numerical identifier assigned to devices on a network. It consists of four octets separated by dots.

### Example

```text
192.168.1.10
```

Each octet ranges from 0 to 255.

---

## Public vs Private IP Address

### Public IP

A globally unique IP address reachable from the internet.

Example:

```text
8.8.8.8
```

### Private IP

Used within local networks and not directly accessible from the internet.

Example:

```text
192.168.1.10
```

---

## Private IP Ranges

### Class A

```text
10.0.0.0 - 10.255.255.255
```

### Class B

```text
172.16.0.0 - 172.31.255.255
```

### Class C

```text
192.168.0.0 - 192.168.255.255
```

---

## Command

```bash
ip addr show
```

### Sample Output

```bash
inet 192.168.1.15/24 brd 192.168.1.255 scope global
```

### Private IP Identified

```text
192.168.1.15
```

This belongs to the private range `192.168.x.x`.

---

# Task 3: CIDR & Subnetting

## What Does `/24` Mean?

In `192.168.1.0/24`, the first 24 bits represent the network portion, and the remaining 8 bits represent host addresses.

Subnet Mask:

```text
255.255.255.0
```

---

## Usable Hosts

### /24

```text
256 Total IPs
254 Usable Hosts
```

### /16

```text
65,536 Total IPs
65,534 Usable Hosts
```

### /28

```text
16 Total IPs
14 Usable Hosts
```

---

## Why Do We Subnet?

Subnetting divides large networks into smaller networks.

Benefits:

* Better network organization
* Improved security
* Reduced broadcast traffic
* Efficient IP address utilization

---

## CIDR Table

| CIDR | Subnet Mask     | Total IPs | Usable Hosts |
| ---- | --------------- | --------- | ------------ |
| /24  | 255.255.255.0   | 256       | 254          |
| /16  | 255.255.0.0     | 65,536    | 65,534       |
| /28  | 255.255.255.240 | 16        | 14           |

---

# Task 4: Ports – The Doors to Services

## What is a Port?

A port is a logical communication endpoint used by applications and services.

Ports allow multiple services to run on the same IP address without conflict.

---

## Common Ports

| Port  | Service |
| ----- | ------- |
| 22    | SSH     |
| 80    | HTTP    |
| 443   | HTTPS   |
| 53    | DNS     |
| 3306  | MySQL   |
| 6379  | Redis   |
| 27017 | MongoDB |

---

## Command

```bash
ss -tulpn
```

### Sample Output

```bash
tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 128 0.0.0.0:3306
```

### Service Mapping

| Port | Service        |
| ---- | -------------- |
| 22   | SSH Server     |
| 3306 | MySQL Database |

> Your output may vary depending on installed services.

---

# Task 5: Putting It Together

## Q1. You Run

```bash
curl http://myapp.com:8080
```

### Networking Concepts Involved

1. DNS resolves `myapp.com` into an IP address.
2. The connection is established to port `8080`.
3. TCP/IP networking transfers data between client and server.

---

## Q2. Your App Can't Reach Database at `10.0.1.50:3306`

### What Would You Check First?

1. Verify the database service is running on port `3306`.
2. Check firewall and security group rules.
3. Confirm network connectivity and routing between systems.
4. Ensure the IP address is correct.

---

# Commands Used

## DNS Lookup

```bash
dig google.com
```

### Purpose

Retrieves DNS records for a domain.

---

## Network Interface Information

```bash
ip addr show
```

### Purpose

Displays network interfaces and assigned IP addresses.

---

## View Listening Ports

```bash
ss -tulpn
```

### Purpose

Displays open ports and associated services.

---

# Key Learnings

### 1. DNS Converts Names into IP Addresses

Humans use domain names while computers communicate using IP addresses.

### 2. CIDR and Subnetting Improve Network Management

Subnetting helps organize networks efficiently and reduces unnecessary traffic.

### 3. Ports Allow Multiple Services on One Machine

Services such as SSH, HTTP, MySQL, and Redis communicate through different ports on the same IP address.

---

# Conclusion

Today I learned how DNS resolution works, how IP addresses are structured, the fundamentals of CIDR and subnetting, and how ports enable communication between services. These networking concepts form the foundation of cloud, Linux, and DevOps engineering.

---


#DevOpsEngineer
#CloudComputing
