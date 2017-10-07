---
title: aaaDeployment bewerkingen met Azure Resource Manager | Microsoft Docs
description: Hierin wordt beschreven hoe tooview Azure Resource Manager deployment bewerkingen met Hallo-portal, PowerShell, Azure CLI en REST-API.
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Bewerkingen van de implementatie weergeven met Azure Resource Manager


Hallo-bewerkingen voor een implementatie via hello Azure-portal, kunt u weergeven. Hebt u mogelijk interessant Hallo bewerkingen weer te geven wanneer u een fout opgetreden tijdens de implementatie ontvangen hebt zodat dit artikel is gericht op het weergeven van bewerkingen die zijn mislukt. Hallo-portal biedt een interface waarmee u tooeasily zoeken Hallo fouten en mogelijke oplossingen te bepalen.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>Portal
toosee implementatiebewerkingen hello, gebruik Hallo stappen te volgen:

1. U ziet Hallo-status van de laatste implementatie Hallo voor de Hallo resourcegroep voor het Hallo-implementatie. Meer informatie kunt u deze status tooget selecteren.
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/deployment-status.png)
2. U ziet Hallo recente geschiedenis van implementatie. Selecteer Hallo-implementatie die niet zijn geslaagd.
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/select-deployment.png)
3. Selecteer Hallo koppeling toosee een beschrijving van waarom Hallo implementatie is mislukt. In onderstaande Hallo afbeelding is Hallo DNS-record niet uniek.  
   
    ![mislukte implementatie weergeven](./media/resource-manager-deployment-operations/view-error.png)
   
    Dit foutbericht moeten voldoende zijn voor u toobegin het oplossen van problemen. Echter, als u meer informatie over welke taken zijn voltooid, vindt u Hallo bewerkingen zoals weergegeven in de volgende stappen uit Hallo.
4. U kunt alle Hallo implementatiebewerkingen weergeven in Hallo **implementatie** blade. Selecteer een bewerking toosee meer informatie.
   
    ![bewerkingen weergeven](./media/resource-manager-deployment-operations/view-operations.png)
   
    In dit geval zien u dat Hallo storage-account, het virtuele netwerk en beschikbaarheidsset zijn gemaakt. Hallo openbaar IP-adres is mislukt en andere resources zijn niet is uitgevoerd.
5. U kunt gebeurtenissen voor Hallo implementatie bekijken door te selecteren **gebeurtenissen**.
   
    ![gebeurtenissen weergeven](./media/resource-manager-deployment-operations/view-events.png)
6. U alle Hallo gebeurtenissen voor Hallo implementatie zien en selecteert u een voor meer informatie. U ziet te Hallo correlatie-id's. Deze waarde kan nuttig zijn bij het werken met de technische ondersteuning tootroubleshoot een implementatie.
   
    ![Zie gebeurtenissen](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget Hallo algehele status van een implementatie, gebruik Hallo **Get-AzureRmResourceGroupDeployment** opdracht. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   Of u kunt filteren Hallo resultaten voor alleen deze implementaties die zijn mislukt.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Elke implementatie bevat meerdere bewerkingen. Elke bewerking vertegenwoordigt een stap in het implementatieproces Hallo. toodiscover wat gegaan met een implementatie, moet u meestal toosee details over Hallo implementatiebewerkingen. U kunt zien Hallo-status van het Hallo-bewerkingen met **Get-AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Dat meerdere bewerkingen met elkaar Hallo na indeling geretourneerd:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget voor meer informatie over mislukte bewerkingen Hallo-eigenschappen voor bewerkingen met ophalen **mislukt** status.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Dit retourneert dat alle mislukte bewerkingen die met elkaar in de volgende indeling Hallo Hallo:

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    Houd er rekening mee Hallo serviceRequestId en Hallo trackingId voor Hallo-bewerking. Hallo serviceRequestId kan nuttig zijn bij het werken met de technische ondersteuning tootroubleshoot een implementatie. Hallo trackingId gebruikt u in de volgende stap toofocus Hallo op een bepaalde bewerking.
4. Hallo statusbericht tooget van een bepaalde mislukte bewerking gebruik Hallo volgende opdracht:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Die wordt geretourneerd:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Elke implementatiebewerking in Azure bevat-aanvraag en antwoord-inhoud. Hallo aanvraaginhoud is wat u verzonden tooAzure tijdens de implementatie (bijvoorbeeld: Maak een VM besturingssysteemschijf en andere bronnen). Hallo antwoordinhoud is wat Azure van uw implementatieaanvraag teruggestuurd. Tijdens de implementatie, kunt u **DeploymentDebugLogLevel** parameter worden toospecify die Hallo aanvraag en/of antwoord in logboek Hallo worden bewaard. 

  U die gegevens ophalen uit Hallo-logboek en sla het lokaal via Hallo volgende PowerShell-opdrachten:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Azure CLI

1. Ophalen van algemene status van een implementatie met Hallo Hallo **azure-groep implementatie weergeven** opdracht.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Een van de waarden geretourneerd Hallo Hallo is **correlationId**. Deze waarde wordt gebruikt tootrack gerelateerde gebeurtenissen en kan handig zijn wanneer werken met de technische ondersteuning tootroubleshoot een implementatie.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. toosee hello bewerkingen voor een implementatie gebruiken:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Informatie ophalen over een implementatie met Hallo [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) bewerking.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    Hallo reactie, houd er rekening mee in het bijzonder Hallo **provisioningState**, **correlationId**, en **fout** elementen. Hallo **correlationId** wordt gebruikt tootrack gerelateerde gebeurtenissen en kan handig zijn wanneer werken met de technische ondersteuning tootroubleshoot een implementatie.

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. Informatie ophalen over implementatiebewerkingen Hello [lijst van alle implementatiebewerkingen voor sjabloon](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) bewerking. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    Hallo-antwoord bevat de aanvraag en/of antwoord informatie op basis van wat u hebt opgegeven in Hallo **debugSetting** eigenschap tijdens de implementatie.

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a>Volgende stappen
* Zie voor meer informatie over het oplossen van fouten voor bepaalde implementatie, [oplossen van veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn over het gebruik van de activiteit Hallo registreert toomonitor andere soorten acties, Zie [activiteit weergeven logboeken toomanage Azure resources](resource-group-audit.md).
* toovalidate uw implementatie alvorens uit te voeren, Zie [een resourcegroep implementeren met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).

