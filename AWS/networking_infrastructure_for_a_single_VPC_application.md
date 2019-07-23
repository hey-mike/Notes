# Networking Infrastructure for a Single VPC Application

## INTRODUCING THE BASIC AWS NETWORK INFRASTRUCTURE

- **Network Interfaces**: This logical network component serves to represent a physical network interface card (NIC); as such, this component can be configured with IPv4 and IPv6 addresses.

- **Route Tables**: Just as would exist on a physical router, AWS route tables contain a set of rules, called routes, that are used to determine where network traffic is directed.

- **Internet Gateways**: An Internet gateway serves two purposes: to provide a target in your VPC route tables for Internet-routable traffic and to perform Network Address Translation (NAT) for instances that have been assigned public IPv4 addresses.

- **Egress-Only Internet Gateways**: These VPC components allow outbound communication over IPv6 from instances in your VPC to the Internet and prevent the Internet from initiating an IPv6 connection with your instances.

- **DHCP Option Sets**: DHCP provides a standard for passing configuration information to hosts on a TCP/IP network. The Options field of a DHCP message contains the configuration parameters. Some of those parameters are the domain name, domain name server, and the netbios-node-type. The option sets allow you to configure such options for your VPC.

- **DNS**: AWS provides you with a DNS server for your VPC, but it is important to realize that you can also use your own.

- **Elastic IP Addresses**: These static IPv4 addresses are designed for dynamic cloud computing. An Elastic IP address is associated with your AWS account; with this address, you can mask the failure of an instance or software by rapidly remapping the address to another instance in your account.

- **VPC Endpoints**: These endpoints enable you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an Internet gateway, NAT device, VPN connection, or AWS Direct Connect connection.

- **NAT**: You can use a NAT device to enable instances in a private subnet to connect to the Internet (for example, for software updates) or other AWS services but prevent the Internet from initiating connections with the instances. AWS offers two kinds of NAT devices—a NAT gateway and a NAT instance—but strongly recommends the use of NAT gateways.

- **VPC Peering**: This networking connection between two VPCs enables you to route traffic between them privately. You can create a VPC peering connection between your own VPCs, with a VPC in another AWS account, or with a VPC in a different AWS Region.

- **ClassicLink**: This component allows you to link your EC2-Classic instance to a VPC in your account, within the same region. This allows you to associate the VPC security groups with the EC2-Classic instance, enabling communication between your EC2-Classic instance and instances in your VPC using private IPv4 addresses.

## NETWORK INTERFACES

include the following attributes:

- A primary private IPv4 address

- One or more secondary private IPv4 addresses

- One Elastic IP address per private IPv4 address

- One public IPv4 address, which can be auto-assigned to the network interface for eth0 when you launch an instance

- One or more IPv6 addresses

- One or more security groups

- A MAC address

- A source/destination check flag

- A description

### Keep the following in mind

- You can create a network interface, attach it to an instance, detach it from an instance, and attach it to another instance.

- A network interface’s attributes follow it as it is attached or detached from an instance and reattached to another instance.

- When you move a network interface from one instance to another, network traffic is redirected to the new instance.

- Each instance in your VPC has a default network interface (the primary network interface) that is assigned a private IPv4 address from the IPv4 address range of your VPC.

- **You cannot detach a primary network interface from an instance.** You can create and attach an additional network interface to any instance in your subnet.

- The number of network interfaces you can attach varies by instance type. A**ttaching multiple network interfaces to an instance is useful when you want to create a management network**, use network and security appliances in your VPC, create dual-homed instances with workloads/roles on distinct subnets, or create a low-budget, high-availability solution.
