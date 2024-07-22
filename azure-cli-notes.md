# Creating a VM with az cli
$ az vm create \
 --resource-group "test-resource" \
 --name test-vm \
 --public-ip-sku Standard \
 --image Ubuntu2204 \
 --admin-username azureuser \
 --generate-ssh-keys

# create resource group 
az group create --name mylab --location canadacentral --account "Free trial"


# Create virtual network
az network vnet create --resource-group mylab --name MyNet --address-prefix 10.0.0.0/16 --location canadacentral --subnet-name AzureFirewallSubnet --subnet-prefixes 10.0.2.0/26



# Firewall
az network firewall create -g mylab -l \
canadacentral -z 1 -n MyFirewall --sku AZFW_VNet \
--tier Standard --vnet-name MyNet \
--conf-name MyIpConfig \
--m-conf-name MyManagementIpConfig \
--m-public-ip MyPublicIp

----------------------------------------------------
# List the network
$ az network nsg list --resource-group "learn-8725891f-f0d0-4665-a4b1-21a1a2ce4d27" --query '[].name' --output tsv

# Show the network security group rules
$ az network nsg rule list --resource-group "learn-8725891f-f0d0-4665-a4b1-21a1a2ce4d27" --nsg-name my-vmNSG --query '[].{Name:name, Priority:priority, Port:destinationPortRange, Access:access}' --output table

# Run the following az network nsg rule create command to create a rule called allow-http that allows inbound access on port 80:
$ az network nsg rule create --resource-group "learn-8725891f-f0d0-4665-a4b1-21a1a2ce4d27" --nsg-name my-vmNSG --name allow-http --protocol tcp --priority 100 --destination-port-range 80 --access Allow
