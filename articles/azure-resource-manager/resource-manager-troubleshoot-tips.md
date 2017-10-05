---
title: Fouten van de Azure-implementatie begrijpen | Microsoft Docs
description: Beschrijft hoe u meer informatie over Azure-implementatiefouten.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren in azure
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: b67bb30fa259fa08e37e11afec724c8b8c3eb633
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="3c11e-104">Fouten van de Azure-implementatie begrijpen</span><span class="sxs-lookup"><span data-stu-id="3c11e-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="3c11e-105">Dit onderwerp beschrijft implementatiefouten en hoe u meer informatie over een fout kunt detecteren.</span><span class="sxs-lookup"><span data-stu-id="3c11e-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="3c11e-106">Zie voor oplossingen voor algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="3c11e-106">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="3c11e-107">Twee soorten fouten</span><span class="sxs-lookup"><span data-stu-id="3c11e-107">Two types of errors</span></span>
<span data-ttu-id="3c11e-108">Er zijn twee typen fouten die u kunt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="3c11e-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="3c11e-109">Validatiefouten</span><span class="sxs-lookup"><span data-stu-id="3c11e-109">validation errors</span></span>
* <span data-ttu-id="3c11e-110">Implementatiefouten</span><span class="sxs-lookup"><span data-stu-id="3c11e-110">deployment errors</span></span>

<span data-ttu-id="3c11e-111">De volgende afbeelding ziet u het logboek voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="3c11e-111">The following image shows the activity log for a subscription.</span></span> <span data-ttu-id="3c11e-112">Hiermee geeft u twee implementaties.</span><span class="sxs-lookup"><span data-stu-id="3c11e-112">It represents two deployments.</span></span> <span data-ttu-id="3c11e-113">In een implementatie van de sjabloon validatie is mislukt (**valideren**) en niet worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="3c11e-113">In one deployment, the template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="3c11e-114">In de andere implementatie van de sjabloon gevalideerd, maar is mislukt bij het maken van de resources (**schrijven implementaties**).</span><span class="sxs-lookup"><span data-stu-id="3c11e-114">In the other deployment, the template passed validation but failed when creating the resources (**Write Deployments**).</span></span> 

![foutcode weergeven](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="3c11e-116">Validatiefouten worden veroorzaakt door scenario's die vóór de implementatie kunnen worden bepaald.</span><span class="sxs-lookup"><span data-stu-id="3c11e-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="3c11e-117">Ze bevatten syntaxisfouten in de sjabloon of het implementeren van resources die uw abonnement quota's zou overschrijden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-117">They include syntax errors in your template, or trying to deploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="3c11e-118">Implementatiefouten worden veroorzaakt door de voorwaarden die tijdens de implementatie optreden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-118">Deployment errors arise from conditions that occur during the deployment process.</span></span> <span data-ttu-id="3c11e-119">Ze bevatten toegang wilt krijgen tot een resource die parallel wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c11e-119">They include trying to access a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="3c11e-120">Beide soorten fouten retourneren een foutcode die u gebruikt voor het oplossen van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-120">Both types of errors return an error code that you use to troubleshoot the deployment.</span></span> <span data-ttu-id="3c11e-121">Beide soorten fouten worden weergegeven in de [activiteitenlogboek](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="3c11e-121">Both types of errors appear in the [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="3c11e-122">Validatiefouten worden echter niet weergegeven in de geschiedenis van uw implementatie omdat de implementatie is nooit gestart.</span><span class="sxs-lookup"><span data-stu-id="3c11e-122">However, validation errors do not appear in your deployment history because the deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="3c11e-123">Foutcode bepalen</span><span class="sxs-lookup"><span data-stu-id="3c11e-123">Determine error code</span></span>

<span data-ttu-id="3c11e-124">U kunt meer informatie over een fout door te kijken naar het foutbericht en de foutcode.</span><span class="sxs-lookup"><span data-stu-id="3c11e-124">You can learn about an error by looking at the error message and the error code.</span></span> <span data-ttu-id="3c11e-125">De [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md) artikel geeft oplossingen-foutcode.</span><span class="sxs-lookup"><span data-stu-id="3c11e-125">The [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="3c11e-126">Dit onderwerp leest hoe de Azure portal gebruiken voor het detecteren van de foutcode.</span><span class="sxs-lookup"><span data-stu-id="3c11e-126">This topic shows how to use the Azure portal to discover the error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="3c11e-127">Validatiefouten</span><span class="sxs-lookup"><span data-stu-id="3c11e-127">Validation errors</span></span>

<span data-ttu-id="3c11e-128">Bij het implementeren via de portal, ziet u een validatiefout opgetreden na het verzenden van uw waarden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-128">When deploying through the portal, you see a validation error after submitting your values.</span></span>

![Fout bij de portal validatie weergeven](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="3c11e-130">Selecteer het bericht voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-130">Select the message for more details.</span></span> <span data-ttu-id="3c11e-131">In de volgende afbeelding ziet u een **InvalidTemplateDeployment** fout en een bericht verschijnt dat een beleid voor implementatie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="3c11e-131">In the following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![validatie details weergeven](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="3c11e-133">Implementatiefouten</span><span class="sxs-lookup"><span data-stu-id="3c11e-133">Deployment errors</span></span>

<span data-ttu-id="3c11e-134">Als de bewerking is geslaagd, maar niet tijdens de implementatie, ziet u de fout in de meldingen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-134">When the operation passes validation, but fails during deployment, you see the error in the notifications.</span></span> <span data-ttu-id="3c11e-135">Selecteer de melding.</span><span class="sxs-lookup"><span data-stu-id="3c11e-135">Select the notification.</span></span>

![Fout bij wijzigingsbericht](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="3c11e-137">Er is meer informatie over de implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-137">You see more details about the deployment.</span></span> <span data-ttu-id="3c11e-138">Selecteer de optie voor meer informatie over de fout.</span><span class="sxs-lookup"><span data-stu-id="3c11e-138">Select the option to find more information about the error.</span></span>

![implementatie is mislukt](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="3c11e-140">Ziet u de foutmelding en foutcodes.</span><span class="sxs-lookup"><span data-stu-id="3c11e-140">You see the error message and error codes.</span></span> <span data-ttu-id="3c11e-141">Er zijn twee foutcodes.</span><span class="sxs-lookup"><span data-stu-id="3c11e-141">Notice there are two error codes.</span></span> <span data-ttu-id="3c11e-142">De eerste foutcode (**implementatie mislukt**) is een algemene fout die biedt geen informatie die u nodig hebt voor het oplossen van de fout.</span><span class="sxs-lookup"><span data-stu-id="3c11e-142">The first error code (**DeploymentFailed**) is a general error that does not provide the details you need to solve the error.</span></span> <span data-ttu-id="3c11e-143">De tweede foutcode (**StorageAccountNotFound**) bevat de details die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="3c11e-143">The second error code (**StorageAccountNotFound**) provides the details you need.</span></span> 

![Details van fouten](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="3c11e-145">Inschakelen van logboekregistratie voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="3c11e-145">Enable debug logging</span></span>
<span data-ttu-id="3c11e-146">Soms moet u meer informatie over de aanvraag en -antwoord om te ontdekken wat er mis ging.</span><span class="sxs-lookup"><span data-stu-id="3c11e-146">Sometimes you need more information about the request and response to discover what went wrong.</span></span> <span data-ttu-id="3c11e-147">U kunt met behulp van PowerShell of Azure CLI aanvragen dat aanvullende informatie wordt geregistreerd tijdens een implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="3c11e-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3c11e-148">PowerShell</span></span>

   <span data-ttu-id="3c11e-149">In PowerShell, stelt u de **DeploymentDebugLogLevel** parameter naar alle, ResponseContent of RequestContent.</span><span class="sxs-lookup"><span data-stu-id="3c11e-149">In PowerShell, set the **DeploymentDebugLogLevel** parameter to All, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="3c11e-150">Controleer de aanvraag van inhoud met de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3c11e-150">Examine the request content with the following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="3c11e-151">Of het antwoord inhoud met:</span><span class="sxs-lookup"><span data-stu-id="3c11e-151">Or, the response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="3c11e-152">Deze informatie kunt u bepalen of een waarde in de sjabloon niet correct wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3c11e-152">This information can help you determine whether a value in the template is being incorrectly set.</span></span>

- <span data-ttu-id="3c11e-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3c11e-153">Azure CLI</span></span>

   <span data-ttu-id="3c11e-154">Controleer de implementatiebewerkingen met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3c11e-154">Examine the deployment operations with the following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="3c11e-155">Geneste sjabloon</span><span class="sxs-lookup"><span data-stu-id="3c11e-155">Nested template</span></span>

   <span data-ttu-id="3c11e-156">Meld u foutopsporingsgegevens voor een geneste sjabloon met de **debugSetting** element.</span><span class="sxs-lookup"><span data-stu-id="3c11e-156">To log debug information for a nested template, use the **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="3c11e-157">Maken van een sjabloon voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="3c11e-157">Create a troubleshooting template</span></span>
<span data-ttu-id="3c11e-158">In sommige gevallen is de eenvoudigste manier om op te lossen, de sjabloon voor het testen van de onderdelen hiervan.</span><span class="sxs-lookup"><span data-stu-id="3c11e-158">In some cases, the easiest way to troubleshoot your template is to test parts of it.</span></span> <span data-ttu-id="3c11e-159">U kunt maken als een vereenvoudigde sjabloon waarmee u zich kunt richten op het onderdeel dat u denkt dat de fout wordt veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="3c11e-159">You can create a simplified template that enables you to focus on the part that you believe is causing the error.</span></span> <span data-ttu-id="3c11e-160">Stel bijvoorbeeld dat u ontvangt een fout opgetreden bij het verwijzen naar een resource.</span><span class="sxs-lookup"><span data-stu-id="3c11e-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="3c11e-161">In plaats van te moeten omgaan met een volledige sjabloon, een sjabloon die als resultaat geeft het onderdeel dat wordt veroorzaakt door het probleem te maken.</span><span class="sxs-lookup"><span data-stu-id="3c11e-161">Rather than dealing with an entire template, create a template that returns the part that may be causing your problem.</span></span> <span data-ttu-id="3c11e-162">Dit kunt u bepalen of u doorgeeft aan de juiste parameters met sjabloonfuncties correct en ophalen van de resource die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="3c11e-162">It can help you determine whether you are passing in the right parameters, using template functions correctly, and getting the resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="3c11e-163">Of stel fouten implementatie die u van mening zijn gerelateerd bent aan afhankelijkheden niet correct instellen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-163">Or, suppose you are encountering deployment errors that you believe are related to incorrectly set dependencies.</span></span> <span data-ttu-id="3c11e-164">Test uw sjabloon door in vereenvoudigde sjablonen op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="3c11e-165">Maak eerst een sjabloon die slechts één bron (zoals een SQL-Server) implementeert.</span><span class="sxs-lookup"><span data-stu-id="3c11e-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="3c11e-166">Als u zeker dat u die correct gedefinieerd resource hebt, kunt u een resource die afhankelijk zijn van deze (zoals een SQL-Database) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="3c11e-167">Wanneer u deze twee bronnen onjuist is gedefinieerd hebt, moet u andere afhankelijke resources (zoals controlebeleid) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="3c11e-168">Verwijder de resourcegroep om te controleren of u voldoende testen van de afhankelijkheden tussen elke testimplementatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-168">In between each test deployment, delete the resource group to make sure you adequately testing the dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="3c11e-169">Controleer de volgorde van de implementatie</span><span class="sxs-lookup"><span data-stu-id="3c11e-169">Check deployment sequence</span></span>

<span data-ttu-id="3c11e-170">Veel implementatiefouten gebeuren wanneer een onverwachte reeks resources worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c11e-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="3c11e-171">Deze fouten zich voordoen als afhankelijkheden niet correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3c11e-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="3c11e-172">Wanneer er ontbreekt een vereiste afhankelijkheid, kunt u één resource probeert te gebruiken van een waarde voor een andere bron, maar de andere nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c11e-172">When you are missing a needed dependency, one resource attempts to use a value for another resource but the other does not yet exist.</span></span> <span data-ttu-id="3c11e-173">U krijgt een foutmelding weergegeven dat een bron is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="3c11e-174">U kunt dit type fout afwisselend tegenkomen, omdat het tijdstip waarop de implementatie voor elke resource kan verschillen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-174">You may encounter this type of error intermittently because the deployment time for each resource can vary.</span></span> <span data-ttu-id="3c11e-175">Uw eerste poging tot het implementeren van uw resources slaagt bijvoorbeeld omdat een vereiste bron willekeurig tijdstip is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c11e-175">For example, your first attempt to deploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="3c11e-176">Echter, de tweede poging mislukt, omdat de vereiste bron is niet op tijd voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c11e-176">However, your second attempt fails because the required resource did not complete in time.</span></span> 

<span data-ttu-id="3c11e-177">Maar u wilt voorkomen dat afhankelijkheden die nodig zijn niet instellen.</span><span class="sxs-lookup"><span data-stu-id="3c11e-177">But, you want to avoid setting dependencies that are not needed.</span></span> <span data-ttu-id="3c11e-178">Wanneer u onnodige afhankelijkheden hebt, kunt u de duur van de implementatie verlengen door te voorkomen dat de bronnen die niet afhankelijk van elkaar worden geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="3c11e-178">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="3c11e-179">U kunt bovendien circulaire afhankelijkheden die de implementatie blokkeren maken.</span><span class="sxs-lookup"><span data-stu-id="3c11e-179">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="3c11e-180">De [verwijzing](resource-group-template-functions-resource.md#reference) functie maakt een impliciete afhankelijkheid voor de bron waarnaar wordt verwezen, wanneer deze resource is geïmplementeerd in dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3c11e-180">The [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on the referenced resource, when that resource is deployed in the same template.</span></span> <span data-ttu-id="3c11e-181">Daarom kunnen er meer afhankelijkheden dan de afhankelijkheden die zijn opgegeven de **dependsOn** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3c11e-181">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="3c11e-182">De [resourceId](resource-group-template-functions-resource.md#resourceid) functie niet maken van een impliciete afhankelijkheid of valideren dat de resource bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c11e-182">The [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that the resource exists.</span></span>

<span data-ttu-id="3c11e-183">Wanneer u afhankelijkheid problemen ondervindt, moet u meer inzicht krijgen in de volgorde van de resource-implementatie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-183">When you encounter dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="3c11e-184">De volgorde van implementatiebewerkingen weergeven:</span><span class="sxs-lookup"><span data-stu-id="3c11e-184">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="3c11e-185">Selecteer de geschiedenis van de implementatie voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3c11e-185">Select the deployment history for your resource group.</span></span>

   ![Geschiedenis van implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="3c11e-187">Selecteer een implementatie van de geschiedenis en selecteer **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="3c11e-187">Select a deployment from the history, and select **Events**.</span></span>

   ![gebeurtenissen van de implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="3c11e-189">Controleer de volgorde van gebeurtenissen voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="3c11e-189">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="3c11e-190">Let op de status van elke bewerking.</span><span class="sxs-lookup"><span data-stu-id="3c11e-190">Pay attention to the status of each operation.</span></span> <span data-ttu-id="3c11e-191">De volgende afbeelding ziet u bijvoorbeeld drie storage-accounts die geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="3c11e-191">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="3c11e-192">U ziet dat de drie storage-accounts op hetzelfde moment worden gestart.</span><span class="sxs-lookup"><span data-stu-id="3c11e-192">Notice that the three storage accounts are started at the same time.</span></span>

   ![Parallelle implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="3c11e-194">De volgende afbeelding ziet u drie opslagaccounts die niet zijn geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="3c11e-194">The next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="3c11e-195">Het tweede storage-account is afhankelijk van het eerste storage-account en het derde storage-account is afhankelijk van de tweede storage-account.</span><span class="sxs-lookup"><span data-stu-id="3c11e-195">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="3c11e-196">Daarom wordt het eerste opslagaccount gestart, geaccepteerd en voltooid voordat de volgende is gestart.</span><span class="sxs-lookup"><span data-stu-id="3c11e-196">Therefore, the first storage account is started, accepted, and completed before the next is started.</span></span>

   ![sequentiële implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="3c11e-198">Zelfs voor complexere scenario's, kunt u dezelfde techniek gebruiken om te detecteren wanneer de implementatie wordt gestart en voltooid voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="3c11e-198">Even for more complicated scenarios, you can use the same technique to discover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="3c11e-199">Bekijk de gebeurtenissen van uw implementatie om te zien als de volgorde anders is dan u verwacht.</span><span class="sxs-lookup"><span data-stu-id="3c11e-199">Look through your deployment events to see if the sequence is different than you would expect.</span></span> <span data-ttu-id="3c11e-200">Zo ja, Herzie de afhankelijkheden voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="3c11e-200">If so, reevaluate the dependencies for this resource.</span></span>

<span data-ttu-id="3c11e-201">Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3c11e-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="3c11e-202">Retourneert een foutbericht weergegeven waarin wordt vermeld specifiek een circulaire afhankelijkheid bestaat.</span><span class="sxs-lookup"><span data-stu-id="3c11e-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="3c11e-203">Voor het oplossen van een circulaire afhankelijkheid:</span><span class="sxs-lookup"><span data-stu-id="3c11e-203">To solve a circular dependency:</span></span>

1. <span data-ttu-id="3c11e-204">In de sjabloon de bron die is geïdentificeerd in de circulaire afhankelijkheid te vinden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-204">In your template, find the resource identified in the circular dependency.</span></span> 
2. <span data-ttu-id="3c11e-205">Voor die bron onderzoekt de **dependsOn** eigenschap en het gebruik van de **verwijzing** om te zien welke resources afhankelijk van is de functie.</span><span class="sxs-lookup"><span data-stu-id="3c11e-205">For that resource, examine the **dependsOn** property and any uses of the **reference** function to see which resources it depends on.</span></span> 
3. <span data-ttu-id="3c11e-206">Controleer deze bronnen om te zien welke bronnen ze afhankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="3c11e-206">Examine those resources to see which resources they depend on.</span></span> <span data-ttu-id="3c11e-207">Volg de afhankelijkheden totdat er een resource die afhankelijk van de oorspronkelijke bron is.</span><span class="sxs-lookup"><span data-stu-id="3c11e-207">Follow the dependencies until you notice a resource that depends on the original resource.</span></span>
5. <span data-ttu-id="3c11e-208">Voor de resources die zijn betrokken bij de circulaire afhankelijkheid zorgvuldig al gebruik van de **dependsOn** eigenschap voor het identificeren van eventuele afhankelijkheden die niet nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="3c11e-208">For the resources involved in the circular dependency, carefully examine all uses of the **dependsOn** property to identify any dependencies that are not needed.</span></span> <span data-ttu-id="3c11e-209">Verwijder deze afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="3c11e-209">Remove those dependencies.</span></span> <span data-ttu-id="3c11e-210">Als u niet zeker weet dat er een afhankelijkheid is vereist, probeert u het verwijdert.</span><span class="sxs-lookup"><span data-stu-id="3c11e-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="3c11e-211">De sjabloon opnieuw implementeert.</span><span class="sxs-lookup"><span data-stu-id="3c11e-211">Redeploy the template.</span></span>

<span data-ttu-id="3c11e-212">Verwijderen van de waarden uit de **dependsOn** eigenschap kan fouten veroorzaken wanneer u de sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="3c11e-212">Removing values from the **dependsOn** property can cause errors when you deploy the template.</span></span> <span data-ttu-id="3c11e-213">Als u er een fout optreedt, voegt u de afhankelijkheid terug naar de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3c11e-213">If you encounter an error, add the dependency back into the template.</span></span> 

<span data-ttu-id="3c11e-214">Als deze aanpak circulaire afhankelijkheid niet wordt opgelost, kunt u deel uitmaakt van uw implementatie logica verplaatsen naar onderliggende resources (zoals extensies of configuratie-instellingen).</span><span class="sxs-lookup"><span data-stu-id="3c11e-214">If that approach does not solve the circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="3c11e-215">Deze onderliggende resources implementeren na de resources die zijn betrokken bij de circulaire afhankelijkheid configureren.</span><span class="sxs-lookup"><span data-stu-id="3c11e-215">Configure those child resources to deploy after the resources involved in the circular dependency.</span></span> <span data-ttu-id="3c11e-216">Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk criterium die verwijzen naar de andere.</span><span class="sxs-lookup"><span data-stu-id="3c11e-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="3c11e-217">U kunt deze implementeren in de volgende volgorde:</span><span class="sxs-lookup"><span data-stu-id="3c11e-217">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="3c11e-218">vm1</span><span class="sxs-lookup"><span data-stu-id="3c11e-218">vm1</span></span>
2. <span data-ttu-id="3c11e-219">vm2</span><span class="sxs-lookup"><span data-stu-id="3c11e-219">vm2</span></span>
3. <span data-ttu-id="3c11e-220">Extensie op vm1, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="3c11e-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="3c11e-221">De extensie waarden ingesteld op vm1 die van vm2 krijgt.</span><span class="sxs-lookup"><span data-stu-id="3c11e-221">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="3c11e-222">Extensie op vm2, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="3c11e-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="3c11e-223">De extensie waarden ingesteld op vm2 van van vm1 krijgt.</span><span class="sxs-lookup"><span data-stu-id="3c11e-223">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="3c11e-224">Dezelfde manier werkt voor App Service-apps.</span><span class="sxs-lookup"><span data-stu-id="3c11e-224">The same approach works for App Service apps.</span></span> <span data-ttu-id="3c11e-225">Overweeg configuratiewaarden verplaatsen naar een onderliggende resource van resource voor de app.</span><span class="sxs-lookup"><span data-stu-id="3c11e-225">Consider moving configuration values into a child resource of the app resource.</span></span> <span data-ttu-id="3c11e-226">U kunt twee web-apps in de volgende volgorde kunt implementeren:</span><span class="sxs-lookup"><span data-stu-id="3c11e-226">You can deploy two web apps in the following order:</span></span>

1. <span data-ttu-id="3c11e-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="3c11e-227">webapp1</span></span>
2. <span data-ttu-id="3c11e-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="3c11e-228">webapp2</span></span>
3. <span data-ttu-id="3c11e-229">configuratie voor webapp1, is afhankelijk van webapp1 en webapp2.</span><span class="sxs-lookup"><span data-stu-id="3c11e-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="3c11e-230">Het bevat app-instellingen met waarden uit webapp2.</span><span class="sxs-lookup"><span data-stu-id="3c11e-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="3c11e-231">configuratie voor webapp2, is afhankelijk van webapp1 en webapp2.</span><span class="sxs-lookup"><span data-stu-id="3c11e-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="3c11e-232">Het bevat app-instellingen met waarden uit webapp1.</span><span class="sxs-lookup"><span data-stu-id="3c11e-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="3c11e-233">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c11e-233">Next steps</span></span>
* <span data-ttu-id="3c11e-234">Zie voor oplossingen voor algemene implementatiefouten [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="3c11e-234">For resolutions to common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="3c11e-235">Zie voor meer informatie over het controleren van acties, [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="3c11e-235">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="3c11e-236">Zie voor meer informatie over acties om de fouten tijdens de implementatie, [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="3c11e-236">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
