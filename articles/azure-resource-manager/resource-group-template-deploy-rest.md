---
title: aaaDeploy resources met de REST-API en de sjabloon | Microsoft Docs
description: Azure Resource Manager en de REST-API van Resource Manager toodeploy een tooAzure resources gebruiken. Hallo-bronnen worden gedefinieerd in het Resource Manager-sjabloon.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 1d8fbd4c-78b0-425b-ba76-f2b7fd260b45
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: tomfitz
ms.openlocfilehash: 347ad3bdb604429e7291297d448688204af69b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-with-resource-manager-templates-and-resource-manager-rest-api"></a>Resources implementeren met Resource Manager-sjablonen en Resource Manager REST API
> [!div class="op_single_selector"]
> * [PowerShell](resource-group-template-deploy.md)
> * [Azure CLI](resource-group-template-deploy-cli.md)
> * [Portal](resource-group-template-deploy-portal.md)
> * [REST API](resource-group-template-deploy-rest.md)
> 
> 

Dit artikel wordt uitgelegd hoe toouse Hallo REST-API van Resource Manager met Resource Manager-sjablonen toodeploy uw tooAzure resources.  

> [!TIP]
> Zie voor informatie over wanneer foutopsporing is een fout opgetreden tijdens de implementatie:
> 
> * [Implementatiebewerkingen weergeven](resource-manager-deployment-operations.md) toolearn over het ophalen van informatie die u helpt problemen met de fout
> * [Oplossen van veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager](resource-manager-common-deployment-errors.md) toolearn hoe algemene implementatiefouten tooresolve
> 
> 

De sjabloon is een lokaal bestand of een extern bestand dat is beschikbaar via een URI. Wanneer de sjabloon bevindt zich in een opslagaccount, kunt u access toohello sjabloon beperken en bieden een shared access signature (SAS)-token tijdens de implementatie.

[!INCLUDE [resource-manager-deployments](../../includes/resource-manager-deployments.md)]

## <a name="deploy-with-hello-rest-api"></a>Met de Hallo REST-API implementeren
1. Stel [algemene parameters en -koppen](https://docs.microsoft.com/rest/api/index), met inbegrip van verificatietokens.
2. Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken. Geef uw abonnements-ID, het Hallo-naam van de nieuwe resourcegroep Hallo en locatie die u nodig hebt voor uw oplossing. Zie voor meer informatie [een resourcegroep maken](https://docs.microsoft.com/rest/api/resources/resourcegroups#ResourceGroups_CreateOrUpdate).
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>?api-version=2015-01-01
          <common headers>
          {
            "location": "West US",
            "tags": {
               "tagname1": "tagvalue1"
            }
          }
3. Valideren van uw implementatie voordat deze wordt uitgevoerd door het uitvoeren van Hallo [valideren van de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Validate) bewerking. Bij het testen van Hallo implementatie Geef parameters op exact dezelfde manier als bij het uitvoeren van Hallo-implementatie (weergegeven in de volgende stap Hallo).
4. Maakt een implementatie. Geef uw abonnements-ID, Hallo-naam van de resourcegroep Hallo Hallo-naam van het Hallo-implementatie en een koppeling tooyour sjabloon. Zie voor meer informatie over het sjabloonbestand Hallo [parameterbestand](#parameter-file). Zie voor meer informatie over Hallo REST-API toocreate een resourcegroep [sjabloonimplementatie met een maakt](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_CreateOrUpdate). Kennisgeving Hallo **modus** te is ingesteld,**incrementele**. instellen van een volledige implementatie toorun **modus** te**Complete**. Wees voorzichtig met behulp van Hallo volledige modus kunt u de resources die zich niet in uw sjabloon per ongeluk verwijderen.
   
        PUT https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
          <common headers>
          {
            "properties": {
              "templateLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
                "contentVersion": "1.0.0.0"
              },
              "mode": "Incremental",
              "parametersLink": {
                "uri": "http://mystorageaccount.blob.core.windows.net/templates/parameters.json",
                "contentVersion": "1.0.0.0"
              }
            }
          }
   
      Als u wilt dat toolog antwoordinhoud, aanvraaginhoud of beide, opnemen **debugSetting** in Hallo-aanvraag.
   
        "debugSetting": {
          "detailLevel": "requestContent, responseContent"
        }
   
      U kunt instellen uw storage-account toouse een shared access signature (SAS)-token. Zie voor meer informatie [toegang delegeren met Shared Access Signature](https://docs.microsoft.com/rest/api/storageservices/delegating-access-with-a-shared-access-signature).
5. Hallo-status van de sjabloonimplementatie Hallo ophalen. Zie voor meer informatie [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).
   
          GET https://management.azure.com/subscriptions/<YourSubscriptionId>/resourcegroups/<YourResourceGroupName>/providers/Microsoft.Resources/deployments/<YourDeploymentName>?api-version=2015-01-01
           <common headers>

## <a name="parameter-file"></a>Parameterbestand

[!INCLUDE [resource-manager-parameter-file](../../includes/resource-manager-parameter-file.md)]

## <a name="next-steps"></a>Volgende stappen
* toolearn over het verwerken van asynchrone REST-bewerkingen, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).
* Zie voor een voorbeeld van het implementeren van resources via de .NET-clientbibliotheek Hallo [resources met behulp van .NET-bibliotheken en een sjabloon implementeren](../virtual-machines/windows/csharp-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* toodefine parameters in de sjabloon, Zie [sjablonen](resource-group-authoring-templates.md#parameters).
* Zie voor instructies over het implementeren van uw oplossing toodifferent omgevingen [ontwikkel- en testomgevingen in Microsoft Azure](solution-dev-test-environments.md).
* Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).

