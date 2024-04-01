---
title: "3. Tasks"
weight: 3
---

These tasks were thinking of to demo some features of using FortiGate with gateway load balancer, but you can think in other tests.

Feel free to explore the AWS routing tables, check TGW configuration, etc. If you have suggestions for other labs, that are not here or you don't have permission to do it, please write a comment in the same Sharepoint page you got the credentials.

There is no specific order to perform the tasks.

{{% notice info %}}
**In this AWS account you will see subnets, route tables and other network elements for 2 AZs (availability zones), however we will use only one AZ. Why? With one AZ you can see how it works and it is faster. But we left two AZs configured because you can use this demo to understand how routing works, using GWLB/FGT and maybe help your customer**
{{% /notice %}}

## Use Cases
### 3.1 Connectivity: North-South

Cloud network security, usually, starts with North-South inspection (sometimes performed by different elements, such as WAF for incoming traffic depending on the application/target workload) so that's why it is our first use case. 

With FortiGate inspecting the NS traffic, the customer can have:
* Visibility
* Control
* Security

IPS, anti-malware, geo-ip control, DLP, etc are only few of security features when deploying FortiGate's in such scenario. In this particular case we are using AWS gateway load-balancer, where the customer doesnt need to remove public IP's (EIPs) from EC2s and without the need to configure NAT in FortiGate for inspection, with the change of route tables it can be done.

### 3.2 Connectivity: East-West

Usually the common step after NS. With ES inspection, the customer can control easliy and in a central management, all of traffic security inside AWS. In this use case you will how to manage it and block traffic from subnets inside the same VPC

### 3.3 IPS: Log4Shell attack

Maybe you need to demo "why to have a FortiGate in AWS if I already have security groups and "AWS cloud datacenter" security for free?" Well... there are a lot of answers for this question and the most common is the [AWS Shared Responsability Model] (https://aws.amazon.com/compliance/shared-responsibility-model/) but a ~~image~~ demo worth a thousand words.