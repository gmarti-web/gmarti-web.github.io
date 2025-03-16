---
title: What is a hub-and-spoke network?
last_modified_at: 2025-03-16
permalink: /portfolio/what-is-a-hub-and-spoke-network/
---

## Introduction

Network architecture patterns are reliable, industry-standard ways to manage connections between computing devices. They give you an example to follow as you set up your networking infrastructure. There are two archicture pattern categories you can use: _distributed_ or _centralized_. The best pattern category for your network depends on your use case and requirements.

The following table highlights some pros and cons of each category.

<table>
  <thead>
    <th>Architecture pattern</th>
    <th>Pros</th>
    <th>Cons</th>
  </thead>
  <tbody>
    <tr>
      <td>Distributed</td>
      <td><ul>
        <li>Easy to scale with new applications.</li>
        <li>Isolated networks limit how much one network impacts another.</li>
        <li>Networks can have individually customized firewall rules.</li>
      </ul></td>
      <td><ul>
        <li>Difficult to manage network-wide changes.</li>
        <li>Costly to maintain duplicated infrastructure.</li>
        <li>Overall network has many connections exposed to the public internet.</li>
      </ul></td>
    </tr>
    <tr>
      <td>Centralized</td>
      <td><ul>
        <li>Lower overall networking costs by sharing network services, like firewalls and internet gateways.</li>
        <li>Improved security against data breaches.</li>
        <li>Easy to make network-wide changes for security or compliance reasons.</li>
      </ul></td>
      <td><ul>
        <li>New applications must be attached to the hub network to be protected.</li>
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


In the cloud, [a best practice](https://learn.microsoft.com/en-us/azure/architecture/networking/architecture/hub-spoke) is a centralized network architecture called the _hub-and-spoke model_. This pattern directs traffic between many networks (spokes) and one central network (hub). The hub network shares its resources, like a firewall endpoint and an internet connection, with all the spoke networks. In the cloud, consolidated resources save the company money and lower the threat of exposing information.

In this article, you will learn about how traffic moves between a hub and each spoke in an AWS hub-and-spoke network. You'll also learn how the hub network secures the traffic with a network firewall.

## How does traffic move between a spoke and the hub?

In AWS, a hub-and-spoke network model is powered by [AWS Transit Gateway](https://aws.amazon.com/transit-gateway/). AWS Transit Gateway connects multiple [Amazon Virtual Private Clouds (VPCs)](https://aws.amazon.com/vpc/) to a central hub. You can connect a single transit gateway hub to [5,000 spoke VPCs](https://docs.aws.amazon.com/vpc/latest/tgw/transit-gateway-quotas.html) with transit gateway attachments. You define how traffic moves through these attachments with VPC route tables.

A VPC route table is a set of rules that determine where to send incoming traffic. Route tables have two main components:

<dl>
  <dt>Destination</dt>
  <dd>The IP address range where you want traffic to go. For example, <code>172.16.0.0/12</code>.</dd>
  <dt>Target</dt>
  <dd>The connection through which to send traffic. For example, an internet gateway or transit gateway attachment.</dd>
</dl>

The following diagram shows a network that sends all traffic through an internet gateway (the target) to the public internet (the destination).

{% include figure
  popup=true
  image_path="/assets/images/portfolio/hubandspoke/route-table-example.drawio.svg"
  alt="A diagram of an AWS VPC route table directing network traffic"
  caption="Figure 3: VPC route table directs traffic to DESTINATION through the TARGET"
%}

Route tables direct all traffic in to, out of, and within a hub-and-spoke network. In the following sections, we'll see how route tables move traffic:

* Within the hub network.
* Within a spoke network.
* Between the hub and a spoke.

### Hub network

### Spoke network

### Network-to-network communication

## Conclusion
