# DHCP Server Practice using Vagrant 

## Overview

This repository contains a DHCP practice setup where a DHCP server and two clients (c1 and c2) are configured. The practice involves setting up a Linux-based DHCP server and verifying client configurations, including assigning dynamic and static IP addresses based on the client's MAC address.

## Objective

The main goal of this exercise is to configure a DHCP server on a Linux machine and ensure that two clients are able to automatically obtain their IP configurations from the server. Additionally, client `c2` will have a fixed IP address based on its MAC address.

## Setup Details

### 1. DHCP Server Configuration

- **Operating System**: Linux (Virtual Machine) debian bookworm64 based
- **Network Interfaces**:
  - Interface 1: Private host-only network `192.168.56.0/24` with IP `192.168.56.10`.
  - Interface 2: Internal network `192.168.57.0/24` with IP `192.168.57.10`.
  
- **DHCP Service Installation**: 
  - Ensure the DHCP service is installed and configured to listen on the `192.168.57.0/24` interface.
  
- **DHCP Configuration**:
  - Dynamic IP Range: `192.168.57.25 - 192.168.57.50`
  - Lease Time: Default 1 day, Max 8 days
  - Gateway: `192.168.57.10`
  - DNS Servers: `8.8.8.8`, `4.4.4.4`
  - Domain Name: `micasa.es`

### 2. Client Configuration

- **Client 1 (client1)**:
  - Configured to dynamically obtain an IP address from the DHCP server.
  
- **Client 2 (client2)**:
  - Configured to always obtain a static IP (`192.168.57.4`) based on its MAC address.
  - Lease Time: 1 hour
  - DNS Server: `1.1.1.1`

### 3. Verification

- Use commands such as `ip a`, `ifup`, `ifdown`, and `dhclient` to verify the network configurations obtained by the clients.
- Check the DHCP server logs (`/var/log/syslog`) to ensure the correct DHCP messages are exchanged.
- View the list of active leases in `/var/lib/dhcp/dhcpd.leases`.

### Useful Commands

- **Restart DHCP Service**:
  ```bash
  sudo systemctl restart isc-dhcp-server.service
  ```
- **Check DHCP Configuration Syntax**:
  ```bash
  sudo dhcpd -t
  ```
- **View DHCP Logs**:
  ```bash
  sudo cat /var/log/syslog | grep dhcpd
  ```
- **Check Service Status**:
  ```bash
  sudo systemctl status isc-dhcp-server.service
  ```

## Conclusion

This practice demonstrates how to configure a Linux DHCP server and ensure clients receive dynamic or static IP configurations. By following this setup, you can gain a deeper understanding of how DHCP works in a network environment.
