---
title: How to migrate your isolated cloud networks to a hub-and-spoke model
last_modified: 2025-03-15
toc: true
toc_sticky: true
toc_label: Table of contents
categories:
  - networking
  - technical blog
---

## Introduction

## Isolated networks

In an isolated network architecture, each virtual network has its own firewall. Each firewall has its own firewall policies and rules. That leaves each network responsible for managing which traffic is allowed in or out of the system.

{%
  include figure
  popup=true
  image_path="/assets/images/hubandspoke/multiple-network-firewalls.drawio.svg"
  alt="A diagram of multiple virtual networks connected to the internet through separate firewalls"
  caption="Isolated network systems"
%}

### Hard to maintain

This creates problems when all your networks must have the same configuration. Every change in a single network means you must change all networks to keep them in line. That involves a lot of places for something to go wrong, even if you automate the process. Someone must upkeep all this infrastructure. It can cause blindspots and makes it hard to onboard new administrators.

### Costly to support

Another result of having this much infrastructure is cost. Firewalls in any cloud provider are expensive. And the supporting infrastructure cost grows over time. If one of the benefits of the cloud is paying only for what you need, then we need to think about what it is we really need in our network topology.

## Hub-and-spoke model

### Set up a hub network

A hub network needs:

* A virtual network.
* A way to handle communication within the network, such as route tables or peering connections.
* A way to funnel traffic to and from the network through a network firewall.

#### Create a hub virtual private network

To create a hub virtual private network:

1. Go to the [Amazon VPC console](https://console.aws.amazon.com/vpcconsole/).
1. Change the region to **N. Virginia (us-east-1)**.

    {% include figure
      popup=true
      image_path="/assets/images/hubandspoke/region-choice.png"
      alt="A screenshot of the chosen AWS region"
    %}

1. Select **Create VPC**.
1. Enter or select the following:

    | Setting | Value |
    |---------|-------|
    | **Resource to create** | Choose **VPC only**. |
    | **Name tag** | Enter **vpc-hub**. |
    | **IPv4 CIDR block** | Enter **10.0.0.0/16** |

    {% include figure
      popup=true
      image_path="/assets/images/hubandspoke/vpc-settings.png"
      alt="A screenshot of the settings for a new VPC"
    %}

1. Select **Create VPC**.

Amazon VPC quickly launches your VPC. A banner confirms the launch.

#### Create hub subnets

A hub virtual network needs three subnets:

* One public firewall subnet
* One public NAT gateway subnet
* One private transit gateway subnet

To create the subnets:

1. Under Virtual prviate cloud, select **Subnets**.
1. Select **Create subnet**.
1. Create the public firewall subnet:
    1. Enter or select the following:

        | Setting | Value |
        |---------|-------|
        | **VPC ID** | Choose the VPC you created earlier (**vpc-hub**). |
        | **Subnet name** | Enter **fw-public**. |
        | **Availability Zone** | Choose **us-east-1a**.|
        | **IPv4 subnet CIDR block** | Enter **10.0.2.0/26** |

        {% include figure
          popup=true
          image_path="/assets/images/hubandspoke/sg-public-firewall.png"
          alt="A screenshot of a public firewall subnet's settings"
        %}

1. Create the public NAT gateway subnet:
    1. Select **Add new subnet**.
    1. Enter or select the following:

        | Setting | Value |
        |---------|-------|
        | **Subnet name** | Enter **ngw-public** |
        | **Availability zone** | Choose **us-east-1a** |
        | **IPv4 subnet CIDR block** | Enter **10.0.1.0/26** |

        {% include figure
          popup=true
          image_path="/assets/images/hubandspoke/sg-private-ngw.png"
          alt="A screenshot of a private NAT gateway subnet's settings"
        %}

1. Create the private transit gateway subnet:
    1. Select **Add new subnet**.
    1. Enter or select the following:

        | Setting | Value |
        |---------|-------|
        | **Subnnet name** | Enter **tgw-private** |
        | **Availability zone** | Choose **us-east-1a** |
        | **IPv4 subnet CIDR block** | Enter **10.0.0.0/26** |

        {% include figure
          popup=true
          image_path="/assets/images/hubandspoke/sg-private-tgw.png"
          alt="A screenshot of a private transit gateway subnet's settings"
        %}

1. Select **Create subnet**.

Amazon VPC quickly launches your three subnets. A banner confirms the launch.

#### Create internet gateways

To create a NAT gateway:

1. Under Virtual private cloud, select **Nat gateways**.
1. Select **Create NAT gateway**.
1. Enter or select the following:

    | Setting | Value |
    |---------|-------|
    | **Name** | Enter **hub-nat-gateway**. |
    | **Subnet** | Choose the public NAT gateway you created earlier (**ngw-public**). |
    | **Elastic IP allocation ID** | Select **Allocate Elastic IP**. |

    {% include figure
      popup=true
      image_path="/assets/images/hubandspoke/nat-gateway-settings.png"
      alt="A screenshot of a NAT gateway's settings"
    %}

1. Select **Create NAT gateway**.

AWS quickly launches your NAT gateway. A banner confirms the launch.

To create an internet gateway:

1. Under Virtual private cloud, go to **Internet gateways**.
1. Select **Create internet gateway**.
1. Enter **igw-hub** for the internet gateway's name.

    {% include figure
      popup=true
      image_path="/assets/images/hubandspoke/igw-settings.png"
      alt="A screenshot of an internet gateway's settings"
    %}

1. Select **Create internet gateway**.
1. Select **Actions > Attach to VPC**.
1. Select the VPC you created earlier (**hub-vpc**)

    {% include figure
      popup=true
      image_path="/assets/images/hubandspoke/igw-attach-settings.png"
      alt="A screenshot of an internet gateway's attachment settings"
    %}

1. Select **Attach internet gateway**

AWS quickly attaches your internet gateway to your VPC. A banner confirms the attachment.

#### Create a network firewall

To create a network firewall:

1. Under Network Firewall, select **Firewalls**.
1. Select **Create firewall**.

### Set up a spoke network

### Connect spokes to the hub

## Conclusion
