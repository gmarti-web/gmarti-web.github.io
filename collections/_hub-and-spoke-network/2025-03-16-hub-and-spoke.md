---
title: Network communication in an AWS VPC hub-and-spoke architecture
last_modified_at: 2025-03-17
permalink: /portfolio/network-communication-in-an-aws-vpc-hub-and-spoke-architecture/
---

## Introduction

Network architecture patterns are reliable, industry-standard ways to manage connections between computing devices. They give you an example to follow as you set up your networking infrastructure. Two architecture pattern categories you can use are: _decentralized_ or _centralized_.

In the cloud, [a best practice](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke) is a centralized network architecture called the _hub-and-spoke model_. This pattern directs traffic between many networks (spokes) and one central network (hub). The hub network shares its resources, like a [network firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/what-is-aws-network-firewall.html), a [NAT gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html), and an internet gateway, with all the spoke networks. As a company expands its cloud infrastructure footprint, consolidated resources save money and lower the threat of exposing information.

In this article, you'll learn:

* Why a centralized architecture, like the hub-and-spoke model, is a best practice in the cloud.
* How traffic moves between VPCs in a hub-and-spoke model.
* How a hub-and-spoke model saves your organization money by sharing a single network firewall, NAT gateway, and internet gateway with your entire network.

## Decentralized VPC architecture

In a decentralized VPC architecture, each application is completely isolated. This means it has its own infrastructure, security settings, and internet exposure points. To add a new application to the network, you must recreate all these components. While this may suit businesses with one, two, or maybe three applications, it's cumbersome to manage and costly to maintain as the business scales.

For example, consider an organization with only one application. They create a single VPC with:

* A NAT gateway
* A network firewall
* An internet gateway

After some time, they create a new application. To have the same security as their first application, they create a VPC with the same components. Later, they replicate their VPC again for a third application. As the organization scales and creates more applications, they add more infrastructure to their AWS environment.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/multiple-network-firewalls.drawio.svg"
  alt="A diagram of three separate AWS cloud networks"
  caption="Figure 1: Arbitrary number of decentralized AWS VPCs connected to the public internet"
%}

This infrastructure duplication is expensive. For a single VPC in the diagram above, it [costs $322 USD to process just 10 GB of data per month](https://calculator.aws/#/estimate?id=b12e071c14c1cdf95fff8d2618465fbbfe63545b). For three VPCs, the costs triple. And, its multiple exposures to the internet make it less secure. Firewall policies and security measures must be replicated across every VPC.

As an organization scales, then, it must consider how it manages its growing network. The best way to do that is to switch to a centralized VPC architecture, specifically a hub-and-spoke model.

## Centralized (hub-and-spoke) VPC architecture

In a centralized VPC architecture, like the hub-and-spoke model, each application (spokes) connects to a central network (hub). The hub network shares a single set of networking infrastructure with all the spoke networks. This shared infrastructure significantly reduces an organization's overall cloud costs. A hub-and-spoke model is more secure, as well, because it has only one internet exposure point to protect.

For example, in the following diagram, a hub VPC in a hub-and-spoke architecture shares its firewall, NAT gateway, and internet gateway with all three spoke VPCs.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/hub-and-spoke-overview.drawio.svg"
  alt="A diagram of three spoke AWS networks connected to one hub network"
  caption="Figure 2: AWS networks connected to the public internet through a central, firewall-protected hub network"
%}

In the following sections, we'll learn how the spokes communicate with the hub, and the hub with each spoke, in detail.

## Inter-VPC traffic with AWS Transit Gateway

In AWS, a hub-and-spoke network model is powered by [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/). AWS Transit Gateway connects multiple VPCs to a central hub. You can connect a single transit gateway hub to [5,000 spoke VPCs](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-quotas.html) with transit gateway attachments. You define how traffic moves through these attachments with VPC route tables.

A VPC route table is a set of rules, called _routes_, that determine where to send incoming traffic. Route tables have two main components:

<dl>
  <dt>Destination</dt>
  <dd>The IP address range where you want traffic to go. For example, <code>172.16.0.0/16</code>.</dd>
  <dt>Target</dt>
  <dd>The connection or route through which to send traffic. For example, an internet gateway or transit gateway attachment. The default route through a VPC is the <strong>local</strong> route. It lets resources within a VPC communicate through private IP addresses.</dd>
</dl>

{%- capture tip-content -%}

If the route table's destination is `0.0.0.0/0`, it routes all traffic through the target.

{% endcapture %}

{% include tip-notice.html content="If the route table's destination is `0.0.0.0/0`, it routes all traffic to the target." %}

Route tables direct all traffic in to, out of, and within a hub-and-spoke network.

Now, let's explore how route tables move traffic:

* Between the hub and a spoke VPCs.
* Within the hub VPC.
* Within a spoke VPC.

### Traffic between the hub VPC and a spoke VPC

Transit gateway route tables transfer traffic from one VPC to another.

* One route table directs traffic from the firewall to the each spoke.
* One route table for each spoke VPC directs traffic from the spoke to the firewall.

The following diagram shows how route tables direct the traffic between a hub and spoke VPC:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/transit-gateway-details.drawio.svg"
  alt="A diagram of the transit gateway between the hub and a spoke VPC in an AWS hub-and-spoke model"
  caption="Figure 4: Traffic flow between the hub VPC and a spoke VPC"
%}

#### Internet-bound traffic from spoke VPC to hub VPC

When a spoke VPC sends internet-bound traffic to the transit gateway:

1. The traffic enters the transit gateway through the spoke transit gateway attachment.
1. A transit gateway route table sends the traffic to the hub transit gateway attachment.

The following diagram shows traffic from a spoke VPC to the hub:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/spoketgwa-to-hubtgwa.drawio.svg"
  alt="A diagram of internet-bound traffic sent from a spoke VPC to the hub VPC"
  caption="Figure 5: Traffic flow from spoke VPC to hub VPC"
%}


#### Spoke-bound traffic from hub VPC to spoke VPC

When the hub VPC sends traffic back to the spoke VPC through the transit gateway:

1. The traffic enters the transit gateway through the hub transit gateway attachment.
1. A transit gateway route table sends the traffic to the spoke transit gateway attachment.

The following diagram shows traffic from a hub VPC to a spoke:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/hubtgwa-to-spoketgwa.drawio.svg"
  alt="A diagram of spoke-bound traffic sent from the hub VPC to a spoke VPC"
  caption="Figure 6: Traffic flow from hub VPC to spoke VPC"
%}

### Traffic within a hub VPC

The hub VPC has the network's firewall and sole internet connection. Route tables move this traffic from a spoke's VPC, to the internet, and back to the spoke.

The following diagram shows how route tables move traffic within the hub VPC. In this example, the spoke VPC's IP address range is 172.16.0.0/12. Traffic moves from the spoke to the internet through the transit gateway and network firewall:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/hub-network-details.drawio.svg"
  alt="A diagram of the hub VPC in an AWS hub-and-spoke network model"
  caption="Figure 7: Traffic flow within the hub VPC"
%}

#### Internet-bound traffic through the hub VPC

When a spoke VPC sends internet-bound traffic to the hub VPC:

1. The traffic enters the hub VPC from the hub transit gateway attachment through a network interface.
1. The interface's associated route table sends it to a NAT gateway.

The following diagram shows traffic from a spoke VPC as it enters the hub:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/eni-to-nat.drawio.svg"
  alt="A diagram of internet-bound traffic routed from a network interface to a NAT gateway"
  caption="Figure 8: Internet-bound traffic routed through NAT gateway"
%}

The NAT gateway is the hub VPC's connection to the network firewall and the public internet. [NAT gateways](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html) add extra security to internet connections. It translates a VPC subnet's private IP address to a public one.

When the internet-bound traffic reaches the NAT gateway:

1. The gateway's associated route table sends it to the network firewall.
1. The firewall checks its firewall policy for the intended internet address.

    * If the traffic is allowed, the firewall's associated route table sends the traffic to the internet gateway.
    * Otherwise, the firewall blocks the traffic from moving forward.

The following diagram shows traffic as it's routed to the public internet:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/nat-to-igw.drawio.svg"
  alt="A diagram of internet-bound traffic routed from a NAT gateway to an internet gateway through a network firewall"
  caption="Figure 9: Internet-bound traffic routed through network firewall"
%}

#### Spoke-bound traffic through the hub VPC

When the internet sends traffic back to the hub VPC:

1. The traffic enters the hub VPC from the internet through the network firewall.
1. The firewall checks its firewall policy for the incoming internet address.

    * If the traffic is allowed, the firewall's associated route table sends the traffic to the NAT gateway subnet.
    * Otherwise, the firewall blocks the traffic from moving forward.

1. The NAT gateway translates the incoming public IP address to the spoke VPC's private IP address range.
1. The NAT gateway's associated route table sends the traffic back to the spoke through the network interface and transit gateway.

The following diagram shows traffic as it's routed from the public internet back to the spoke VPC:

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/igw-to-tgw.drawio.svg"
  alt="A diagram of spoke-bound traffic from the internet"
  caption="Figure 10: Spoke-bound traffic routed through network firewall and transit gateway"
%}

### Spoke VPC

A spoke VPC is an individual node in the network. A spoke VPC might serve an application in the same AWS account as the hub VPC or in another account from a company's organization.

In the spoke VPC:

1. A route table sends all internet-bound traffic to the transit gateway.
1. A network interface and a transit gateway attachment connect it to the transit gateway.

The following diagram shows how route tables move traffic from a spoke VPC to the hub VPC.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/spoke-network-details.drawio.svg"
  alt="A diagram of a spoke VPC in an AWS hub-and-spoke network model"
  caption="Figure 11: Traffic flow from a single spoke VPC"
%}

## Conclusion

In this article, we saw how:

* The hub-and-spoke model uses AWS Transit Gateways to connect multiple VPCs to a central hub.
* VPC route tables direct traffic flow between all VPCs in the network.
* A single NAT gateway and a network firewall in the hub VPC protect all the spoke VPCs in the network.

The hub-and-spoke network model is a powerful way to manage your cloud networks easily and efficiently. It lets you scale your applications without the cost of additional security services, like firewalls or NAT gateways. It's flexibility lets you modify the architecture to fit your business requirements. For example, you can duplicate your hub VPC across multiple availability zones to improve the network's availability. A centralized network, like the hub-and-spoke model, gives you complete control over the entire system.

Check out the following resources to learn more about centralized networks or how to build your own hub-and-spoke model:

* [Deployment models for AWS Network Firewall](https://aws.amazon.com/blogs/networking-and-content-delivery/deployment-models-for-aws-network-firewall/)
* [Creating a single internet exit point from multiple VPCs using AWS Transit Gateway](https://aws.amazon.com/blogs/networking-and-content-delivery/creating-a-single-internet-exit-point-from-multiple-vpcs-using-aws-transit-gateway/)
* [Using the NAT gateway with AWS Network Firewall for centralized IPv4 egress](https://docs.aws.amazon.com/whitepapers/latest/building-scalable-secure-multi-vpc-network-infrastructure/using-nat-gateway-with-firewall.html)
* [Architecture with an internet gateway and a NAT gateway using AWS Network Firewall](https://docs.aws.amazon.com/network-firewall/latest/developerguide/arch-igw-ngw.html)
