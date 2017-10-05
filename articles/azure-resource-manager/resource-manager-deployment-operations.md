---
title: Implementatiebewerkingen met Azure Resource Manager | Microsoft Docs
description: Hierin wordt beschreven hoe u Azure Resource Manager deployment bewerkingen met de portal, PowerShell, Azure CLI en REST-API.
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="15c54-103">Bewerkingen van de implementatie weergeven met Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="15c54-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="15c54-104">U kunt de bewerkingen voor een implementatie via de Azure portal bekijken.</span><span class="sxs-lookup"><span data-stu-id="15c54-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="15c54-105">Hebt u mogelijk de meest geïnteresseerd in de bewerkingen weer te geven wanneer u een fout opgetreden tijdens de implementatie ontvangen hebt zodat dit artikel is gericht op het weergeven van bewerkingen die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="15c54-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="15c54-106">De portal biedt een interface waarmee u eenvoudig zoeken van de fouten en mogelijke oplossingen te bepalen.</span><span class="sxs-lookup"><span data-stu-id="15c54-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="15c54-107">Portal</span><span class="sxs-lookup"><span data-stu-id="15c54-107">Portal</span></span>
<span data-ttu-id="15c54-108">Als de implementatiebewerkingen weergeven, gebruikt u de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="15c54-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="15c54-109">U ziet de status van de laatste implementatie voor de resourcegroep die zijn betrokken bij de implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="15c54-110">U kunt deze status voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-110">You can select this status to get more details.</span></span>
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="15c54-112">Ziet u de recente implementatiegeschiedenis van de.</span><span class="sxs-lookup"><span data-stu-id="15c54-112">You see the recent deployment history.</span></span> <span data-ttu-id="15c54-113">Selecteer de implementatie die is mislukt.</span><span class="sxs-lookup"><span data-stu-id="15c54-113">Select the deployment that failed.</span></span>
   
    ![Implementatiestatus](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="15c54-115">Selecteer de koppeling voor een beschrijving van waarom de implementatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="15c54-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="15c54-116">De DNS-record is niet uniek in de onderstaande afbeelding.</span><span class="sxs-lookup"><span data-stu-id="15c54-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![mislukte implementatie weergeven](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="15c54-118">Dit foutbericht moeten voldoende voor u om te beginnen met het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="15c54-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="15c54-119">Als u meer informatie nodig over welke taken zijn voltooid, kunt u de bewerkingen weergeven zoals weergegeven in de volgende stappen uit.</span><span class="sxs-lookup"><span data-stu-id="15c54-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="15c54-120">U ziet de implementatiebewerkingen in de **implementatie** blade.</span><span class="sxs-lookup"><span data-stu-id="15c54-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="15c54-121">Selecteer een bewerking voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-121">Select any operation to see more details.</span></span>
   
    ![bewerkingen weergeven](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="15c54-123">In dit geval zien u dat de storage-account, het virtuele netwerk en de beschikbaarheidsset zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="15c54-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="15c54-124">Het openbare IP-adres is mislukt en andere resources zijn niet is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="15c54-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="15c54-125">U kunt gebeurtenissen voor de implementatie weergeven door **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="15c54-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![gebeurtenissen weergeven](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="15c54-127">U selecteert een voor meer informatie en Zie de gebeurtenissen voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="15c54-128">U ziet te de correlatie-id's.</span><span class="sxs-lookup"><span data-stu-id="15c54-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="15c54-129">Deze waarde kan nuttig zijn bij het werken met de technische ondersteuning voor het oplossen van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![Zie gebeurtenissen](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="15c54-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="15c54-131">PowerShell</span></span>
1. <span data-ttu-id="15c54-132">Als u de algehele status van een implementatie, gebruikt de **Get-AzureRmResourceGroupDeployment** opdracht.</span><span class="sxs-lookup"><span data-stu-id="15c54-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="15c54-133">Of u kunt de resultaten filteren voor alleen deze implementaties die zijn mislukt.</span><span class="sxs-lookup"><span data-stu-id="15c54-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="15c54-134">Elke implementatie bevat meerdere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="15c54-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="15c54-135">Elke bewerking vertegenwoordigt een stap in het implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="15c54-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="15c54-136">Om te ontdekken wat is een fout opgetreden bij een implementatie, moet u doorgaans om details over de implementatiebewerkingen te bekijken.</span><span class="sxs-lookup"><span data-stu-id="15c54-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="15c54-137">U ziet de status van de bewerkingen met **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="15c54-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="15c54-138">Dit retourneert meerdere bewerkingen met elkaar in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="15c54-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="15c54-139">Als u meer informatie over mislukte bewerkingen, halen de eigenschappen voor bewerkingen met **mislukt** status.</span><span class="sxs-lookup"><span data-stu-id="15c54-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="15c54-140">Dit retourneert alle mislukte bewerkingen met elkaar in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="15c54-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="15c54-141">Noteer de serviceRequestId en de trackingId voor de bewerking.</span><span class="sxs-lookup"><span data-stu-id="15c54-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="15c54-142">De serviceRequestId kan nuttig zijn bij het werken met de technische ondersteuning voor het oplossen van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="15c54-143">U gebruikt de trackingId in de volgende stap om zich te richten op een bepaalde bewerking.</span><span class="sxs-lookup"><span data-stu-id="15c54-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="15c54-144">Als u het statusbericht dat van een bepaalde bewerking is mislukt, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="15c54-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="15c54-145">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="15c54-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="15c54-146">Elke implementatiebewerking in Azure bevat-aanvraag en antwoord-inhoud.</span><span class="sxs-lookup"><span data-stu-id="15c54-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="15c54-147">Inhoud van de aanvraag is wat u hebt verzonden naar Azure tijdens de implementatie (bijvoorbeeld: Maak een VM besturingssysteemschijf en andere bronnen).</span><span class="sxs-lookup"><span data-stu-id="15c54-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="15c54-148">De antwoordinhoud is wat Azure van uw implementatieaanvraag teruggestuurd.</span><span class="sxs-lookup"><span data-stu-id="15c54-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="15c54-149">Tijdens de implementatie, kunt u **DeploymentDebugLogLevel** parameter worden om op te geven dat de aanvraag en/of antwoord in het logboek behouden blijven.</span><span class="sxs-lookup"><span data-stu-id="15c54-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="15c54-150">U die informatie ophalen van het logboek, en sla het lokaal met behulp van de volgende PowerShell-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="15c54-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="15c54-151">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="15c54-151">Azure CLI</span></span>

1. <span data-ttu-id="15c54-152">Ophalen van de algehele status van een implementatie met de **azure-groep implementatie weergeven** opdracht.</span><span class="sxs-lookup"><span data-stu-id="15c54-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="15c54-153">Een van de geretourneerde waarden is de **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="15c54-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="15c54-154">Deze waarde wordt gebruikt voor het bijhouden van gerelateerde gebeurtenissen en kan nuttig zijn bij het werken met de technische ondersteuning voor het oplossen van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="15c54-155">Als de bewerkingen voor een implementatie wilt weergeven, gebruikt u het:</span><span class="sxs-lookup"><span data-stu-id="15c54-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="15c54-156">REST</span><span class="sxs-lookup"><span data-stu-id="15c54-156">REST</span></span>

1. <span data-ttu-id="15c54-157">Informatie ophalen over een implementatie met de [informatie ophalen over de sjabloonimplementatie van een](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) bewerking.</span><span class="sxs-lookup"><span data-stu-id="15c54-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="15c54-158">In het antwoord, houd er rekening mee met name de **provisioningState**, **correlationId**, en **fout** elementen.</span><span class="sxs-lookup"><span data-stu-id="15c54-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="15c54-159">De **correlationId** wordt gebruikt voor het bijhouden van gerelateerde gebeurtenissen en kan nuttig zijn bij het werken met de technische ondersteuning voor het oplossen van een implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="15c54-160">Informatie ophalen over de implementatiebewerkingen met de [lijst van alle implementatiebewerkingen voor sjabloon](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) bewerking.</span><span class="sxs-lookup"><span data-stu-id="15c54-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="15c54-161">Het antwoord bevat de aanvraag en/of antwoord informatie op basis van wat u hebt opgegeven in de **debugSetting** eigenschap tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="15c54-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="15c54-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="15c54-162">Next steps</span></span>
* <span data-ttu-id="15c54-163">Zie voor meer informatie over het oplossen van fouten voor bepaalde implementatie, [oplossen van veelvoorkomende fouten bij het implementeren van resources in Azure met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="15c54-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="15c54-164">Zie voor meer informatie over het gebruik van de activiteitenlogboeken van de voor het bewaken van andere soorten acties, [activiteitenlogboeken voor het beheren van Azure-resources bekijken](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="15c54-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="15c54-165">Zie voor het valideren van uw implementatie voordat deze wordt uitgevoerd, [een resourcegroep implementeren met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="15c54-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

