Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.

[!INCLUDE [resource group intro text](resource-group.md)]

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

toosee hello beschikbare locaties, Voer Hallo `az appservice list-locations` opdracht. In het algemeen maakt u resources in een regio bij u in de buurt.
