## <a name="clean-up-deployment"></a><span data-ttu-id="a3911-101">Opschonen van de implementatie</span><span class="sxs-lookup"><span data-stu-id="a3911-101">Clean up deployment</span></span> 

<span data-ttu-id="a3911-102">Na het uitvoeren van het voorbeeldscript kan de volgende opdracht worden gebruikt voor het verwijderen van de resourcegroep, Azure Redis-Cache-exemplaar en verwante resources in de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a3911-102">After the script sample has been run, the follow command can be used to remove the resource group, Azure Redis Cache instance, and any related resources in the resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```