# Azure VM + Nginx Web Server Lab

## Overview

Hands-on Azure IaaS lab focused on deploying, configuring, and managing a Linux virtual machine using the Azure Portal and Azure CLI.

## What I Built

* Deployed an Ubuntu 24.04 LTS virtual machine in Azure
* Created an Azure Virtual Network and subnet
* Configured a Network Interface (NIC)
* Configured a public IP address
* Configured a Network Security Group (NSG)
* Allowed inbound SSH (TCP 22) for administration
* Allowed inbound HTTP (TCP 80) for web traffic
* Connected to the VM using SSH
* Installed and configured Nginx
* Created a custom HTML webpage
* Verified the web server locally using `curl`
* Verified the webpage through the VM's public IP
* Managed and inspected the VM using Azure CLI

## Architecture

```text
Internet
    |
    v
Public IP
52.188.15.119
    |
    v
Network Interface (NIC)
Private IP: 172.16.0.4
    |
    v
Network Security Group
- SSH / TCP 22
- HTTP / TCP 80
    |
    v
VNet: 172.16.0.0/16
    |
    v
Subnet: 172.16.0.0/24
    |
    v
Ubuntu 24.04 VM
    |
    v
Nginx
    |
    v
Custom HTML Webpage
```

## Azure Resources

| Resource           | Configuration           |
| ------------------ | ----------------------- |
| Resource Group     | `sean-arm-lab`          |
| VM                 | `sean-az104-vm01`       |
| Region             | East US                 |
| VM Size            | `Standard_D2als_v7`     |
| OS                 | Ubuntu Server 24.04 LTS |
| VNet               | `vnet-eastus-1`         |
| VNet Address Space | `172.16.0.0/16`         |
| Subnet             | `snet-eastus-1`         |
| Subnet Range       | `172.16.0.0/24`         |
| Private IP         | `172.16.0.4`            |
| Public IP          | `52.188.15.119`         |
| NSG                | `sean-az104-vm01-nsg`   |
| Web Server         | Nginx                   |

## Network Security

The NSG was configured with the following inbound rules:

| Rule       | Priority | Protocol | Port | Access |
| ---------- | -------: | -------- | ---: | ------ |
| SSH        |      300 | TCP      |   22 | Allow  |
| Allow-HTTP |      310 | TCP      |   80 | Allow  |

SSH allows remote administration of the Ubuntu VM, while HTTP allows users to access the Nginx web server.

## Azure CLI Management

I practiced using Azure CLI to inspect and manage the deployed infrastructure, including:

```bash
# Check VM status
az vm get-instance-view \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01

# Stop the VM
az vm stop \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01

# Start the VM
az vm start \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01

# Inspect the VM
az vm show \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01 \
  --show-details

# Inspect the NIC
az network nic show \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01900

# List NSG rules
az network nsg rule list \
  --resource-group sean-arm-lab \
  --nsg-name sean-az104-vm01-nsg

# Inspect the VNet
az network vnet show \
  --resource-group sean-arm-lab \
  --name vnet-eastus-1

# List public IPs
az network public-ip list \
  --resource-group sean-arm-lab
```

## Nginx Configuration

After connecting to the Ubuntu VM through SSH, I installed Nginx and verified that it was running locally:

```bash
curl localhost
```

I then modified the default Nginx webpage to create a custom page:

```html
<h1>Sean's Azure Cloud Lab</h1>

<p>Running on an Ubuntu VM in Azure.</p>

<p>Hosted with Nginx.</p>
```

The webpage was successfully accessible through the VM's public IP over HTTP.

## Key Concepts Learned

* Azure Virtual Machines
* Azure Virtual Networks
* Subnets and CIDR address ranges
* Network Interfaces (NICs)
* Public vs. private IP addresses
* Network Security Groups (NSGs)
* Inbound vs. outbound traffic
* SSH administration
* HTTP traffic
* Linux VM administration
* Nginx web servers
* Azure CLI
* VM lifecycle management
* Azure IaaS architecture

## Outcome

Successfully deployed and managed an Ubuntu based Azure VM and hosted a custom Nginx webpage accessible through the internet.

This lab was completed as part of my hands on preparation for the **Microsoft Azure Administrator (AZ-104)** certification.
