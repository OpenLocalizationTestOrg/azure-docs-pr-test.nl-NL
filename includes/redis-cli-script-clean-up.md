## <a name="clean-up-deployment"></a><span data-ttu-id="fae95-101">Opschonen van implementatie</span><span class="sxs-lookup"><span data-stu-id="fae95-101">Clean up deployment</span></span> 

<span data-ttu-id="fae95-102">Na het uitvoeren van het voorbeeldscript Hallo is Hallo Volg opdracht gebruikte tooremove Hallo-resourcegroep, Azure Redis-Cache-exemplaar en gerelateerde bronnen in de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="fae95-102">After hello script sample has been run, hello follow command can be used tooremove hello resource group, Azure Redis Cache instance, and any related resources in hello resource group.</span></span>

```azurecli
az group delete --name contosoGroup
```