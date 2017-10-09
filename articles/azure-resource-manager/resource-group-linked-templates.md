---
title: sjablonen voor Azure-implementatie aaaLink | Microsoft Docs
description: Hierin wordt beschreven hoe toouse gekoppeld sjablonen in een Azure Resource Manager-sjabloon toocreate een sjabloonoplossing modulaire. Ziet u hoe de waarden van de parameters toopass, geeft een parameterbestand en URL's dynamisch gemaakt.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Gekoppelde sjablonen gebruiken bij het implementeren van Azure-resources
Uit binnen een Azure Resource Manager-sjabloon kunt u koppelen tooanother sjabloon waarmee u toodecompose uw implementatie in een set van gerichte, doel-specifieke sjablonen. Net als bij een toepassing in verschillende codeklassen ontleedt, biedt afbreken voordelen wat betreft testen, hergebruiken en leesbaarheid.  

U kunt parameters doorgeven van een sjabloon belangrijkste tooa gekoppelde sjabloon en deze parameters kunnen rechtstreeks toewijzen tooparameters of variabelen die worden weergegeven door Hallo aanroepen van de sjabloon. Hallo gekoppelde sjabloon kunt ook de bronsjabloon voor een uitvoer variabele back toohello, waardoor een wederzijdse gegevensuitwisseling tussen sjablonen doorgeven.

## <a name="linking-tooa-template"></a>Sjabloon tooa koppelen
U maakt een koppeling tussen twee sjablonen door toe te voegen een implementatie-bron in de belangrijkste sjabloon Hallo die punten toohello gekoppelde sjabloon. Instellen van Hallo **templateLink** eigenschap toohello URI van de gekoppelde Hallo-sjabloon. U kunt parameterwaarden kan opgeven voor de gekoppelde sjabloon Hallo rechtstreeks in uw sjabloon of in een parameterbestand. Hallo volgende voorbeeld wordt Hallo **parameters** eigenschap toospecify rechtstreeks een parameterwaarde.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Net als andere brontypen, kunt u de afhankelijkheden tussen de gekoppelde sjabloon Hallo en andere resources instellen. Daarom als voor andere bronnen vereist een waarde voor de uitvoer van de gekoppelde sjabloon hello, kunt u zorgen Hallo gekoppelde sjabloon voordat deze wordt geïmplementeerd. Of als de gekoppelde sjabloon Hallo is afhankelijk van andere bronnen, kunt u ervoor zorgen dat andere resources worden geïmplementeerd voordat Hallo gekoppelde sjabloon. U kunt een waarde ophalen uit een gekoppelde sjabloon Hello de volgende syntaxis:

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hallo Resource Manager-service moet kunnen tooaccess Hallo gekoppelde sjabloon. U kunt een lokaal bestand of een bestand dat is alleen beschikbaar op uw lokale netwerk voor de gekoppelde sjabloon Hallo opgeven. U kunt alleen een URI-waarde die een bevat opgeven **http** of **https**. Een mogelijkheid is de gekoppelde sjabloon in een opslagaccount en gebruik URI voor het item, zoals weergegeven in het volgende voorbeeld Hallo Hallo tooplace:

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Hoewel Hallo gekoppelde sjabloon moet extern beschikbaar zijn, hoeft deze niet toobe algemeen beschikbaar toohello openbaar. U kunt uw sjabloon tooa persoonlijke storage-account dat is eigenaar van het opslagaccount Hallo toegankelijk tooonly toevoegen. Vervolgens maakt u een shared access signature (SAS)-token tooenable toegang tijdens de implementatie. U toevoegen deze SAS-token toohello URI voor de gekoppelde sjabloon Hallo. Zie voor stappen over het instellen van een sjabloon in een opslagaccount en een SAS-token te genereren, [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md) of [resources met Resource Manager-sjablonen te implementeren en Azure CLI](resource-group-template-deploy-cli.md). 

Hallo volgende voorbeeld ziet u een sjabloon voor bovenliggend die koppelingen tooanother sjabloon. Hallo gekoppelde sjabloon wordt geopend met een SAS-token dat is doorgegeven als parameter.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Hoewel Hallo-token is doorgegeven als een beveiligde tekenreeks, wordt hello URI van Hallo gekoppelde sjabloon, Hallo SAS-token, inclusief vastgelegd op Hallo implementatiebewerkingen. toolimit blootstelling, instellen dat een verlopen voor Hallo-token.

Resource Manager verwerkt elke gekoppelde sjabloon als een afzonderlijke implementatie. In de geschiedenis van Hallo implementatie voor de resourcegroep hello ziet u afzonderlijke implementaties voor de bovenliggende Hallo en geneste sjablonen.

![implementatiegeschiedenis](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Het parameterbestand tooa koppelen
Hallo volgende voorbeeld wordt met Hallo **parametersLink** eigenschap toolink tooa parameterbestand.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Hallo URI waarde Hallo gekoppelde parameterbestand mag geen een lokaal bestand, en vergezeld gaan van een **http** of **https**. Hallo parameterbestand kan ook worden beperkt tooaccess via een SAS-token.

## <a name="using-variables-toolink-templates"></a>Met behulp van variabelen toolink sjablonen
Hallo voorgaande voorbeelden toonden vastgelegde URL waarden voor Hallo sjabloon koppelingen. Deze methode werkt mogelijk voor een eenvoudige sjabloon, maar werkt niet goed bij het werken met een groot aantal modulaire sjablonen. U kunt in plaats daarvan maken van een statische variabele die een basis-URL voor de belangrijkste sjabloon Hallo opslaat en URL's dynamisch voor Hallo gekoppelde sjablonen van deze basis-URL te maken. Hallo voordeel van deze benadering is kunt u gemakkelijk verplaatsen of fork Hallo-sjabloon, omdat u alleen toochange Hallo statische variabele in de belangrijkste sjabloon Hallo nodig hebt. de belangrijkste sjabloon Hallo Hallo juiste dat URI 's in de gehele Hallo ontleed sjabloon is geslaagd.

Hallo volgende voorbeeld laat zien hoe een base URL toocreate toouse twee URL's voor gekoppeld sjablonen (**sharedTemplateUrl** en **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

U kunt ook [deployment()](resource-group-template-functions-deployment.md#deployment) tooget basis-URL voor de huidige sjabloon Hallo Hallo en die tooget Hallo-URL gebruiken voor andere sjablonen in Hallo dezelfde locatie. Deze methode is handig als uw sjabloonlocatie wijzigt (mogelijk vanwege tooversioning) of het gewenste tooavoid harde-URL's in het sjabloonbestand Hallo coderen. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Compleet voorbeeld
Hallo voorbeeld sjablonen na weergeven een vereenvoudigde rangschikking van gekoppelde sjablonen tooillustrate diverse Hallo concepten in dit artikel. Er wordt vanuit gegaan Hallo sjablonen toohello dezelfde container in een opslagaccount met openbare toegang uitgeschakeld zijn toegevoegd. Hallo gekoppelde sjabloon wordt een waarde back toohello belangrijkste sjabloon doorgegeven in Hallo **levert** sectie.

Hallo **parent.json** bestand bestaat uit:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Hallo **helloworld.json** bestand bestaat uit:

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

In PowerShell moet u een token voor de container Hallo ophalen en implementeren van Hallo sjablonen met:

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

In Azure CLI 2.0 ophalen van een token voor Hallo-container en Hallo sjablonen met Hallo na de code implementeren:

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Volgende stappen
* Zie toolearn over Hallo Hallo implementatievolgorde voor uw resources definiëren [afhankelijkheden definiëren in Azure Resource Manager-sjablonen](resource-group-define-dependencies.md)
* toolearn hoe toodefine één resource maken maar veel exemplaren ervan raadpleegt [meerdere exemplaren van resources in Azure Resource Manager maken](resource-group-create-multiple.md)

