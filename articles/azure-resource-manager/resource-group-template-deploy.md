---
title: resources met PowerShell en de sjabloon aaaDeploy | Microsoft Docs
description: Azure Resource Manager en Azure PowerShell toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 55903f35-6c16-4c6d-bf52-dbf365605c3f
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 41506811ba3c2ea5df6313db70978ade50f71161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-powershell"></a>Resources implementeren met Resource Manager-sjablonen en Azure PowerShell

Dit onderwerp wordt uitgelegd hoe toouse Azure PowerShell met Resource Manager-sjablonen toodeploy uw tooAzure resources. Als u niet bekend met het Hallo-concepten voor het implementeren bent en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).

Hallo Resource Manager-sjabloon die u implementeert, kan een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een zoals GitHub-opslagplaats. Hallo-sjabloon die u in dit artikel implementeert is beschikbaar in Hallo [voorbeeldsjabloon](#sample-template) sectie, of als [storage accountsjabloon in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

<a id="deploy-local-template" />

## <a name="deploy-a-template-from-your-local-machine"></a>Een sjabloon implementeren vanuit uw lokale computer

Bij het implementeren van resources tooAzure, u:

1. Meld u bij tooyour Azure-account
2. Maak een resourcegroep die als Hallo-container voor resources Hallo geïmplementeerd fungeert. Hallo-naam van de resourcegroep Hallo kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten. Het kan zijn van too90 tekens. Het mag niet eindigen op een punt.
3. Toohello resource groep Hallo-sjabloon die Hallo resources toocreate definieert implementeren

Een sjabloon kan parameters die u in staat toocustomize Hallo implementatie stellen bevatten. U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie). Hallo-voorbeeldsjabloon definieert een parameter voor het opslagaccount Hallo SKU.

Hallo volgende voorbeeld maakt een resourcegroep en implementeert een sjabloon op basis van uw lokale computer:

```powershell
Login-AzureRmAccount
 
New-AzureRmResourceGroup -Name ExampleResourceGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Hallo-implementatie kan toocomplete van enkele minuten duren. Wanneer deze is voltooid, ziet u een bericht met Hallo resultaat:

```powershell
ProvisioningState       : Succeeded
```

## <a name="deploy-a-template-from-an-external-source"></a>Een sjabloon implementeren vanuit een externe bron

In plaats van Resource Manager-sjablonen worden opgeslagen op uw lokale computer, kunt u desgewenst toostore ze in een externe locatie. U kunt sjablonen opslaan in een resourcebeheerbibliotheek (zoals GitHub). Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.

toodeploy een externe-sjabloon gebruiken Hallo **TemplateUri** parameter. Gebruik hello URI in Hallo voorbeeld toodeploy Hallo voorbeeldsjabloon vanuit GitHub.

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -storageAccountType Standard_GRS
```

Hallo voorgaande voorbeeld vereist een openbaar toegankelijke URI voor Hallo-sjabloon voor de meeste scenario werkt, omdat de sjabloon mag geen gevoelige gegevens bevatten. Als u moet toospecify gevoelige gegevens (zoals een beheerderswachtwoord), wordt die waarde als beveiligde parameter doorgeven. Echter, als u niet wilt dat uw sjabloon toobe openbaar toegankelijk is, kunt u deze beschermen door op te slaan deze in een container particuliere opslag. Zie voor meer informatie over het implementeren van een sjabloon waarvoor een shared access signature (SAS)-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).

## <a name="parameter-files"></a>De parameterbestanden

In plaats van met parameters wordt doorgegeven als inline-waarden in het script, soms is het eenvoudiger toouse een JSON-bestand met de Hallo parameterwaarden. Hallo parameterbestand moet Hallo na indeling zijn:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
     "storageAccountType": {
         "value": "Standard_GRS"
     }
  }
}
```

U ziet dat de sectie parameters Hallo een parameternaam die overeenkomt met de Hallo parameter die is gedefinieerd in de sjabloon (storageAccountType) bevat. Hallo parameterbestand bevat een waarde voor parameter Hallo. Deze waarde wordt automatisch toohello sjabloon doorgegeven tijdens de implementatie. U kunt meerdere parameterbestanden voor verschillende scenario's maken en geeft u de juiste parameterbestand Hallo. 

Hallo voorgaande voorbeeld kopiëren en opslaan als een bestand met de naam `storage.parameters.json`.

een lokale parameterbestand toopass gebruiken Hallo **TemplateParameterFile** parameter:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json `
  -TemplateParameterFile c:\MyTemplates\storage.parameters.json
```

een externe parameterbestand toopass gebruiken Hallo **TemplateParameterUri** parameter:

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json `
  -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.parameters.json
```

U kunt de parameters inline gebruiken en een lokale parameter bestand Hallo dezelfde bewerking voor implementatie. U kunt bijvoorbeeld waarden opgeven in de lokale parameterbestand Hallo en andere waarden inline toevoegen tijdens de implementatie. Als u waarden voor een parameter in zowel de lokale parameterbestand Hallo als inline opgeven, voorrang Hallo inline.

Echter, wanneer u een parameterbestand externe gebruikt, u kunt niet doorgeven andere waarden beide inline of vanuit een lokaal bestand. Wanneer u een parameterbestand opgeeft in Hallo **TemplateParameterUri** parameter, alle inline parameters worden genegeerd. Alle parameterwaarden in het externe bestand Hallo opgeven. Als de sjabloon een gevoelige waarde die u niet opnemen in het parameterbestand hello bevat, voeg die waarde tooa-sleutelkluis of dynamisch bieden alle parameter waarden inline.

Als de sjabloon een parameter met dezelfde naam als een van de parameters in de PowerShell-opdracht Hallo Hallo hello bevat, PowerShell biedt Hallo-parameter van uw sjabloon Hallo postfix **FromTemplate**. Bijvoorbeeld, een parameter genaamd **ResourceGroupName** in uw sjabloon is in strijd met Hallo **ResourceGroupName** parameter in Hallo [New-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment)cmdlet. U bent na vragen aan gebruiker tooprovide een waarde voor **ResourceGroupNameFromTemplate**. In het algemeen voorkomt u deze verwarring door te geven geen parameters met Hallo dezelfde naam als parameters die worden gebruikt voor implementatiebewerkingen.

## <a name="test-a-template-deployment"></a>Een sjabloonimplementatie testen

tootest uw sjabloon en de parameterbestanden waarden zonder het distribueren van alle resources gebruiken [Test-AzureRmResourceGroupDeployment](/powershell/module/azurerm.resources/test-azurermresourcegroupdeployment). 

```powershell
Test-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleResourceGroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType Standard_GRS
```

Als er geen fouten worden aangetroffen, wordt Hallo-opdracht is voltooid zonder reactie. Als er een fout wordt gedetecteerd, retourneert Hallo opdracht een foutbericht weergegeven. Poging een onjuiste waarde voor het opslagaccount Hallo SKU, toopass retourneert bijvoorbeeld Hallo volgende fout:

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName testgroup `
  -TemplateFile c:\MyTemplates\storage.json -storageAccountType badSku

Code    : InvalidTemplate
Message : Deployment template validation failed: 'hello provided value 'badSku' for hello template parameter 'storageAccountType'
          at line '15' and column '24' is not valid. hello parameter value is not part of hello allowed value(s):
          'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.
Details :
```

Als uw sjabloon een syntaxisfout heeft, foutmelding Hallo opdracht een die aangeeft dat Hallo sjabloon kan niet worden geparseerd. Hallo-bericht geeft aan Hallo regelnummer en positie van Hallo parseerfout.

```powershell
Test-AzureRmResourceGroupDeployment : After parsing a value an unexpected character was encountered: 
  ". Path 'variables', line 31, position 3.
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse voltooid modus gebruik Hallo `Mode` parameter:

```powershell
New-AzureRmResourceGroupDeployment -Mode Complete -Name ExampleDeployment `
  -ResourceGroupName ExampleResourceGroup -TemplateFile c:\MyTemplates\storage.json 
```

## <a name="sample-template"></a>Voorbeeldsjabloon

Hallo wordt volgende sjabloon gebruikt voor het Hallo-voorbeelden in dit onderwerp. Kopiëren en opslaan als een bestand met de naam storage.json. toounderstand hoe toocreate deze sjabloon Zie [maken van uw eerste Azure Resource Manager-sjabloon](resource-manager-create-first-template.md).  

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccountType": {
      "type": "string",
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS",
        "Premium_LRS"
      ],
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "sku": {
          "name": "[parameters('storageAccountType')]"
      },
      "kind": "Storage", 
      "properties": {
      }
    }
  ],
  "outputs": {
      "storageAccountName": {
          "type": "string",
          "value": "[variables('storageAccountName')]"
      }
  }
}
```

## <a name="next-steps"></a>Volgende stappen
* Hallo-voorbeelden in dit artikel implementeren resources tooa-resourcegroep in uw standaardabonnement. Zie voor een ander abonnement toouse [meerdere Azure-abonnementen beheren](/powershell/azure/manage-subscriptions-azureps).
* Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [script voor implementatie van Resource Manager-sjabloon](resource-manager-samples-powershell-deploy.md).
* hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).
* Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-powershell-sas-token.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

