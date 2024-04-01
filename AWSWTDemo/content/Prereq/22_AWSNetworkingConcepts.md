---
title: "1.1 AWS Networking Concepts"
weight: 2
---

Before diving into the reference architecture in this demo, let's review core AWS networking concepts.

**AWS Virtual Private Cloud (VPC)** is a logically isolated section of the AWS Cloud where you can launch AWS resources in a virtual network that you define. You have complete control over your virtual networking environment, including selection of your own IP address range, creation of subnets, and configuration of route tables and network gateways.

**Availability Zones (AZ)** are multiple, isolated locations within each Region that have independent power, cooling, physical security, etc. A VPC spans all of the AZs in the Region.

**Region**, is a collection of multiple AZs in a geographic location. The collection of AZs in the same region are all interconnected via redundant, ultra-low-latency networks.

All **subnets** within a VPC are able to reach each other with the default or intrinsic router within the VPC. All resources in a subnet use the intrinsic router (1st host IP in each subnet) as the default gateway. Each subnet must be associated with a VPC route table, which specifies the allowed routes for outbound traffic leaving the subnet.

An **Internet Gateway (IGW)** is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic.


![22 image1](22-image1.png)


**AWS Transit Gateway (TGW)** is a highly scalable cloud router that connects your VPCs in the same region to each other, to on-premise networks, and even to the internet through one hub. With the use of multiple route tables for a single TGW, you can design hub and spoke routing for traffic inspection and enforcement of security policy across multiple VPCs.

![22 image2](22-image2.png)

**AWS (Gateway Load Balancer (GWLB)** is a transparent network gateway that distributes traffic (in a 3/5 tuple flow aware manner) to a fleet of virtual appliances for inspection. This is a regional load balancer that uses GWLB endpoints (GWLBe) to securely intercept data plane traffic within consumer VPCs in the same region.

![22 image3](22-image3.png)

In this demo you will use all these components to test FortiGate VM in an enterprise design. 

For a deep dive on AWS networking concepts in your own lab, outside of this demo, you can follow the [**AWS Network Immersion Day workshop**](https://catalog.workshops.aws/networking/en-US) in your own AWS account at your leisure.

If you want to read more about AWS network elements, [**click here**](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)


### Check this example to understand the packet walk in a GWLB deployment

![](https://raw.githubusercontent.com/FortiLatam/aws-ql-netsec-pub/main/media/image16.png)

**Packet walk**
1)  EC2 will check the route table for the more specific route. In this case 10.1.2.0/24 pointing to GWLBe-A
2)  Traffic arrives at GWBLe-A. Every time the traffic arrives at a GWLB endpoint it sends to the GWLB
3)  Traffic at GWLB will be forwarded to one member of the target group
4)  In this case we have only one FortiGate, so traffic arrives at FortiGate. It inspects the traffic and if allowed, send it back to GWLB
5)  GWLB sends the reply to GWLBe-A which originated the connection
6)  When traffic returns to GWLBe it checks its route table. For 10.1.0.0/24 it is "local". So it sends directly.
7)  Traffic arrives at the final destination


This concludes this section.
