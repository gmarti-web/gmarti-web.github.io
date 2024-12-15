---
title: PTW 310 audience analysis
last_modified_at: 2024-12-07
categories:
    - PTW310
excerpt: An audience analysis for my PTW310 portfolio project.
---

## Writer-centered analysis

| Gatekeepers |
|-------------|
| Carl Chatfield |
| Ratula Chakrabarti |

<table>
    <thead>
        <tr>
            <th></th>
            <th>Audience</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Tertiary</th>
            <td><ul>
                <li>Hobbyists</li>
                <li>Interested general public</li>
            </ul></td>
        </tr>
        <tr>
            <th>Secondary</th>
            <td><ul>
                <li>Engineering managers</li>
                <li>Cloud architects</li>
            </ul></td>
        </tr>
        <tr>
            <th>Primary</th>
            <td>Junior cloud engineers</td>
        </tr>
        <tr>
            <th>Writer</th>
            <td>Greg Martinez</td>
        </tr>
    </tbody>
</table>

## Reader analysis

<table>
    <thead>
        <tr>
            <th></th>
            <th>Needs</th>
            <th>Values</th>
            <th>Attitudes</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th>Primary</th>
            <td><ul>
                <li>Clear examples</li>
                <li>Visual aides</li>
                <li>Troubleshooting recommendations</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Few decision points</li>
            </ul></td>
            <td><ul>
                <li>Busy</li>
                <li>Task-oriented</li>
            </ul></td>
        </tr>
        <tr>
            <th>Secondary</th>
            <td><ul>
                <li>Clear use cases</li>
                <li>Resource architecture</li>
                <li>Approximate costs</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Technical accuracy</li>
                <li>Client satisfaction</li>
                <li>Cost efficiency</li>
            </ul></td>
            <td><ul>
                <li>Skeptical</li>
                <li>Busy</li>
            </ul></td>
        </tr>
        <tr>
            <th>Tertiary</th>
            <td><ul>
                <li>Clear examples</li>
                <li>Visual aides</li>
                <li>Conceptual background</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Lack of technical jargon</li>
            </ul></td>
            <td><ul>
                <li>Open-minded</li>
                <li>Curious</li>
            </ul></td>
        </tr>
        <tr>
            <th>Gatekeepers</th>
            <td><ul>
                <li>Well-written content</li>
                <li>Tight document structure</li>
                <li>Consistent style</li>
            </ul></td>
            <td><ul>
                <li>Clarity</li>
                <li>Clear process</li>
                <li>Logical thinking</li>
            </ul></td>
            <td><ul>
                <li>Optimistic</li>
                <li>Open-minded</li>
            </ul></td>
        </tr>
    </tbody>
</table>

## Reader context analysis

| | Physical context | Mobile context | Economic context | Ethical context |
|-|------------------|----------------|------------------|---------|
| **Primary readers** | Blog on the internet | Scales with the size of the reader's device. | Solving a client request | Is this the solution the client truly needs? |
| **Reader's organization** | Blog on the internet | Scales with the size of the reader's device. | Managing cloud costs | Does the client understand the pricing model for the solution? |
| **Reader's industry** | Blog on the internet | Scales with the size of the reader's device | Cost of training engineers | Environmental impact of maintaining cloud servers |

## Audience's desired outcome

The primary audience’s desired outcome is to satisfy their current and future clients.

Junior cloud engineers, the primary audience for this project, must deliver a service
to a client. And they know they must do so for other clients in the future. So,
they need a way to deliver this service without starting over from scratch. To
accomplish this, they can use a script multiple times with different configurations.
This way, they can satisfy any client that needs a web application platform with
minimal time and effort.

## Outline of deliverable

- Introduction
  - Background - Web applications in Azure
  - Purpose and scope
- Prerequisites
  - Create a free Azure account
  - Configure the Azure CLI
    - Download the CLI
    - Log into Azure
  - Set up a Terraform project
    - Install Terraform CLI
    - Install the Terraform VS Code extensions
    - Explore the Terraform Registry
- Create a virtual network (VNet)
  - Background
  - Create a VNet
  - Troubleshooting
  - Next section
  - Learn more
- Create a virtual machine (VM)
  - Background
  - Create a VM
  - Troubleshooting
  - Next section
  - Learn more
- Create an Azure SQL server
  - Background
  - Create a SQL server
  - Troubleshooting
  - Next section
  - Learn more
- Put it all together
  - Background
  - Connect the services
  - Troubleshooting
  - Next section
  - Learn more
- Conclusion
  - Review of resources created
  - How to delete resources
  - Explore other projects
- FAQs

