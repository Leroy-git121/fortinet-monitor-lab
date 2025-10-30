Fortinet VM64-KVM Web GUI Configuration Guide
Introduction

This guide explains how to configure your Fortinet firewall to enable network traffic monitoring using only the web management interface—no CLI required. Follow along using the screenshots provided in your repo.
1. Interface Configuration

WAN Interface

    Go to Network > Interfaces.

    Click Edit on port1 (WAN), set:

        Alias: WAN

        IP/Netmask: 192.168.42.139/255.255.255.0

        Administrative Access: Select HTTPS, HTTP, PING, SSH

    Click OK.

LAN Interface

    Edit port2 (LAN), set:

        Alias: LAN

        IP/Netmask: 10.0.0.1/255.255.255.0

        Administrative Access: Select HTTPS, HTTP, PING, SSH

    Click OK.

![WAN GUI Config](g]( 2. DHCP Server Setup

    Still in Network > Interfaces, edit your LAN interface.

    Under DHCP Server, enable and set:

        IP Range: 10.0.0.2 – 10.0.0.254

        Default Gateway: 10.0.0.1

        DNS Server: e.g., 208.91.112.53

    Save changes.

![DHCP Server](3.jpg Static Route

    Go to Network > Static Routes.

    Add a new route:

        Destination: 0.0.0.0/0

        Interface: WAN (port1)

        Gateway: 192.168.42.2

        Administrative Distance: 10

    Enable the route and click OK.

![Static Route GUI]( 4. Firewall Policy

    Navigate to Policy & Objects > IPv4 Policy.

    Click Create New or edit rule:

        Name: LAN to WAN

        Incoming Interface: LAN (port2)

        Outgoing Interface: WAN (port1)

        Source/Destination: all

        Schedule: always

        Service: ALL

        Action: ACCEPT

        NAT: Enable

    Enable and save the policy.

![Firewall Policy GUI]( 5. Traffic Monitoring

    Go to FortiView > Traffic from LAN/DMZ.

    Watch live endpoints, sessions, and bandwidth.

    Click on details for per-host or per-application views.

![Traffic View 1](2](

    Refresh DHCP and FortiView monitors to see live changes.

    Use the policy monitor for troubleshooting blocked or unexpected traffic.

    Screenshot your config changes for easy documentation.

Feel free to add local or WAN PCs in EVE-NG for simulated endpoint testing and produce more monitoring data. This guide keeps all actions in the GUI so users can replicate without needing CLI familiarity.
