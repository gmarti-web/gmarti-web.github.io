---
title: How to migrate your isolated cloud network architecture to a hub-and-spoke model
last_modified: 2025-03-15
categories:
  - networking
  - technical blog
---

## Introduction

## Isolated network firewalls—A firewall for each account

In an isolated network architecture, each virtual network has its own firewall. Each firewall has its own firewall policies and rules. That leaves each network responsible for managing which traffic is allowed in or out of the system.

{%
  include figure
  popup=true
  image_path="/assets/images/hubandspoke/multiple-network-firewalls.drawio.svg"
  alt="A diagram of multiple virtual networks connected to the internet through separate firewalls"
  caption="Isolated network system"
%}

This creates problems when you want all your networks to have the same configuration.

### Hard to maintain

### Costly to support

## Hub-and-spoke modle

### Set up a hub account

### Set up a spoke account

### Connect spokes to the hub

## Conclusion
