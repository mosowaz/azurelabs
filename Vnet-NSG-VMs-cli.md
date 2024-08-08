
### 1. Create a resource group
```az group create --name test-rg --location canadacentral```

### 2. Create a virtual network and subnet
```
az network vnet create \
    --name vnet-1 \
    --resource-group test-rg \
    --address-prefix 10.0.0.0/16 \
    --subnet-name subnet-1 \
    --subnet-prefixes 10.0.0.0/24
```

### 3. Deploy AzureBastionSubnet, create public IP, and create a Bastion host in AzureBastionSubnet
```
az network vnet subnet create \
    --name AzureBastionSubnet \
    --resource-group test-rg \
    --vnet-name vnet-1 \
    --address-prefix 10.0.1.0/26

az network public-ip create \
    --resource-group test-rg \
    --name public-ip \
    --sku Standard \
    --location eastus2 \
    --zone 1 2 3

az network bastion create \
    --name bastion \
    --public-ip-address public-ip \
    --resource-group test-rg \
    --vnet-name vnet-1 \
    --location eastus2
```

### 4. Create 2 Linux VMs for test in the subnet-1 subnet
```
az vm create \
    --resource-group test-rg \
    --admin-username azureuser \
    --authentication-type password \
    --name vm-1 \
    --image Ubuntu2204 \
    --public-ip-address ""

az vm create \
    --resource-group test-rg \
    --admin-username azureuser \
    --authentication-type password \
    --name vm-2 \
    --image Ubuntu2204 \
    --public-ip-address ""
```

## Clean up resources
```az group delete --name test-rg --yes```

