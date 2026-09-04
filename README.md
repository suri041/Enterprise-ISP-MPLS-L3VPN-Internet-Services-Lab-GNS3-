# Enterprise ISP MPLS L3VPN & Internet Services Lab — GNS3

## Overview

This project demonstrates an enterprise ISP network built using GNS3, providing MPLS Layer 3 VPN (L3VPN) and Internet Leased Line (ILL) services.

## Services

- MPLS L3VPN
- Internet / ILL
- Customer VPN isolation
- End-to-end customer connectivity

## Technologies Used

- Cisco IOS
- GNS3
- OSPF
- MPLS
- LDP
- BGP
- MP-BGP VPNv4
- VRF

## Network Architecture

The network consists of:

- P1 and P2 — ISP Core Routers
- PE1 and PE2 — Provider Edge Routers
- CE1 and CE2 — Customer Edge Routers
- Internet Router — Internet / ILL connectivity

## Routing & Services

### OSPF

OSPF is used as the IGP inside the ISP core to provide reachability between provider routers and loopback interfaces.

Verification commands:

    show ip interface brief
    show ip ospf neighbor
    show ip route ospf

### MPLS & LDP

MPLS is deployed across the ISP core and LDP is used for label distribution.

Verification commands:

    show mpls interfaces
    show mpls ldp neighbor
    show mpls forwarding-table

### BGP

BGP is used for Internet / ILL connectivity.

    ISP AS      : 65100
    Internet AS : 65110

Verification commands:

    show ip bgp summary
    show ip bgp
    show ip route bgp

### VRF

VRF is used to isolate VPN customer routing tables.

    VRF : customer-A
    RD  : 65100:10

Verification commands:

    show vrf
    show ip route vrf customer-A

Example:

    S  192.168.10.0/24
    B  192.168.20.0/24 via 4.4.4.4

The BGP route confirms that the remote customer network is being learned through the VPN.

### MP-BGP VPNv4

MP-BGP is used between PE1 and PE2 to exchange VPNv4 routes.

Verification commands:

    show ip bgp vpnv4 all summary
    show ip bgp vpnv4 all

## Customer Networks

    CE1
    192.168.10.0/24

            |
            | MPLS L3VPN
            |

    CE2
    192.168.20.0/24

## End-to-End Verification

A connectivity test was performed from CE1 to CE2:

    ping 192.168.20.1 source 192.168.10.1 repeat 100

Result:

    Success rate is 100 percent (100/100)

This confirms successful end-to-end connectivity between the VPN customer sites across the ISP MPLS L3VPN network.

## Verification Summary

| Technology | Status |
|---|---|
| OSPF | Verified |
| MPLS | Verified |
| LDP | Verified |
| BGP | Verified |
| VRF | Verified |
| MP-BGP VPNv4 | Verified |
| MPLS L3VPN | Verified |
| ILL / Internet | Verified |
| CE-to-CE Connectivity | Verified |

## Project Objectives

- Build an ISP network in GNS3
- Configure OSPF for ISP core connectivity
- Implement MPLS and LDP
- Configure BGP for Internet / ILL services
- Implement VRF-based customer isolation
- Configure MP-BGP VPNv4
- Provide MPLS L3VPN connectivity
- Verify end-to-end customer connectivity

## Lab Environment

    Platform : GNS3
    Vendor   : Cisco IOS
    Network  : ISP / Service Provider
    Services : MPLS L3VPN + Internet / ILL

## Disclaimer

This project is a GNS3-based networking lab created for learning, testing, and demonstration purposes.
