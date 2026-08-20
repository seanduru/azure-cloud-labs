# VMSS + Load Balancer Lab — CLI Commands

# Check VMSS Instances
az vmss list-instances \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --query "[].{InstanceId:instanceId,Name:name}" \
  -o table

# Scale VMSS from 2 to 3 Instances
az vmss scale \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --new-capacity 3

# Scale VMSS Back to 2 Instances
az vmss scale \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --new-capacity 2

# Check VMSS Configuration
az vmss show \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --query "{SKU:sku.name,Capacity:sku.capacity,UpgradePolicy:upgradePolicy.mode}" \
  -o table

# Change VMSS SKU
az vmss update \
  --resource-group vmss-lab-rg \
  --name vmss-lab-vmss \
  --vm-sku Standard_F1als_v7

# Create Load Balancer Health Probe
az network lb probe create \
  --resource-group vmss-lab-rg \
  --lb-name vmss-lab-vmssLB \
  --name HTTPProbe \
  --protocol Tcp \
  --port 80 \
  --interval 5 \
  --threshold 2

# Attach Health Probe to Load Balancing Rule
az network lb rule update \
  --resource-group vmss-lab-rg \
  --lb-name vmss-lab-vmssLB \
  --name LBRule \
  --probe HTTPProbe

# Install Nginx on VMSS Instances
az vm run-command invoke \
  --resource-group vmss-lab-rg \
  --name <VMSS-INSTANCE-NAME> \
  --command-id RunShellScript \
  --scripts "sudo apt-get update && sudo apt-get install -y nginx && sudo systemctl enable --now nginx"

# Verify Nginx is Listening on Port 80
az vm run-command invoke \
  --resource-group vmss-lab-rg \
  --name <VMSS-INSTANCE-NAME> \
  --command-id RunShellScript \
  --scripts "sudo ss -tlnp | grep ':80 '"

# Check NSG Rules
az network nsg rule list \
  --resource-group vmss-lab-rg \
  --nsg-name vmss-lab-vmssNSG \
  --query "[].{Name:name,Priority:priority,Direction:direction,Access:access,Protocol:protocol,Source:sourceAddressPrefix,DestPort:destinationPortRange}" \
  -o table

# Test Load Balancer
curl http://<LOAD-BALANCER-PUBLIC-IP>

# Lab Flow
# Internet → Public IP → Azure Load Balancer → Backend Pool → VMSS Instances → Nginx
