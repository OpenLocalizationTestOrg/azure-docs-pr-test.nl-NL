---
title: resources met Azure CLI en sjabloon aaaDeploy | Microsoft Docs
description: Azure Resource Manager en Azure CLI toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 493b7932-8d1e-4499-912c-26098282ec95
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/31/2017
ms.author: tomfitz
ms.openlocfilehash: 9f8bb9a8720399390a407030d2d32bcd97d32f13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-azure-cli"></a>Resources implementeren met Resource Manager-sjablonen en Azure CLI

Dit onderwerp wordt uitgelegd hoe toouse Azure CLI 2.0 met Resource Manager-sjablonen toodeploy uw tooAzure resources. Als u niet bekend met het Hallo-concepten voor het implementeren bent en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md).  

Hallo Resource Manager-sjabloon die u implementeert, kan een lokaal bestand op uw computer of een extern bestand dat zich bevindt in een zoals GitHub-opslagplaats. Hallo-sjabloon die u in dit artikel implementeert is beschikbaar in Hallo [voorbeeldsjabloon](#sample-template) sectie, of als een [storage accountsjabloon in GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/101-storage-account-create/azuredeploy.json).

[!INCLUDE [sample-cli-install](../../includes/sample-cli-install.md)]

Als u geen Azure CLI is geïnstalleerd, kunt u Hallo [Cloud Shell](#deploy-template-from-cloud-shell).

## <a name="deploy-local-template"></a>Lokale sjabloon implementeren

Bij het implementeren van resources tooAzure, u:

1. Meld u bij tooyour Azure-account
2. Maak een resourcegroep die als Hallo-container voor resources Hallo geïmplementeerd fungeert. Hallo-naam van de resourcegroep Hallo kan alleen alfanumerieke tekens, punten, onderstrepingstekens, afbreekstreepjes en haakjes bevatten. Het kan zijn van too90 tekens. Het mag niet eindigen op een punt.
3. Toohello resource groep Hallo-sjabloon die Hallo resources toocreate definieert implementeren

Een sjabloon kan parameters die u in staat toocustomize Hallo implementatie stellen bevatten. U kunt bijvoorbeeld waarden die zijn toegesneden opgeven voor een bepaalde omgeving (zoals ontwikkelen, testen en productie). Hallo-voorbeeldsjabloon definieert een parameter voor het opslagaccount Hallo SKU. 

Hallo volgende voorbeeld maakt een resourcegroep en implementeert een sjabloon op basis van uw lokale computer:

```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
```

Hallo-implementatie kan toocomplete van enkele minuten duren. Wanneer deze is voltooid, ziet u een bericht met Hallo resultaat:

```azurecli
"provisioningState": "Succeeded",
```

## <a name="deploy-external-template"></a>Externe sjabloon implementeren

In plaats van Resource Manager-sjablonen worden opgeslagen op uw lokale computer, kunt u desgewenst toostore ze in een externe locatie. U kunt sjablonen opslaan in een resourcebeheerbibliotheek (zoals GitHub). Of u kunt ze opslaan in Azure storage-account voor gedeelde toegang in uw organisatie.

toodeploy een externe-sjabloon gebruiken Hallo **sjabloon uri** parameter. Gebruik hello URI in Hallo voorbeeld toodeploy Hallo voorbeeldsjabloon vanuit GitHub.
   
```azurecli
az login

az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
    --parameters storageAccountType=Standard_GRS
```

Hallo voorgaande voorbeeld vereist een openbaar toegankelijke URI voor Hallo-sjabloon voor de meeste scenario werkt, omdat de sjabloon mag geen gevoelige gegevens bevatten. Als u moet toospecify gevoelige gegevens (zoals een beheerderswachtwoord), wordt die waarde als beveiligde parameter doorgeven. Echter, als u niet wilt dat uw sjabloon toobe openbaar toegankelijk is, kunt u deze beschermen door op te slaan deze in een container particuliere opslag. Zie voor meer informatie over het implementeren van een sjabloon waarvoor een shared access signature (SAS)-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-cli-sas-token.md).

## <a name="deploy-template-from-cloud-shell"></a>Sjabloon implementeren vanuit Cloud Shell

U kunt [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI-opdrachten voor het implementeren van uw sjabloon. Echter, moet u eerst uw sjabloon in laden Hallo bestandsshare voor uw Cloud-Shell. Als u Cloud Shell niet hebt gebruikt, raadpleegt u [Overzicht van Azure Cloud Shell](../cloud-shell/overview.md) voor informatie over het instellen.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).   

2. Selecteer de Cloud Shell-resourcegroep. Hallo naampatroon is `cloud-shell-storage-<region>`.

   ![Resourcegroep selecteren](./media/resource-group-template-deploy-cli/select-cs-resource-group.png)

3. Hallo storage-account selecteren voor uw Cloud-Shell.

   ![Opslagaccount selecteren](./media/resource-group-template-deploy-cli/select-storage.png)

4. Selecteer **Bestanden**.

   ![Bestanden selecteren](./media/resource-group-template-deploy-cli/select-files.png)

5. Selecteer Hallo bestandsshare voor Cloud-Shell. Hallo naampatroon is `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Bestandsshare selecteren](./media/resource-group-template-deploy-cli/select-file-share.png)

6. Selecteer **Map toevoegen**.

   ![Map toevoegen](./media/resource-group-template-deploy-cli/select-add-directory.png)

7. Geef deze de naam **Sjablonen** en selecteer **OK**.

   ![Map een naam geven](./media/resource-group-template-deploy-cli/name-templates.png)

8. Selecteer een nieuwe map.

   ![Map selecteren](./media/resource-group-template-deploy-cli/select-templates.png)

9. Selecteer **Uploaden**.

   ![Uploaden selecteren](./media/resource-group-template-deploy-cli/select-upload.png)

10. Zoek de sjabloon en upload deze.

   ![Bestand uploaden](./media/resource-group-template-deploy-cli/upload-files.png)

11. Open Hallo-prompt.

   ![Cloud Shell openen](./media/resource-group-template-deploy-cli/start-cloud-shell.png)

12. Voer de volgende opdrachten in de Cloud Shell Hallo Hallo:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageAccountType=Standard_GRS
   ```

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

gebruik van een lokale parameterbestand toopass `@` toospecify een lokaal bestand met de naam storage.parameters.json.

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

## <a name="test-a-template-deployment"></a>Een sjabloonimplementatie testen

tootest uw sjabloon en de parameterbestanden waarden zonder het distribueren van alle resources gebruiken [az implementatie valideren](/cli/azure/group/deployment#validate). 

```azurecli
az group deployment validate \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters @storage.parameters.json
```

Als er geen fouten worden aangetroffen, retourneert Hallo opdracht informatie over de testimplementatie Hallo. In het bijzonder, zoals u ziet dat Hallo **fout** waarde null is.

```azurecli
{
  "error": null,
  "properties": {
      ...
```

Als er een fout wordt gedetecteerd, retourneert Hallo opdracht een foutbericht weergegeven. Poging een onjuiste waarde voor het opslagaccount Hallo SKU, toopass retourneert bijvoorbeeld Hallo volgende fout:

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template validation failed: 'hello provided value 'badSKU' for hello template parameter 
      'storageAccountType' at line '13' and column '20' is not valid. hello parameter value is not part of hello allowed 
      value(s): 'Standard_LRS,Standard_ZRS,Standard_GRS,Standard_RAGRS,Premium_LRS'.'.",
    "target": null
  },
  "properties": null
}
```

Als uw sjabloon een syntaxisfout heeft, foutmelding Hallo opdracht een die aangeeft dat Hallo sjabloon kan niet worden geparseerd. Hallo-bericht geeft aan Hallo regelnummer en positie van Hallo parseerfout.

```azurecli
{
  "error": {
    "code": "InvalidTemplate",
    "details": null,
    "message": "Deployment template parse failed: 'After parsing a value an unexpected character was encountered:
      \". Path 'variables', line 31, position 3.'.",
    "target": null
  },
  "properties": null
}
```

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

toouse voltooid modus gebruik Hallo `mode` parameter:

```azurecli
az group deployment create \
    --name ExampleDeployment \
    --mode Complete \
    --resource-group ExampleGroup \
    --template-file storage.json \
    --parameters storageAccountType=Standard_GRS
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
* Hallo-voorbeelden in dit artikel implementeren resources tooa-resourcegroep in uw standaardabonnement. Zie voor een ander abonnement toouse [meerdere Azure-abonnementen beheren](/cli/azure/manage-azure-subscriptions-azure-cli).
* Zie voor een compleet codevoorbeeld-script waarmee een sjabloon wordt geïmplementeerd, [script voor implementatie van Resource Manager-sjabloon](resource-manager-samples-cli-deploy.md).
* hoe toodefine-parameters in de sjabloon zien toounderstand [begrijpen Hallo structuur en syntaxis van Azure Resource Manager-sjablonen](resource-group-authoring-templates.md).
* Zie voor tips over het oplossen van algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Zie voor meer informatie over het implementeren van een sjabloon waarvoor een SAS-token [persoonlijke sjabloon implementeren met SAS-token](resource-manager-cli-sas-token.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).
