# Azure VM Scale Set + Load Balancer Lab

## Overview

Built an Azure Virtual Machine Scale Set (VMSS) with multiple Linux VM instances behind an Azure Load Balancer.

The lab focused on:

- VM Scale Sets
- Horizontal scaling
- VM SKU/size management
- Azure compute quotas
- Load balancer backend pools
- Health probes
- Network Security Groups (NSGs)
- HTTP traffic
- Nginx web servers

## Architecture

Internet
   |
   v
Azure Public IP
   |
   v
Azure Load Balancer
   |
   +---- VMSS Instance 1
   |
   +---- VMSS Instance 2

## What I Did

### 1. Created the VM Scale Set

Created a Linux VM Scale Set in East US with two instances.

- Ubuntu 22.04
- 2 VM instances
- Flexible orchestration
- Azure Load Balancer
- Standard SKU

### 2. Tested Horizontal Scaling

Scaled the VMSS from 2 instances to 3:

```bash
az vmss scale \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --new-capacity 3
Then scaled back down to 2 instances.
