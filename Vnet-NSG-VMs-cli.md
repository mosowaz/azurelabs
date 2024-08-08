
###Create a resource group
```az group create --name test-rg --location canadacentral```

###Create a virtual network and subnet
```
az network vnet create \
    --name vnet-1 \
    --resource-group test-rg \
    --address-prefix 10.0.0.0/16 \
    --subnet-name subnet-1 \
    --subnet-prefixes 10.0.0.0/24
```
