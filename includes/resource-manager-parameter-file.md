Als u een parameterwaarden bestand toopass parameter tijdens de implementatie gebruikt, moet u op toocreate een JSON-bestand met een indeling vergelijkbaar toohello voorbeeld te volgen:

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

Hallo-grootte van het parameterbestand Hallo mag niet meer dan 64 KB.

Als u tooprovide een gevoelige waarde moet een parameter (zoals een wachtwoord), voegt u die waarde tooa-sleutelkluis. Hallo sleutelkluis tijdens de implementatie, zoals weergegeven in het vorige voorbeeld Hallo ophalen. Zie voor meer informatie [beveiligde waarden doorgeven tijdens de implementatie van](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md). 

