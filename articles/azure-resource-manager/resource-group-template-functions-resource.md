---
title: aaaAzure Resource Manager-sjabloonfuncties - resources | Microsoft Docs
description: Beschrijft Hallo functies toouse in een Azure Resource Manager sjabloon tooretrieve waarden over bronnen.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a>Resource-functies voor Azure Resource Manager-sjablonen

Resource Manager biedt Hallo functies voor het ophalen van waarden van de resource te volgen:

* [listKeys en de lijst {Value}](#listkeys)
* [providers](#providers)
* [verwijzing](#reference)
* [resourceGroup](#resourcegroup)
* [resourceId](#resourceid)
* [abonnement](#subscription)

tooget waarden van parameters, variabelen of de huidige implementatie hello, Zie [implementatie waarde functies](resource-group-template-functions-deployment.md).

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a>listKeys en de lijst {Value}
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

Retourneert Hallo waarden voor elk resourcetype die ondersteuning biedt voor bewerking Hallo-lijst. de meest voorkomende gebruik Hallo is `listKeys`. 

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| resourceName of resourceIdentifier |Ja |Tekenreeks |De unieke id voor Hallo resource. |
| apiVersion |Ja |Tekenreeks |API-versie van de status van de runtime. Normaal gesproken in Hallo-indeling, **jjjj-mm-dd**. |

### <a name="return-value"></a>Retourwaarde

Hallo geretourneerd object op basis van listKeys heeft Hallo volgende indeling:

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

Andere functies van de lijst met hebben verschillende retour-indelingen. toosee hello indeling van een functie, opnemen in Hallo uitvoer sectie zoals weergegeven in het Hallo-voorbeeldsjabloon. 

### <a name="remarks"></a>Opmerkingen

Een bewerking die met begint **lijst** kan worden gebruikt als een functie in uw sjabloon. Hallo beschikbare bewerkingen zijn niet alleen listKeys, maar ook bewerkingen, zoals `list`, `listAdminKeys`, en `listStatus`. U kunt geen echter gebruiken **lijst** bewerkingen uit waarbij de waarden in Hallo aanvraagtekst. Bijvoorbeeld, Hallo [lijst Account-SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) bewerking moet de aanvraag hoofdtekst parameters, zoals *signedExpiry*, zodat u deze niet binnen een sjabloon gebruiken.

toodetermine welke resourcetypen er een lijstbewerking, hebt u Hallo volgende opties:

* Weergave Hallo [REST-API-bewerkingen](/rest/api/) voor een resourceprovider en zoekt u bewerkingen na opvragen. Storage-accounts bijvoorbeeld Hallo [listKeys bewerking](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).
* Gebruik Hallo [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell-cmdlet. Hallo wordt volgende voorbeeld alle bewerkingen na opvragen voor storage-accounts:

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* Hallo na toofilter alleen bewerkingen na opvragen hello Azure CLI-opdracht gebruiken:

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

Hallo resource opgeven met behulp van beide Hallo [resourceId functie](#resourceid), of de indeling Hallo `{providerNamespace}/{resourceType}/{resourceName}`.


### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u hoe tooreturn Hallo primaire en secundaire sleutels van een opslagaccount in Hallo sectie levert.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a>providers
`providers(providerNamespace, [resourceType])`

Retourneert informatie over een resourceprovider en de volgende resourcetypen ondersteund. Als u een resourcetype niet opgeeft, Hallo alle Hallo ondersteunde typen voor Hallo resourceprovider geretourneerd.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| providerNamespace |Ja |Tekenreeks |Namespace van Hallo-provider |
| resourceType |Nee |Tekenreeks |Hallo type bron binnen Hallo opgegeven naamruimte. |

### <a name="return-value"></a>Retourwaarde

Elk type ondersteunde wordt geretourneerd als Hallo volgende indeling: 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

Matrix ordening van Hallo geretourneerd waarden kan niet worden gegarandeerd.

### <a name="example"></a>Voorbeeld

Hallo volgende voorbeeld ziet u hoe toouse Hallo provider functie:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a>Verwijzing
`reference(resourceName or resourceIdentifier, [apiVersion])`

Retourneert een object dat de runtimestatus van de bron.

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| resourceName of resourceIdentifier |Ja |Tekenreeks |Naam of de unieke id van een resource. |
| apiVersion |Nee |Tekenreeks |API-versie van Hallo van de opgegeven bron. Deze parameter bevatten wanneer Hallo resource niet binnen dezelfde sjabloon ingericht is. Normaal gesproken in Hallo-indeling, **jjjj-mm-dd**. |

### <a name="return-value"></a>Retourwaarde

Elk resourcetype retourneert verschillende eigenschappen voor de functie voor Hallo-verwijzing. Hallo-functie retourneert een enkele, vooraf gedefinieerde indeling. toosee hello eigenschappen voor een brontype retourneren Hallo-object in Hallo levert sectie zoals weergegeven in Hallo-voorbeeld.

### <a name="remarks"></a>Opmerkingen

Hallo verwijzing functie is afgeleid van de waarde van een runtimestatus en daarom niet worden gebruikt in de sectie met sjabloonvariabelen Hallo. Het kan worden gebruikt in het gedeelte van de uitvoer van een sjabloon. 

Hallo verwijzing functie impliciet kunt declareren u één resource afhankelijk is van een andere bron, als resource Hallo waarnaar wordt verwezen is ingericht binnen dezelfde sjabloon. U hoeft niet tooalso gebruik Hallo dependsOn eigenschap. Hallo wordt functie niet geëvalueerd als hello resource waarnaar wordt verwezen heeft implementatie voltooid.

Hallo toosee namen en waarden voor een resourcetype, maakt een sjabloon die Hallo-object als resultaat geeft in Hallo uitvoer sectie. Als er een bestaande resource van dat type is, retourneert de sjabloon Hallo object zonder eventuele nieuwe resources implementeren. 

Normaal gesproken gebruikt u Hallo **verwijzing** werken tooreturn een bepaalde waarde van een object, zoals het blobeindpunt Hallo URI of een volledig gekwalificeerde domeinnaam.

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a>Voorbeeld

naslaginformatie en toodeploy Hallo-bron in Hallo dezelfde sjabloon gebruikt:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

Hallo volgende voorbeeld verwijst naar een opslagaccount dat niet is geïmplementeerd in deze sjabloon. Hallo storage-account bestaat al binnen Hallo dezelfde resourcegroep.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a>resourceGroup
`resourceGroup()`

Retourneert een object dat de huidige resourcegroep Hallo vertegenwoordigt. 

### <a name="return-value"></a>Retourwaarde

Hallo geretourneerd object bevindt zich in de volgende indeling Hallo:

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a>Opmerkingen

Wordt vaak gebruikt van Hallo resourceGroup functie toocreate bronnen in Hallo dezelfde locatie als Hallo resourcegroep. Hallo volgende voorbeeld wordt Hallo locatie tooassign Hallo locatie voor resourcegroep voor een website.

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a>Voorbeeld

Hallo retourneert volgende sjabloon Hallo-eigenschappen van de resourcegroep Hallo.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a>resourceId
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

Retourneert Hallo de unieke id van een resource. U deze functie gebruiken wanneer Hallo bronnaam niet eenduidig of niet ingericht binnen Hallo is dezelfde sjabloon. 

### <a name="parameters"></a>Parameters

| Parameter | Vereist | Type | Beschrijving |
|:--- |:--- |:--- |:--- |
| subscriptionId |Nee |tekenreeks (In GUID-indeling) |Standaardwaarde is Hallo huidige abonnement. Deze waarde opgeven wanneer u een resource in een ander abonnement tooretrieve nodig. |
| resourceGroupName |Nee |Tekenreeks |Standaardwaarde is de huidige resourcegroep. Deze waarde opgeven wanneer u een resource in een andere resourcegroep tooretrieve nodig. |
| resourceType |Ja |Tekenreeks |Type resource, met inbegrip van de naamruimte van de resource-provider. |
| resourceName1 |Ja |Tekenreeks |Naam van de resource. |
| resourceName2 |Nee |Tekenreeks |Volgende naam resourcesegment als bron is genest. |

### <a name="return-value"></a>Retourwaarde

Hallo-id wordt in de volgende indeling Hallo geretourneerd:

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a>Opmerkingen

Hallo parameterwaarden die u opgeeft afhankelijk van of Hallo resource in Hallo is hetzelfde abonnement en de resource-groep als de huidige implementatie Hallo.

tooget hello resource-ID voor een opslagaccount in Hallo hetzelfde abonnement en resourcegroep gebruiken:

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello resource-ID voor een opslagaccount in Hallo hetzelfde abonnement, maar een andere resourcegroep, gebruiken:

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello resource-ID voor een opslagaccount in een ander abonnement en resourcegroep gebruiken:

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

tooget hello resource-ID voor een database in een andere resourcegroep gebruikt:

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

Vaak het geval is, moet u toouse deze functie wanneer u een opslagaccount of een virtueel netwerk in een andere resourcegroep. Hallo volgende voorbeeld ziet u hoe een resource van een externe resourcegroep gemakkelijk kan worden gebruikt:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a>Voorbeeld

Hallo retourneert volgende voorbeeld Hallo resource-ID voor een opslagaccount in de resourcegroep Hallo:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:

| Naam | Type | Waarde |
| ---- | ---- | ----- |
| sameRGOutput | Tekenreeks | /Subscriptions/{Current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentRGOutput | Tekenreeks | /Subscriptions/{Current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| differentSubOutput | Tekenreeks | /Subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage |
| nestedResourceOutput | Tekenreeks | /Subscriptions/{Current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/servername/databases/databaseName |

<a id="subscription" />

## <a name="subscription"></a>abonnement
`subscription()`

Retourneert details over Hallo abonnement voor de huidige implementatie Hallo. 

### <a name="return-value"></a>Retourwaarde

Hallo-functie retourneert Hallo volgende indeling:

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a>Voorbeeld

Hallo ziet volgende voorbeeld Hallo abonnement functie die in Hallo uitvoer sectie. 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a>Volgende stappen
* Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).
* een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).
* toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

