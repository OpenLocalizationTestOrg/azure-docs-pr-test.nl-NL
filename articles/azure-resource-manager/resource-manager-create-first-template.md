---
title: de eerste Azure Resource Manager-sjabloon aaaCreate | Microsoft Docs
description: Een stapsgewijze handleiding toocreating uw eerste Azure Resource Manager-sjabloon. Hier ziet u hoe toouse verwijzing naar de sjabloon voor een sjabloon storage account toocreate Hallo Hallo.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 07/27/2017
ms.topic: get-started-article
ms.author: tomfitz
ms.openlocfilehash: 92e6d6bb7094fe0e4537ee080704967862804bdb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-your-first-azure-resource-manager-template"></a>Uw eerste Azure Resource Manager-sjabloon maken en implementeren
In dit onderwerp leidt u door Hallo stappen voor het maken van uw eerste Azure Resource Manager-sjabloon. Resource Manager-sjablonen zijn JSON-bestanden die Hallo resources moet u toodeploy voor uw oplossing definiëren. toounderstand hello concepten die horen bij het implementeren en beheren van uw Azure-oplossingen, Zie [overzicht van Azure Resource Manager](resource-group-overview.md). Als u bestaande resources hebt en tooget een sjabloon voor deze bronnen wilt, raadpleegt u [een Azure Resource Manager-sjabloon uit bestaande resources exporteren](resource-manager-export-template.md).

toocreate en herzien sjablonen, moet u een JSON-editor. [Visual Studio Code](https://code.visualstudio.com/) is een lichte, open-source, platformoverschrijdende code-editor. U wordt sterk aangeraden om Visual Studio Code te gebruiken voor het maken van Resource Manager-sjablonen. In dit onderwerp wordt ervan uitgegaan dat u VS Code gebruikt. Als u een andere JSON-editor (zoals Visual Studio) hebt, kunt u die editor gebruiken.

## <a name="prerequisites"></a>Vereisten

* Visual Studio Code. U kunt VS Code, indien nodig, installeren via [https://code.visualstudio.com/](https://code.visualstudio.com/).
* Een Azure-abonnement. Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

## <a name="create-template"></a>Sjabloon maken

Laten we beginnen met een eenvoudige sjabloon waarmee een tooyour voor opslagaccountabonnement wordt geïmplementeerd.

1. Selecteer **Bestand** > **Nieuw bestand**. 

   ![Nieuw bestand](./media/resource-manager-create-first-template/new-file.png)

2. Kopieer en plak de volgende JSON-syntaxis in het bestand Hallo:

   ```json
   {
     "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
     "contentVersion": "1.0.0.0",
     "parameters": {
     },
     "variables": {
     },
     "resources": [
       {
         "name": "[concat('storage', uniqueString(resourceGroup().id))]",
         "type": "Microsoft.Storage/storageAccounts",
         "apiVersion": "2016-01-01",
         "sku": {
           "name": "Standard_LRS"
         },
         "kind": "Storage",
         "location": "South Central US",
         "tags": {},
         "properties": {}
       }
     ],
     "outputs": {  }
   }
   ```

   Namen van opslagaccounts zijn enkele beperkingen waardoor ze moeilijk tooset. Hallo-naam moet tussen 3 en 24 tekens lang, gebruik alleen cijfers en kleine letters en uniek zijn. Hallo voorgaande sjabloon worden gebruikt voor Hallo [uniqueString](resource-group-template-functions-string.md#uniquestring) werken toogenerate een hash-waarde. toogive deze hash waarde meer betekenis: Hallo voorvoegsel wordt toegevoegd *opslag*. 

3. Sla dit bestand als **azuredeploy.json** tooa lokale map.

   ![Sjabloon opslaan](./media/resource-manager-create-first-template/save-template.png)

## <a name="deploy-template"></a>Sjabloon implementeren

U gereed toodeploy deze sjabloon zijn. U PowerShell of Azure CLI toocreate een resourcegroep. Vervolgens implementeert u een opslaggroep account toothat resource.

* Gebruik Hallo volgende opdrachten uit Hallo-map met de Hallo-sjabloon voor PowerShell:

   ```powershell
   Login-AzureRmAccount
   
   New-AzureRmResourceGroup -Name examplegroup -Location "South Central US"
   New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json
   ```

* Gebruik voor een lokale installatie van Azure CLI Hallo volgende opdrachten uit Hallo-map met de Hallo sjabloon:

   ```azurecli
   az login

   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file azuredeploy.json
   ```

Wanneer de implementatie is voltooid, wordt uw storage-account bestaat in de resourcegroep Hallo.

## <a name="deploy-template-from-cloud-shell"></a>Sjabloon implementeren vanuit Cloud Shell

U kunt [Cloud Shell](../cloud-shell/overview.md) toorun hello Azure CLI-opdrachten voor het implementeren van uw sjabloon. Echter, moet u eerst uw sjabloon in laden Hallo bestandsshare voor uw Cloud-Shell. Als u Cloud Shell niet hebt gebruikt, raadpleegt u [Overzicht van Azure Cloud Shell](../cloud-shell/overview.md) voor informatie over het instellen.

1. Meld u bij toohello [Azure-portal](https://portal.azure.com).   

2. Selecteer de Cloud Shell-resourcegroep. Hallo naampatroon is `cloud-shell-storage-<region>`.

   ![Resourcegroep selecteren](./media/resource-manager-create-first-template/select-cs-resource-group.png)

3. Hallo storage-account selecteren voor uw Cloud-Shell.

   ![Opslagaccount selecteren](./media/resource-manager-create-first-template/select-storage.png)

4. Selecteer **Bestanden**.

   ![Bestanden selecteren](./media/resource-manager-create-first-template/select-files.png)

5. Selecteer Hallo bestandsshare voor Cloud-Shell. Hallo naampatroon is `cs-<user>-<domain>-com-<uniqueGuid>`.

   ![Bestandsshare selecteren](./media/resource-manager-create-first-template/select-file-share.png)

6. Selecteer **Map toevoegen**.

   ![Map toevoegen](./media/resource-manager-create-first-template/select-add-directory.png)

7. Geef deze de naam **Sjablonen** en selecteer **OK**.

   ![Map een naam geven](./media/resource-manager-create-first-template/name-templates.png)

8. Selecteer een nieuwe map.

   ![Map selecteren](./media/resource-manager-create-first-template/select-templates.png)

9. Selecteer **Uploaden**.

   ![Uploaden selecteren](./media/resource-manager-create-first-template/select-upload.png)

10. Zoek de sjabloon en upload deze.

   ![Bestand uploaden](./media/resource-manager-create-first-template/upload-files.png)

11. Open Hallo-prompt.

   ![Cloud Shell openen](./media/resource-manager-create-first-template/start-cloud-shell.png)

12. Voer de volgende opdrachten in de Cloud Shell Hallo Hallo:

   ```azurecli
   az group create --name examplegroup --location "South Central US"
   az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json
   ```

Wanneer de implementatie is voltooid, wordt uw storage-account bestaat in de resourcegroep Hallo.

## <a name="customize-hello-template"></a>Hallo-sjabloon aanpassen

Hallo sjabloon werkt goed samen, maar het is niet flexibel. Altijd implementeert u een lokaal redundante opslag tooSouth VS-midden. de naam van de Hallo is altijd *opslag* gevolgd door een hash-waarde. tooenable Hallo-sjabloon voor verschillende scenario's met parameters toohello sjabloon toevoegen.

Hallo ziet volgende voorbeeld Hallo parameters sectie met twee parameters. de eerste parameter Hallo `storageSKU` kunt u toospecify Hallo type redundantie. Deze wordt beperkt door Hallo-waarden die u kunt doorgeven in toovalues die geldig voor een opslagaccount zijn. Er wordt ook een standaardwaarde opgegeven. tweede parameter Hallo `storageNamePrefix` set tooallow maximaal 11 tekens is. Hiermee wordt een standaardwaarde opgegeven.

```json
"parameters": {
  "storageSKU": {
    "type": "string",
    "allowedValues": [
      "Standard_LRS",
      "Standard_ZRS",
      "Standard_GRS",
      "Standard_RAGRS",
      "Premium_LRS"
    ],
    "defaultValue": "Standard_LRS",
    "metadata": {
      "description": "hello type of replication toouse for hello storage account."
    }
  },
  "storageNamePrefix": {
    "type": "string",
    "maxLength": 11,
    "defaultValue": "storage",
    "metadata": {
      "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
    }
  }
},
```

Voeg een variabele met de naam in gedeelte variabelen Hallo `storageName`. Het voorvoegsel op Hallo van Hallo parameters en een hash van Hallo combineert [uniqueString](resource-group-template-functions-string.md#uniquestring) functie. Hierbij Hallo [toLower](resource-group-template-functions-string.md#tolower) tooconvert alle tekens toolowercase werken.

```json
"variables": {
  "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
},
```

toouse deze nieuwe waarden voor uw opslagaccount, wijzig de resourcedefinitie Hallo:

```json
"resources": [
  {
    "name": "[variables('storageName')]",
    "type": "Microsoft.Storage/storageAccounts",
    "apiVersion": "2016-01-01",
    "sku": {
      "name": "[parameters('storageSKU')]"
    },
    "kind": "Storage",
    "location": "[resourceGroup().location]",
    "tags": {},
    "properties": {}
  }
],
```

U ziet dat Hallo naam van het opslagaccount hello toohello variabele die u hebt toegevoegd nu is ingesteld. Hallo SKU-naam is toohello waarde van parameter Hallo ingesteld. Hallo vestiging dezelfde locatie als de resourcegroep Hallo Hallo.

Sla het bestand op. 

Na het voltooien van Hallo stappen in dit artikel is de sjabloon nu ziet eruit als:

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    },   
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name. Use only lowercase letters and numbers."
      }
    }
  },
  "variables": {
    "storageName": "[concat(toLower(parameters('storageNamePrefix')), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {}
    }
  ],
  "outputs": {  }
}
```

## <a name="redeploy-template"></a>Sjabloon opnieuw implementeren

Implementeer opnieuw Hallo sjabloon met verschillende waarden.

Gebruik voor PowerShell:

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile azuredeploy.json -storageNamePrefix newstore -storageSKU Standard_RAGRS
```

Gebruik voor Azure CLI:

```azurecli
az group deployment create --resource-group examplegroup --template-file azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

Upload de gewijzigde sjabloon toohello file share voor Hallo Cloud-Shell. Hallo bestaand bestand overschrijven. Gebruik vervolgens Hallo volgende opdracht:

```azurecli
az group deployment create --resource-group examplegroup --template-file clouddrive/templates/azuredeploy.json --parameters storageSKU=Standard_RAGRS storageNamePrefix=newstore
```

## <a name="clean-up-resources"></a>Resources opschonen

Wanneer deze niet langer nodig is, Hallo resources die u hebt geïmplementeerd door het verwijderen van resourcegroep Hallo opschonen.

Gebruik voor PowerShell:

```powershell
Remove-AzureRmResourceGroup -Name examplegroup
```

Gebruik voor Azure CLI:

```azurecli
az group delete --name examplegroup
```

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn meer informatie over het Hallo-structuur van een sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).
* Zie toolearn over de eigenschappen voor een opslagaccount hello [opslagaccounts sjabloonverwijzing](/azure/templates/microsoft.storage/storageaccounts).
* tooview voltooid sjablonen voor verschillende soorten oplossingen, Zie Hallo [Azure-Snelstartsjablonen](https://azure.microsoft.com/documentation/templates/).
