<span data-ttu-id="cc108-101">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="cc108-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="cc108-102">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.</span><span class="sxs-lookup"><span data-stu-id="cc108-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="cc108-103">toosee hello beschikbare locaties, Voer Hallo `az appservice list-locations` opdracht.</span><span class="sxs-lookup"><span data-stu-id="cc108-103">toosee hello available locations, run hello `az appservice list-locations` command.</span></span> <span data-ttu-id="cc108-104">In het algemeen maakt u resources in een regio bij u in de buurt.</span><span class="sxs-lookup"><span data-stu-id="cc108-104">You generally create resources in a region near you.</span></span>
