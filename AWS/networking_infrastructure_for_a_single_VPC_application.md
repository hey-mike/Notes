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

## ROUTE TABLES

### Keep these points in mind

- Your VPC has an implicit router.

- Your VPC automatically comes with a main route table that you can modify.

- You can create additional custom route tables for your VPC.

- Each subnet must be associated with a route table, which controls the routing for the subnet. If you do not explicitly associate a subnet with a particular route table, the subnet is implicitly associated with the main route table.

- You cannot delete the main route table, but you can replace the main route table with a custom table that you have created.

- Each route in a table specifies a destination CIDR and a target. Just like physical routers, the most specific route that matches the traffic determines how to route the traffic.

- CIDR blocks for IPv4 and IPv6 are treated separately.

- Every route table contains a local route for communication within the VPC over IPv4. If your VPC has more than one IPv4 CIDR block, your route tables contain a local route for each IPv4 CIDR block. If you have associated an IPv6 CIDR block with your VPC, your route tables contain a local route for the IPv6 CIDR block. You cannot modify or delete these routes.

- When you add an Internet gateway, an egress-only Internet gateway, a virtual private gateway, a NAT device, a peering connection, or a VPC endpoint in your VPC, you must update the route table for any subnet that uses these gateways or connections.

- There is a limit on the number of route tables you can create per VPC and the number of routes you can add per route table.

## INTERNET GATEWAYS

## To enable access to or from the Internet for instances in a VPC subnet, you must do the following:

- Attach an Internet gateway to your VPC.

- Ensure that your subnet’s route table points to the Internet gateway.

- Ensure that instances in your subnet have a globally unique IP address.

- Ensure that your network access control and security group rules allow the relevant traffic to flow to and from your instance.

## EGRESS-ONLY INTERNET GATEWAYS

> Note
> To enable outbound-only Internet communication over IPv4, use a NAT gateway instead.
> IPv6 addresses are globally unique and are therefore public by default. If you want your instance to be able to access the Internet but you want to prevent resources on the Internet from initiating communication with your instance, you can use this egress-only Internet gateway.

- An egress-only Internet gateway is **stateful**: it forwards traffic from the instances in the subnet to the Internet or other AWS services and then sends the response back to the instances.

### characteristics

- You cannot associate a security group with an egress-only Internet gateway. You can use security groups for your instances in the private subnet to control the traffic to and from those instances.

- You can use a network ACL to control the traffic to and from the subnet for which the egress-only Internet gateway routes traffic.

## DHCP OPTION SETS

- domain-name-servers

- domain-name

- ntp-servers

- netbios-name-servers

- netbios-node-type

## DNS

- As you know, Domain Name System (DNS) is a standard by which names used on the Internet are resolved to their corresponding IP addresses. A DNS hostname is a name that uniquely and absolutely names a computer. It is composed of a hostname and a domain name. DNS servers resolve DNS hostnames to their corresponding IP addresses.
- Public IPv4 addresses enable communication over the Internet, while private IPv4 addresses enable communication within the network of the instance (either EC2-Classic or a VPC).
- AWS provides you with an Amazon DNS server. To use your own DNS server, create a new set of DHCP options for your VPC.

## ELASTIC IP ADDRESSES

- An Elastic IP address is a public IPv4 address, which is reachable from the Internet
- AWS does not currently support Elastic IP addresses for IPv6

### Characteristics

- To use an Elastic IP address, you first allocate one to your account and then associate it with your instance or a network interface.

- When you associate an Elastic IP address with an instance or its primary network interface, the instance’s public IPv4 address (if it had one) is released back into Amazon’s pool of public IPv4 addresses. You cannot reuse a public IPv4 address.

- You can disassociate an Elastic IP address from a resource and reassociate it with a different resource. Any open connections to an instance continue to work for a time even after you disassociate its Elastic IP address and reassociate it with another instance. We recommend that you reopen these connections using the reassociated Elastic IP address.

- A disassociated Elastic IP address remains allocated to your account until you explicitly release it.

- To ensure efficient use of Elastic IP addresses, Amazon imposes a small hourly charge if an Elastic IP address is not associated with a running instance, or if it is associated with a stopped instance or an unattached network interface. While your instance is running, you are not charged for one Elastic IP address associated with the instance, but you are charged for any additional Elastic IP addresses associated with the instance.

- An Elastic IP address is for use in a specific region only.

- When you associate an Elastic IP address with an instance that previously had a public IPv4 address, the public DNS hostname of the instance changes to match the Elastic IP address.

- AWS resolves a public DNS hostname to the public IPv4 address or the Elastic IP address of the instance outside the network of the instance, and to the private IPv4 address of the instance from within the network of the instance.

## VPC ENDPOINTS

- A VPC endpoint enables you to privately connect your VPC to supported AWS services and VPC endpoint services powered by PrivateLink without requiring an Internet gateway, NAT device, VPN connection, or AWS Direct Connect connection. I
- Instances in your VPC do not require public IP addresses to communicate with resources in the service. Traffic between your VPC and the other service does not leave the Amazon network.
- Endpoints are virtual devices. They are highly available VPC components that allow communication between instances in your VPC and services without imposing availability risks or bandwidth constraints on your network traffic.
- There are **two types of VPC endpoints**: **interface endpoints and gateway endpoints**. You should create the type of VPC endpoint required by the supported service.

### Interface Endpoints (Powered by AWS PrivateLink)

- API Gateway

- CloudWatch

- CloudWatch Events

- CloudWatch Logs

- CodeBuild

- Config

- EC2 API

- Elastic Load Balancing API

- Key Management Service

- Kinesis Data Streams

- SageMaker Runtime

- Secrets Manager

- Security Token Service

- Service Catalog

- SNS

- Systems Manager

- Endpoint services hosted by other AWS accounts

- Supported AWS Marketplace partner services

### Gateway Endpoints

A gateway endpoint is a gateway that is a target for a specified route in your route table, used for traffic destined to a supported AWS service. The following AWS services are supported:

- S3
- DynamoDB

## NAT

- a NAT device to enable instances in a private subnet to connect to the Internet or other AWS services but prevent the Internet from initiating connections with the instances
- forwards traffic from the instances in the private subnet to the Internet or other AWS services and then sends the response back to the instances.
- When traffic goes to the Internet, the source IPv4 address is replaced with the NAT device’s address, and similarly, when the response traffic goes to those instances, the NAT device translates the address back to those instances’ private IPv4 addresses.
- NAT devices are not supported for IPv6 traffic.
- a NAT gateway and a NAT instance. **AWS recommends NAT gateways** because they provide better availability and bandwidth over NAT instances
- A NAT instance is launched from a NAT AMI.

## VPC PEERING

- An AWS VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them privately. You can create a VPC peering connection between your own VPCs, **with a VPC in another AWS account**, or **with a VPC in a different AWS Region**.
- AWS uses the existing infrastructure of a VPC to create a VPC peering connection
- it is neither a gateway nor a VPN connection, and does not rely on a separate piece of physical hardware.

## CLASSICLINK

- ClassicLink allows you to link your **EC2-Classic** instance to a VPC in your account, within the same region.
- This enables you to associate the VPC security groups with the EC2-Classic instance.
- enabling communication between your EC2-Classic instance and instances in your VPC using private IPv4 addresses.
- ClassicLink removes the need to make use of public IPv4 addresses or Elastic IP addresses to enable communication between instances in these platforms.
  > Note
  > EC2-Classic instances cannot be enabled for IPv6 communication. You can associate an IPv6 CIDR block with your VPC and assign IPv6 addresses to resources in your VPC; however, communication between a ClassicLinked instance and resources in the VPC is over IPv4 only.
