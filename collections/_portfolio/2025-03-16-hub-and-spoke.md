---
title: What is a hub-and-spoke network?
last_modified_at: 2025-03-16
permalink: /portfolio/what-is-a-hub-and-spoke-network/
---

## Introduction

Network architecture patterns are reliable, industry-standard ways to manage connections between computing devices. They give you an example to follow as you set up your networking infrastructure. Two architecture pattern categories you can use are: _distributed_ or _centralized_. The best pattern category for your network depends on your use case and requirements.

The following table highlights some pros and cons of each category.

<table>
  <thead>
    <th>Architecture pattern</th>
    <th>Pros</th>
    <th>Cons</th>
  </thead>
  <tbody>
    <tr>
      <td><strong>Distributed</strong></td>
      <td><ul>
        <li>Easy to add new applications.</li>
        <li>Isolated networks limit one network's impact on another.</li>
        <li>Networks can have individually customized firewall rules.</li>
      </ul></td>
      <td><ul>
        <li>Difficult to manage network-wide changes.</li>
        <li>Costly to maintain duplicated infrastructure.</li>
        <li>Overall network has many connections exposed to the public internet.</li>
      </ul></td>
    </tr>
    <tr>
      <td><strong>Centralized</strong></td>
      <td><ul>
        <li>Lower overall networking costs by sharing network services, like firewalls and internet gateways.</li>
        <li>Improved security against data breaches.</li>
        <li>Easy to make network-wide changes for security or compliance reasons.</li>
      </ul></td>
      <td><ul>
        <li>New applications must be attached to the hub network.</li>
        <li>Complex structure compared to a distributed network.</li>
      </ul></td>
    </tr>
  </tbody>
</table>

The following diagrams show a distributed and a centralized network configured in an Amazon Web Services (AWS) environment.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/multiple-network-firewalls.drawio.svg"
  alt="A diagram of three separate AWS cloud networks"
  caption="Figure 1: Distributed AWS networks connected to the public internet"
%}


{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/hub-and-spoke-overview.drawio.svg"
  alt="A diagram of three spoke AWS networks connected to one hub network"
  caption="Figure 2: AWS networks connected to the public internet through a central, firewall-protected hub network"
%}


In the cloud, [a best practice](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke) is a centralized network architecture called the _hub-and-spoke model_. This pattern directs traffic between many networks (spokes) and one central network (hub). The hub network shares its resources, like a network firewall, a [NAT gateway](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-nat-gateway.html), and an internet connection, with all the spoke networks. As a company expands its cloud infrastructure footprint, consolidated resources save money and lower the threat of exposing information.

In this article, you will learn about how traffic moves between a hub and each spoke in an AWS hub-and-spoke network. You'll also learn how the hub network secures the traffic with a network firewall.

## How does traffic move between a spoke and the hub?

In AWS, a hub-and-spoke network model is powered by [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/). AWS Transit Gateway connects multiple [Amazon Virtual Private Clouds (VPCs)](https://aws.amazon.com/vpc/) to a central hub. You can connect a single transit gateway hub to [5,000 spoke VPCs](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-quotas.html) with transit gateway attachments. You define how traffic moves through these attachments with VPC route tables.

A VPC route table is a set of rules, called _routes_, that determine where to send incoming traffic. Route tables have two main components:

<dl>
  <dt>Destination</dt>
  <dd>The IP address range where you want traffic to go. For example, <code>172.16.0.0/12</code>.</dd>
  <dt>Target</dt>
  <dd>The connection or route through which to send traffic. For example, an internet gateway or transit gateway attachment. The default route through a VPC is the <strong>local</strong> route. It lets resources within a VPC communicate through private IP addresses.</dd>
</dl>

The following diagram shows a network that sends all traffic through an internet gateway (the target) to the public internet (the destination).

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/route-table-example.drawio.svg"
  alt="A diagram of an AWS VPC route table directing network traffic"
  caption="Figure 3: VPC route table directs traffic to DESTINATION through the TARGET"
%}

{%- capture tip-content -%}

If the route table's destination is `0.0.0.0/0`, it routes all traffic to the target.

{% endcapture %}

{% include tip-notice.html content="If the route table's destination is `0.0.0.0/0`, it routes all traffic to the target." %}

Route tables direct all traffic in to, out of, and within a hub-and-spoke network. In the following sections, we'll see how route tables move traffic:

* Within the hub network.
* Within a spoke network.
* Between the hub and a spoke.

### Hub network

The hub network has the network's firewall and sole internet endpoint. Route tables move this traffic from a spoke's transit gateway attachment, to the internet, and back to the spoke.

The following diagram shows how route tables move traffic within the hub network. In this example, the spoke VPC's IP address range is 172.16.0.0/12.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/hub-network-details.drawio.svg"
  alt="A diagram of the hub VPC in an AWS hub-and-spoke network model"
  caption="Figure 4: Traffic flow within the hub VPC"
%}

#### Transit gateway to hub VPC

The transit gateway routes all traffic from a spoke VPC to a network interface associated with the hub's transit gateway attachment.

The transit gateway attachment and its network interface are associated with a specific subsection of the hub VPC, called a subnet. A subnet occupies a portion of the hub VPC's full IP address range. For example, if a subnet has 10,000 available IP addresses, a subnet might use only 3,000 of them. We use a subnet's IP address range to route traffic through it with the network's route tables.

The subnet's route table sends all traffic from a spoke to the NAT gateway.

#### NAT gateway

The NAT gateway is the hub network's connection to the network firewall and the public internet. NAT gateways add extra security to internet connections. They limit the number of outgoing IP address, and they reject all unsolicited incoming traffic. It allows incoming traffic only in response to a request from a spoke network.

The NAT gateway subnet's route table sends all traffic from the transit gateway subnet to the network firewall.

#### Network Firewall

The network firewall checks all traffic against the firewall policy. The policy defines which domains the network can access. Firewall polies block any traffic to a non-allowed domain.

The firewall subnet's route table sends all allowed traffic from the NAT gateway subnet to the internet gateway. From the internet gateway, the traffic exists the hub VPC and connects to the public internet.

#### Traffic from the internet

All traffic that returns from the internet is routed to the NAT gateway subnet through the network firewall. The firewall inspects traffic as it comes in. If it's allowed, then it continues to the NAT gateway subnet. Otherwise, the firewall policy blocks it.

Traffic that reaches the NAT gateway subnet is routed back to the spoke VPC through the transit gateway.

### Spoke network

A spoke network is an individual node in your network architecture. A spoke network might belong to an application in the same AWS account or another account in a company's organization.

Route tables in the spoke network send all traffic to the transit gateway. Similar to the hub VPC, the spoke VPC connects to the transit gateway with a transit gateway attachment and a network interface.

The following diagram shows how route tables move traffic from a spoke VPC to the hub VPC.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/spoke-network-details.drawio.svg"
  alt="A diagram of a spoke VPC in an AWS hub-and-spoke network model"
  caption="Figure 5: Traffic flow from a single spoke VPC"
%}

### Network-to-network communication

The transfer from one VPC to another happens at the transit gateway. The gateway has:

* One route table to direct traffic from the firewall to the each spoke.
* One route table for each spoke VPC to direct traffic from the spoke to the firewall.

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/transit-gateway-details.drawio.svg"
  alt="A diagram of the transit gateway between the hub and a spoke VPC in an AWS hub-and-spoke model"
  caption="Figure 6: Traffic flow between the hub VPC and a spoke VPC"
%}

## Conclusion
