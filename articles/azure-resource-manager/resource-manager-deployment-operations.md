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
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="b55a2-103">Bewerkingen van de implementatie weergeven met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b55a2-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="b55a2-104">Hallo-bewerkingen voor een implementatie via hello Azure-portal, kunt u weergeven.</span><span class="sxs-lookup"><span data-stu-id="b55a2-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="b55a2-105">Hebt u mogelijk interessant Hallo bewerkingen weer te geven wanneer u een fout opgetreden tijdens de implementatie ontvangen hebt zodat dit artikel is gericht op het weergeven van bewerkingen die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="b55a2-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="b55a2-106">Hallo-portal biedt een interface waarmee u tooeasily zoeken Hallo fouten en mogelijke oplossingen te bepalen.</span><span class="sxs-lookup"><span data-stu-id="b55a2-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="b55a2-107">Portal</span><span class="sxs-lookup"><span data-stu-id="b55a2-107">Portal</span></span>
<span data-ttu-id="b55a2-108">toosee implementatiebewerkingen hello, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b55a2-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="b55a2-109">U ziet Hallo-status van de laatste implementatie Hallo voor de Hallo resourcegroep voor het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="b55a2-110">Meer informatie kunt u deze status tooget selecteren.</span><span class="sxs-lookup"><span data-stu-id="b55a2-110">You can select this status tooget more details.</span></span>
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="b55a2-112">U ziet Hallo recente geschiedenis van implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-112">You see hello recent deployment history.</span></span> <span data-ttu-id="b55a2-113">Selecteer Hallo-implementatie die niet zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="b55a2-113">Select hello deployment that failed.</span></span>
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="b55a2-115">Selecteer Hallo koppeling toosee een beschrijving van waarom Hallo implementatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="b55a2-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="b55a2-116">In onderstaande Hallo afbeelding is Hallo DNS-record niet uniek.</span><span class="sxs-lookup"><span data-stu-id="b55a2-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![mislukte implementatie weergeven](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="b55a2-118">Dit foutbericht moeten voldoende zijn voor u toobegin het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="b55a2-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="b55a2-119">Echter, als u meer informatie over welke taken zijn voltooid, vindt u Hallo bewerkingen zoals weergegeven in de volgende stappen uit Hallo.</span><span class="sxs-lookup"><span data-stu-id="b55a2-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="b55a2-120">U kunt alle Hallo implementatiebewerkingen weergeven in Hallo **implementatie** blade.</span><span class="sxs-lookup"><span data-stu-id="b55a2-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="b55a2-121">Selecteer een bewerking toosee meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-121">Select any operation toosee more details.</span></span>
   
    ![bewerkingen weergeven](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="b55a2-123">In dit geval zien u dat Hallo storage-account, het virtuele netwerk en beschikbaarheidsset zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b55a2-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="b55a2-124">Hallo openbaar IP-adres is mislukt en andere resources zijn niet is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b55a2-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="b55a2-125">U kunt gebeurtenissen voor Hallo implementatie bekijken door te selecteren **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="b55a2-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![gebeurtenissen weergeven](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="b55a2-127">U alle Hallo gebeurtenissen voor Hallo implementatie zien en selecteert u een voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="b55a2-128">U ziet te Hallo correlatie-id's.</span><span class="sxs-lookup"><span data-stu-id="b55a2-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="b55a2-129">Deze waarde kan nuttig zijn bij het werken met de technische ondersteuning tootroubleshoot een implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![Zie gebeurtenissen](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="b55a2-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b55a2-131">PowerShell</span></span>
1. <span data-ttu-id="b55a2-132">tooget Hallo algehele status van een implementatie, gebruik Hallo **Get-AzureRmResourceGroupDeployment** opdracht.</span><span class="sxs-lookup"><span data-stu-id="b55a2-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="b55a2-133">Of u kunt filteren Hallo resultaten voor alleen deze implementaties die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="b55a2-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="b55a2-134">Elke implementatie bevat meerdere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b55a2-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="b55a2-135">Elke bewerking vertegenwoordigt een stap in het implementatieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="b55a2-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="b55a2-136">toodiscover wat gegaan met een implementatie, moet u meestal toosee details over Hallo implementatiebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="b55a2-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="b55a2-137">U kunt zien Hallo-status van het Hallo-bewerkingen met **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="b55a2-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="b55a2-138">Dat meerdere bewerkingen met elkaar Hallo na indeling geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b55a2-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="b55a2-139">tooget voor meer informatie over mislukte bewerkingen Hallo-eigenschappen voor bewerkingen met ophalen **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="b55a2-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="b55a2-140">Dit retourneert dat alle mislukte bewerkingen die met elkaar in de volgende indeling Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="b55a2-140">Which returns all hello failed operations with each one in hello following format:</span></span>

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

    <span data-ttu-id="b55a2-141">Houd er rekening mee Hallo serviceRequestId en Hallo trackingId voor Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b55a2-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="b55a2-142">Hallo serviceRequestId kan nuttig zijn bij het werken met de technische ondersteuning tootroubleshoot een implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="b55a2-143">Hallo trackingId gebruikt u in de volgende stap toofocus Hallo op een bepaalde bewerking.</span><span class="sxs-lookup"><span data-stu-id="b55a2-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="b55a2-144">Hallo statusbericht tooget van een bepaalde mislukte bewerking gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="b55a2-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="b55a2-145">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b55a2-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="b55a2-146">Elke implementatiebewerking in Azure bevat-aanvraag en antwoord-inhoud.</span><span class="sxs-lookup"><span data-stu-id="b55a2-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="b55a2-147">Hallo aanvraaginhoud is wat u verzonden tooAzure tijdens de implementatie (bijvoorbeeld: Maak een VM besturingssysteemschijf en andere bronnen).</span><span class="sxs-lookup"><span data-stu-id="b55a2-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="b55a2-148">Hallo antwoordinhoud is wat Azure van uw implementatieaanvraag teruggestuurd.</span><span class="sxs-lookup"><span data-stu-id="b55a2-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="b55a2-149">Tijdens de implementatie, kunt u **DeploymentDebugLogLevel** parameter worden toospecify die Hallo aanvraag en/of antwoord in logboek Hallo worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="b55a2-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="b55a2-150">U die gegevens ophalen uit Hallo-logboek en sla het lokaal via Hallo volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b55a2-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="b55a2-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b55a2-151">Azure CLI</span></span>

1. <span data-ttu-id="b55a2-152">Ophalen van algemene status van een implementatie met Hallo Hallo **azure-groep implementatie weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="b55a2-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="b55a2-153">Een van de waarden geretourneerd Hallo Hallo is **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="b55a2-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="b55a2-154">Deze waarde wordt gebruikt tootrack gerelateerde gebeurtenissen en kan handig zijn wanneer werken met de technische ondersteuning tootroubleshoot een implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="b55a2-155">toosee hello bewerkingen voor een implementatie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="b55a2-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="b55a2-156">REST</span><span class="sxs-lookup"><span data-stu-id="b55a2-156">REST</span></span>

1. <span data-ttu-id="b55a2-157">Informatie ophalen over een implementatie met Hallo [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="b55a2-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="b55a2-158">Hallo reactie, houd er rekening mee in het bijzonder Hallo **provisioningState**, **correlationId**, en **fout** elementen.</span><span class="sxs-lookup"><span data-stu-id="b55a2-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="b55a2-159">Hallo **correlationId** wordt gebruikt tootrack gerelateerde gebeurtenissen en kan handig zijn wanneer werken met de technische ondersteuning tootroubleshoot een implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="b55a2-160">Informatie ophalen over implementatiebewerkingen Hello [lijst van alle implementatiebewerkingen voor sjabloon](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) bewerking.</span><span class="sxs-lookup"><span data-stu-id="b55a2-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="b55a2-161">Hallo-antwoord bevat de aanvraag en/of antwoord informatie op basis van wat u hebt opgegeven in Hallo **debugSetting** eigenschap tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="b55a2-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="b55a2-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b55a2-162">Next steps</span></span>
* <span data-ttu-id="b55a2-163">Zie voor meer informatie over het oplossen van fouten voor bepaalde implementatie, [oplossen van veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="b55a2-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="b55a2-164">toolearn over het gebruik van de activiteit Hallo registreert toomonitor andere soorten acties, Zie [activiteit weergeven logboeken toomanage Azure resources](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="b55a2-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="b55a2-165">toovalidate uw implementatie alvorens uit te voeren, Zie [een resourcegroep implementeren met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="b55a2-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

