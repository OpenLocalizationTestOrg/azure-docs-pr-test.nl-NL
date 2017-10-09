<span data-ttu-id="6bb79-101">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="6bb79-101">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [resource group intro text](resource-group.md)]

<span data-ttu-id="6bb79-102">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *westeurope* locatie.</span><span class="sxs-lookup"><span data-stu-id="6bb79-102">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="6bb79-103">In het algemeen u uw resource groep en Hallo resources in een regio in de buurt.</span><span class="sxs-lookup"><span data-stu-id="6bb79-103">You generally create your resource group and hello resources in a region near you.</span></span> <span data-ttu-id="6bb79-104">toosee ondersteunde locaties voor Azure Web Apps, Voer Hallo `az appservice list-locations` opdracht.</span><span class="sxs-lookup"><span data-stu-id="6bb79-104">toosee all supported locations for Azure Web Apps, run hello `az appservice list-locations` command.</span></span> 
