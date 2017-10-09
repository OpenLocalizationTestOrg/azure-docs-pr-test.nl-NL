Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.

[!INCLUDE [resource group intro text](resource-group.md)]

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

In het algemeen u uw resource groep en Hallo resources in een regio in de buurt. toosee ondersteunde locaties voor Azure Web Apps, Voer Hallo `az appservice list-locations` opdracht. 
