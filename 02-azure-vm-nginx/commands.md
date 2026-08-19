# Azure VM + Nginx Lab — Azure CLI Commands

These are the primary Azure CLI commands used to deploy, manage, and inspect the Azure VM and its networking resources.

## VM Management

### Check VM status

```bash
az vm get-instance-view \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01 \
  --query "instanceView.statuses[1].displayStatus" \
  --output tsv
```

### Start the VM

```bash
az vm start \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01
```

### Stop the VM

```bash
az vm stop \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01
```

### View VM details

```bash
az vm show \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01 \
  --show-details \
  --query "{VM:name, Location:location, Size:hardwareProfile.vmSize, PublicIP:publicIps, PrivateIP:privateIps, PowerState:powerState}" \
  --output table
```

## Network Interface

### Find the NIC attached to the VM

```bash
az vm nic list \
  --resource-group sean-arm-lab \
  --vm-name sean-az104-vm01 \
  --query "[].id" \
  --output tsv
```

### Inspect the NIC

```bash
az network nic show \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01900 \
  --query "{NIC:name, PrivateIP:ipConfigurations[0].privateIPAddress, VNet:ipConfigurations[0].subnet.id, NSG:networkSecurityGroup.id}" \
  --output table
```

## Network Security Group

### List NSG rules

```bash
az network nsg rule list \
  --resource-group sean-arm-lab \
  --nsg-name sean-az104-vm01-nsg \
  --output table
```

The custom inbound rules created for the lab were:

* SSH — TCP 22 — Allow
* HTTP — TCP 80 — Allow

## Virtual Network

### View the VNet address space

```bash
az network vnet show \
  --resource-group sean-arm-lab \
  --name vnet-eastus-1 \
  --query "addressSpace.addressPrefixes" \
  --output tsv
```

### List VNet subnets

```bash
az network vnet subnet list \
  --resource-group sean-arm-lab \
  --vnet-name vnet-eastus-1 \
  --output table
```

### View subnet details

```bash
az network vnet subnet show \
  --resource-group sean-arm-lab \
  --vnet-name vnet-eastus-1 \
  --name snet-eastus-1 \
  --output json
```

## Public IP

### List public IP resources

```bash
az network public-ip list \
  --resource-group sean-arm-lab \
  --output table
```

## SSH Connection

The VM was accessed remotely using Azure CLI:

```bash
az ssh vm \
  --resource-group sean-arm-lab \
  --name sean-az104-vm01
```

## Linux / Nginx

After connecting to the Ubuntu VM, Nginx was installed and tested locally.

### Test Nginx

```bash
curl localhost
```

### Edit the Nginx default webpage

```bash
sudo nano /var/www/html/index.nginx-debian.html
```

The default page was replaced with a custom HTML page for the Azure lab.

## Lab Architecture

```text
Internet
    |
    v
Public IP
    |
    v
Network Interface
    |
    v
Network Security Group
    |
    v
VNet
    |
    v
Subnet
    |
    v
Ubuntu VM
    |
    v
Nginx Web Server
```
