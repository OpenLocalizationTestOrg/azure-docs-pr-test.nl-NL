---
title: Resource Manager-sjabloon aaaExport met Azure CLI | Microsoft Docs
description: Gebruik Azure Resource Manager en Azure CLI tooexport een sjabloon van een resourcegroep.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a>Azure Resource Manager-sjablonen met Azure CLI exporteren

Resource Manager kunt u tooexport Resource Manager-sjabloon uit bestaande resources in uw abonnement. U kunt deze gegenereerde sjabloon toolearn over Hallo sjabloon syntaxis of tooautomate Hallo hergebruik van uw oplossing naar behoefte.

Het is belangrijk toonote dat er twee verschillende manieren tooexport een sjabloon zijn:

* Hallo werkelijke sjabloon die u voor een implementatie gebruikt, kunt u exporteren. Hallo geëxporteerde sjabloon bevat alle Hallo parameters en variabelen exact zo worden weergegeven in de oorspronkelijke sjabloon Hallo. Deze methode is handig wanneer u een sjabloon tooretrieve nodig.
* U kunt een sjabloon met de huidige status van de resourcegroep Hallo Hallo exporteren. Hallo geëxporteerde sjabloon is niet op basis van een sjabloon die u voor implementatie gebruikt. In plaats daarvan wordt een sjabloon die een momentopname van de resourcegroep Hallo is gemaakt. geëxporteerde sjabloon Hallo heeft veel vastgelegde waarden en waarschijnlijk niet zoveel parameters zoals u normaal gesproken zou definiëren. Deze methode is handig als u de resourcegroep Hallo hebt gewijzigd. Nu moet u toocapture Hallo resourcegroep als sjabloon.

Dit onderwerp bevat beide methoden.

## <a name="deploy-a-solution"></a>Een oplossing implementeren

tooillustrate, zowel voor het exporteren van een sjabloon nadert, u begint met het implementeren van een oplossing tooyour-abonnement. Als u al een resourcegroep in uw abonnement dat u wilt dat tooexport, hoeft u geen toodeploy deze oplossing. Hallo rest van dit artikel verwijst echter toohello sjabloon voor deze oplossing. Hallo-voorbeeldscript implementeert een opslagaccount.

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a>Sjabloon opslaan in de implementatiegeschiedenis

U kunt een sjabloon ophalen uit de implementatiegeschiedenis van een met behulp van Hallo [az implementatie exporteren](/cli/azure/group/deployment#export) opdracht. Hallo bespaart Hallo voorbeeldsjabloon die u eerder implementeert te volgen:

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

Het resultaat Hallo-sjabloon. Hallo JSON kopiëren en opslaan als een bestand. U ziet dat het Hallo exacte sjabloon die u voor implementatie gebruikt. Hallo-parameters en variabelen overeen met de Hallo sjabloon vanuit GitHub. U kunt deze sjabloon opnieuw implementeren.


## <a name="export-resource-group-as-template"></a>Resourcegroep exporteren als sjabloon

In plaats van een sjabloon worden opgehaald uit de implementatiegeschiedenis hello, kunt u een sjabloon die Hallo huidige status van een resourcegroep vertegenwoordigt met behulp van Hallo ophalen [exporteren az](/cli/azure/group#export) opdracht. U kunt deze opdracht gebruiken wanneer u veel wijzigingen tooyour-resourcegroep hebt aangebracht en er geen bestaande sjabloon alle Hallo wijzigingen vertegenwoordigt.

```azurecli
az group export --name ExampleGroup
```

Het resultaat Hallo-sjabloon. Hallo JSON kopiëren en opslaan als een bestand. U ziet dat deze anders dan Hallo-sjabloon in GitHub is. Bestaat uit verschillende parameters en geen variabelen. zijn de vastgelegde toovalues Hallo opslag SKU en locatie. Hallo volgende voorbeeld ziet u de geëxporteerde sjabloon hello, maar uw sjabloon is een iets andere parameternaam:

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

U kunt deze sjabloon kunt implementeren, maar het vereist raden een unieke naam voor het Hallo-opslagaccount. Hallo-naam van de parameter is enigszins anders.

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a>Geëxporteerde sjabloon aanpassen

U kunt deze sjabloon toomake wijzigen het toouse gemakkelijker en flexibeler. tooallow voor meer locaties, wijziging Hallo locatie-eigenschap toouse Hallo dezelfde locatie als Hallo resourcegroep:

```json
"location": "[resourceGroup().location]",
```

tooavoid met tooguess uniques naam voor het opslagaccount, verwijderen Hallo-parameter voor de opslagaccountnaam Hallo. Een parameter voor een achtervoegsel voor opslag en een opslag SKU toevoegen:

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

Een variabele die wordt gemaakt van de opslagaccountnaam Hallo met Hallo uniqueString functie toevoegen:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Hallo-naam van Hallo storage account toohello variabele instellen:

```json
"name": "[variables('storageAccountName')]",
```

Hallo SKU toohello parameter ingesteld:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

De sjabloon ziet er nu als volgt uit:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

Implementeer Hallo gewijzigde sjabloon opnieuw.

## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het gebruik van Hallo portal tooexport een sjabloon [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).
* toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).
* Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).