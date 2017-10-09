<span data-ttu-id="721a6-101">Als u een parameterwaarden bestand toopass parameter tijdens de implementatie gebruikt, moet u op toocreate een JSON-bestand met een indeling vergelijkbaar toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="721a6-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

<span data-ttu-id="721a6-102">Hallo-grootte van het parameterbestand Hallo mag niet meer dan 64 KB.</span><span class="sxs-lookup"><span data-stu-id="721a6-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="721a6-103">Als u tooprovide een gevoelige waarde moet een parameter (zoals een wachtwoord), voegt u die waarde tooa-sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="721a6-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="721a6-104">Hallo sleutelkluis tijdens de implementatie, zoals weergegeven in het vorige voorbeeld Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="721a6-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="721a6-105">Zie voor meer informatie [beveiligde waarden doorgeven tijdens de implementatie van](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span><span class="sxs-lookup"><span data-stu-id="721a6-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

