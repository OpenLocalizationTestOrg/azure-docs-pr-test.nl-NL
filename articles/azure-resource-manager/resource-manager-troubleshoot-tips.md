---
title: de Azure implementatiefouten aaaUnderstand | Microsoft Docs
description: Hierin wordt beschreven hoe toolearn over Azure-implementatiefouten.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren tooazure
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="8f6df-104">Fouten van de Azure-implementatie begrijpen</span><span class="sxs-lookup"><span data-stu-id="8f6df-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="8f6df-105">Dit onderwerp beschrijft implementatiefouten en hoe u meer informatie over een fout kunt detecteren.</span><span class="sxs-lookup"><span data-stu-id="8f6df-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="8f6df-106">Zie voor oplossingen toocommon implementatiefouten, [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="8f6df-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="8f6df-107">Twee soorten fouten</span><span class="sxs-lookup"><span data-stu-id="8f6df-107">Two types of errors</span></span>
<span data-ttu-id="8f6df-108">Er zijn twee typen fouten die u kunt ontvangen:</span><span class="sxs-lookup"><span data-stu-id="8f6df-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="8f6df-109">Validatiefouten</span><span class="sxs-lookup"><span data-stu-id="8f6df-109">validation errors</span></span>
* <span data-ttu-id="8f6df-110">Implementatiefouten</span><span class="sxs-lookup"><span data-stu-id="8f6df-110">deployment errors</span></span>

<span data-ttu-id="8f6df-111">Hallo volgende afbeelding toont Hallo activiteitenlogboek voor een abonnement.</span><span class="sxs-lookup"><span data-stu-id="8f6df-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="8f6df-112">Hiermee geeft u twee implementaties.</span><span class="sxs-lookup"><span data-stu-id="8f6df-112">It represents two deployments.</span></span> <span data-ttu-id="8f6df-113">In een implementatie Hallo sjabloon validatie is mislukt (**valideren**) en niet worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="8f6df-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="8f6df-114">Hallo in andere implementatie, Hallo sjabloon gevalideerd, maar is mislukt bij het maken van Hallo resources (**schrijven implementaties**).</span><span class="sxs-lookup"><span data-stu-id="8f6df-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![foutcode weergeven](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="8f6df-116">Validatiefouten worden veroorzaakt door scenario's die vóór de implementatie kunnen worden bepaald.</span><span class="sxs-lookup"><span data-stu-id="8f6df-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="8f6df-117">Ze bevatten syntaxisfouten in de sjabloon of tijdens toodeploy resources die uw abonnement quota's zou overschrijden.</span><span class="sxs-lookup"><span data-stu-id="8f6df-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="8f6df-118">Implementatiefouten worden veroorzaakt door de voorwaarden die tijdens het implementatieproces Hallo optreden.</span><span class="sxs-lookup"><span data-stu-id="8f6df-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="8f6df-119">Ze bevatten tooaccess probeert een resource die parallel wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8f6df-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="8f6df-120">Beide soorten fouten retourneren een foutcode tootroubleshoot Hallo implementatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8f6df-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="8f6df-121">Beide soorten fouten worden weergegeven in Hallo [activiteitenlogboek](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="8f6df-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="8f6df-122">Validatiefouten worden echter niet weergegeven in de geschiedenis van uw implementatie omdat Hallo implementatie nooit gestart.</span><span class="sxs-lookup"><span data-stu-id="8f6df-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="8f6df-123">Foutcode bepalen</span><span class="sxs-lookup"><span data-stu-id="8f6df-123">Determine error code</span></span>

<span data-ttu-id="8f6df-124">U kunt meer informatie over een fout door te kijken fout het Hallo-bericht en Hallo-foutcode.</span><span class="sxs-lookup"><span data-stu-id="8f6df-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="8f6df-125">Hallo [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md) artikel geeft oplossingen-foutcode.</span><span class="sxs-lookup"><span data-stu-id="8f6df-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="8f6df-126">Dit onderwerp leest hoe toouse hello Azure portal toodiscover Hallo-foutcode.</span><span class="sxs-lookup"><span data-stu-id="8f6df-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="8f6df-127">Validatiefouten</span><span class="sxs-lookup"><span data-stu-id="8f6df-127">Validation errors</span></span>

<span data-ttu-id="8f6df-128">Bij het implementeren via de portal hello, ziet u een validatiefout opgetreden na het verzenden van uw waarden.</span><span class="sxs-lookup"><span data-stu-id="8f6df-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![Fout bij de portal validatie weergeven](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="8f6df-130">Selecteer het Hallo-bericht voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8f6df-130">Select hello message for more details.</span></span> <span data-ttu-id="8f6df-131">In Hallo installatiekopie te volgen, ziet u een **InvalidTemplateDeployment** fout en een bericht verschijnt dat een beleid voor implementatie wordt geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="8f6df-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![validatie details weergeven](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="8f6df-133">Implementatiefouten</span><span class="sxs-lookup"><span data-stu-id="8f6df-133">Deployment errors</span></span>

<span data-ttu-id="8f6df-134">Als het Hallo-bewerking is geslaagd, maar niet tijdens de implementatie, ziet u Hallo-fout bij het Hallo-meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="8f6df-135">Selecteer Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="8f6df-135">Select hello notification.</span></span>

![Fout bij wijzigingsbericht](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="8f6df-137">Ziet u meer informatie over het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8f6df-137">You see more details about hello deployment.</span></span> <span data-ttu-id="8f6df-138">Selecteer Hallo optie toofind meer informatie over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="8f6df-138">Select hello option toofind more information about hello error.</span></span>

![implementatie is mislukt](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="8f6df-140">Ziet u Hallo-bericht en de fout-foutcodes.</span><span class="sxs-lookup"><span data-stu-id="8f6df-140">You see hello error message and error codes.</span></span> <span data-ttu-id="8f6df-141">Er zijn twee foutcodes.</span><span class="sxs-lookup"><span data-stu-id="8f6df-141">Notice there are two error codes.</span></span> <span data-ttu-id="8f6df-142">eerste foutcode Hallo (**implementatie mislukt**) is een algemene fout die biedt geen Hallo details u moet toosolve Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="8f6df-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="8f6df-143">tweede foutcode Hallo (**StorageAccountNotFound**) biedt Hallo informatie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![Details van fouten](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="8f6df-145">Inschakelen van logboekregistratie voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="8f6df-145">Enable debug logging</span></span>
<span data-ttu-id="8f6df-146">Soms moet u meer informatie over het Hallo-aanvraag en -antwoord toodiscover wat er mis ging.</span><span class="sxs-lookup"><span data-stu-id="8f6df-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="8f6df-147">U kunt met behulp van PowerShell of Azure CLI aanvragen dat aanvullende informatie wordt geregistreerd tijdens een implementatie.</span><span class="sxs-lookup"><span data-stu-id="8f6df-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="8f6df-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8f6df-148">PowerShell</span></span>

   <span data-ttu-id="8f6df-149">In PowerShell instellen Hallo **DeploymentDebugLogLevel** parameter tooAll, ResponseContent of RequestContent.</span><span class="sxs-lookup"><span data-stu-id="8f6df-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="8f6df-150">Bekijk Hallo aanvraaginhoud Hello volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="8f6df-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="8f6df-151">Of Hallo antwoord inhoud met:</span><span class="sxs-lookup"><span data-stu-id="8f6df-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="8f6df-152">Deze informatie kunt u bepalen of een waarde in de sjabloon Hallo onjuist wordt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8f6df-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="8f6df-153">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8f6df-153">Azure CLI</span></span>

   <span data-ttu-id="8f6df-154">Controleer Hallo implementatiebewerkingen Hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8f6df-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="8f6df-155">Geneste sjabloon</span><span class="sxs-lookup"><span data-stu-id="8f6df-155">Nested template</span></span>

   <span data-ttu-id="8f6df-156">toolog foutopsporingsgegevens voor een geneste sjabloon gebruik Hallo **debugSetting** element.</span><span class="sxs-lookup"><span data-stu-id="8f6df-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

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


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="8f6df-157">Maken van een sjabloon voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="8f6df-157">Create a troubleshooting template</span></span>
<span data-ttu-id="8f6df-158">In sommige gevallen Hallo gemakkelijkste manier tootroubleshoot uw sjabloon is tootest onderdelen hiervan.</span><span class="sxs-lookup"><span data-stu-id="8f6df-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="8f6df-159">U kunt een vereenvoudigde sjabloon waarmee u toofocus maken op Hallo-onderdeel dat u van mening bent Hallo fout veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="8f6df-160">Stel bijvoorbeeld dat u ontvangt een fout opgetreden bij het verwijzen naar een resource.</span><span class="sxs-lookup"><span data-stu-id="8f6df-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="8f6df-161">In plaats van te moeten omgaan met een volledige sjabloon, een sjabloon die als resultaat geeft Hallo-onderdeel dat wordt veroorzaakt door het probleem te maken.</span><span class="sxs-lookup"><span data-stu-id="8f6df-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="8f6df-162">Dit kunt u bepalen of u aan de juiste parameters hello doorgeeft, met behulp van de sjabloonfuncties correct en Hallo bron ophalen die u verwacht.</span><span class="sxs-lookup"><span data-stu-id="8f6df-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

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

<span data-ttu-id="8f6df-163">Of stel fouten implementatie die u van mening bent zijn gerelateerd tooincorrectly afhankelijkheden instellen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="8f6df-164">Test uw sjabloon door in vereenvoudigde sjablonen op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="8f6df-165">Maak eerst een sjabloon die slechts één bron (zoals een SQL-Server) implementeert.</span><span class="sxs-lookup"><span data-stu-id="8f6df-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="8f6df-166">Als u zeker dat u die correct gedefinieerd resource hebt, kunt u een resource die afhankelijk zijn van deze (zoals een SQL-Database) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="8f6df-167">Wanneer u deze twee bronnen onjuist is gedefinieerd hebt, moet u andere afhankelijke resources (zoals controlebeleid) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="8f6df-168">Verwijder Hallo groep toomake zeker dat u voldoende testen Hallo bronafhankelijkheden tussen elke testimplementatie.</span><span class="sxs-lookup"><span data-stu-id="8f6df-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="8f6df-169">Controleer de volgorde van de implementatie</span><span class="sxs-lookup"><span data-stu-id="8f6df-169">Check deployment sequence</span></span>

<span data-ttu-id="8f6df-170">Veel implementatiefouten gebeuren wanneer een onverwachte reeks resources worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8f6df-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="8f6df-171">Deze fouten zich voordoen als afhankelijkheden niet correct zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="8f6df-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="8f6df-172">Wanneer er ontbreekt een vereiste afhankelijkheid, kunt u probeert een resource toouse een waarde op voor een andere bron, maar andere Hallo nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="8f6df-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="8f6df-173">U krijgt een foutmelding weergegeven dat een bron is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="8f6df-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="8f6df-174">U kunt dit type fout afwisselend tegenkomen, omdat de implementatietijd Hallo voor elke resource kan verschillen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="8f6df-175">Bijvoorbeeld de eerste poging toodeploy uw resources is gelukt, omdat een vereiste bron willekeurig tijdstip is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f6df-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="8f6df-176">De tweede poging mislukt echter omdat Hallo vereiste resource is niet op tijd voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f6df-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="8f6df-177">Maar u wilt dat tooavoid instelling afhankelijkheden die niet nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="8f6df-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="8f6df-178">Wanneer u onnodige afhankelijkheden hebt, wordt het Hallo-duur van Hallo implementatie verlengen door te voorkomen dat de bronnen die niet afhankelijk van elkaar worden geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="8f6df-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="8f6df-179">U kunt bovendien circulaire afhankelijkheden die Hallo implementatie blokkeren maken.</span><span class="sxs-lookup"><span data-stu-id="8f6df-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="8f6df-180">Hallo [verwijzing](resource-group-template-functions-resource.md#reference) functie maakt een impliciete afhankelijkheid voor de bron waarnaar wordt verwezen hello, als deze bron wordt geïmplementeerd op Hallo dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8f6df-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="8f6df-181">Daarom wellicht hebt u meer afhankelijkheden dan Hallo afhankelijkheden die zijn opgegeven in Hallo **dependsOn** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8f6df-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="8f6df-182">Hallo [resourceId](resource-group-template-functions-resource.md#resourceid) functie niet maken van een impliciete afhankelijkheid of valideren dat Hallo resource bestaat.</span><span class="sxs-lookup"><span data-stu-id="8f6df-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="8f6df-183">Wanneer u afhankelijkheid problemen ondervindt, moet u toogain inzicht in de Hallo volgorde van de resource-implementatie.</span><span class="sxs-lookup"><span data-stu-id="8f6df-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="8f6df-184">tooview hello bewerkingsvolgorde implementatie:</span><span class="sxs-lookup"><span data-stu-id="8f6df-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="8f6df-185">Selecteer de implementatiegeschiedenis Hallo voor de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="8f6df-185">Select hello deployment history for your resource group.</span></span>

   ![Geschiedenis van implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="8f6df-187">Selecteer een implementatie van Hallo geschiedenis en selecteer **gebeurtenissen**.</span><span class="sxs-lookup"><span data-stu-id="8f6df-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![gebeurtenissen van de implementatie selecteren](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="8f6df-189">Bekijk Hallo reeks gebeurtenissen voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="8f6df-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="8f6df-190">Betalen aandacht toohello status van elke bewerking.</span><span class="sxs-lookup"><span data-stu-id="8f6df-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="8f6df-191">Hallo ziet volgende afbeelding u bijvoorbeeld drie storage-accounts die geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="8f6df-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="8f6df-192">U ziet dat Hallo drie storage-accounts zijn gestart op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8f6df-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![Parallelle implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="8f6df-194">Hallo volgende afbeelding ziet u drie opslagaccounts die niet zijn geïmplementeerd parallel.</span><span class="sxs-lookup"><span data-stu-id="8f6df-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="8f6df-195">Hallo tweede storage-account is afhankelijk van Hallo eerste storage-account en Hallo derde storage-account is afhankelijk van Hallo tweede storage-account.</span><span class="sxs-lookup"><span data-stu-id="8f6df-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="8f6df-196">Daarom wordt Hallo eerste storage-account gestart, geaccepteerd en voltooid voordat de volgende Hallo is gestart.</span><span class="sxs-lookup"><span data-stu-id="8f6df-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![sequentiële implementatie](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="8f6df-198">Zelfs voor een meer complexe scenario's, kunt u dezelfde techniek toodiscover Hallo toen deze implementatie is gestart en voltooid voor elke resource.</span><span class="sxs-lookup"><span data-stu-id="8f6df-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="8f6df-199">Bekijk uw implementatie gebeurtenissen toosee als Hallo sequence anders is dan u verwacht.</span><span class="sxs-lookup"><span data-stu-id="8f6df-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="8f6df-200">Zo ja, herzie Hallo afhankelijkheden voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="8f6df-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="8f6df-201">Resource Manager identificeert circulaire afhankelijkheden tijdens de validatie van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="8f6df-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="8f6df-202">Retourneert een foutbericht weergegeven waarin wordt vermeld specifiek een circulaire afhankelijkheid bestaat.</span><span class="sxs-lookup"><span data-stu-id="8f6df-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="8f6df-203">toosolve een circulaire afhankelijkheid:</span><span class="sxs-lookup"><span data-stu-id="8f6df-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="8f6df-204">In de sjabloon vinden Hallo resource in Hallo circulaire afhankelijkheid geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="8f6df-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="8f6df-205">Voor die bron onderzoeken Hallo **dependsOn** eigenschap en elk gebruik van Hallo **verwijzing** toosee welke resources afhankelijk van is werken.</span><span class="sxs-lookup"><span data-stu-id="8f6df-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="8f6df-206">Bekijk deze resources toosee welke bronnen ze afhankelijk zijn.</span><span class="sxs-lookup"><span data-stu-id="8f6df-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="8f6df-207">Volg Hallo afhankelijkheden totdat u een resource die afhankelijk van de oorspronkelijke bron Hallo is merkt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="8f6df-208">Voor Hallo bronnen die zijn betrokken bij Hallo circulaire afhankelijkheid zorgvuldig al gebruik van Hallo **dependsOn** eigenschap tooidentify eventuele afhankelijkheden die niet nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="8f6df-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="8f6df-209">Verwijder deze afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="8f6df-209">Remove those dependencies.</span></span> <span data-ttu-id="8f6df-210">Als u niet zeker weet dat er een afhankelijkheid is vereist, probeert u het verwijdert.</span><span class="sxs-lookup"><span data-stu-id="8f6df-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="8f6df-211">Hallo-sjabloon implementeren.</span><span class="sxs-lookup"><span data-stu-id="8f6df-211">Redeploy hello template.</span></span>

<span data-ttu-id="8f6df-212">Verwijderen van waarden uit Hallo **dependsOn** eigenschap kan fouten veroorzaken wanneer u Hallo sjabloon implementeert.</span><span class="sxs-lookup"><span data-stu-id="8f6df-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="8f6df-213">Als er een fout optreden, moet u de afhankelijkheid Hallo terug naar het Hallo-sjabloon toevoegen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="8f6df-214">Als deze aanpak Hallo circulaire afhankelijkheid niet wordt opgelost, kunt u deel uitmaakt van uw implementatie logica verplaatsen naar onderliggende resources (zoals extensies of configuratie-instellingen).</span><span class="sxs-lookup"><span data-stu-id="8f6df-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="8f6df-215">Deze onderliggende resources toodeploy na Hallo resources van Hallo circulaire afhankelijkheid configureren.</span><span class="sxs-lookup"><span data-stu-id="8f6df-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="8f6df-216">Stel bijvoorbeeld dat u twee virtuele machines implementeert, maar u moet eigenschappen instellen voor elk veld dat toohello andere verwijzen.</span><span class="sxs-lookup"><span data-stu-id="8f6df-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="8f6df-217">U kunt deze implementeren in Hallo volgorde:</span><span class="sxs-lookup"><span data-stu-id="8f6df-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="8f6df-218">vm1</span><span class="sxs-lookup"><span data-stu-id="8f6df-218">vm1</span></span>
2. <span data-ttu-id="8f6df-219">vm2</span><span class="sxs-lookup"><span data-stu-id="8f6df-219">vm2</span></span>
3. <span data-ttu-id="8f6df-220">Extensie op vm1, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="8f6df-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="8f6df-221">Hallo-extensie waarden ingesteld op vm1 die van vm2 krijgt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="8f6df-222">Extensie op vm2, is afhankelijk van vm1 en vm2.</span><span class="sxs-lookup"><span data-stu-id="8f6df-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="8f6df-223">Hallo-extensie waarden ingesteld op vm2 van van vm1 krijgt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="8f6df-224">Hallo dezelfde methode voor App Service-apps werkt.</span><span class="sxs-lookup"><span data-stu-id="8f6df-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="8f6df-225">Overweeg configuratiewaarden verplaatsen naar een onderliggende resource van resource Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="8f6df-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="8f6df-226">U kunt twee web-apps in Hallo volgorde kunt implementeren:</span><span class="sxs-lookup"><span data-stu-id="8f6df-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="8f6df-227">webapp1</span><span class="sxs-lookup"><span data-stu-id="8f6df-227">webapp1</span></span>
2. <span data-ttu-id="8f6df-228">webapp2</span><span class="sxs-lookup"><span data-stu-id="8f6df-228">webapp2</span></span>
3. <span data-ttu-id="8f6df-229">configuratie voor webapp1, is afhankelijk van webapp1 en webapp2.</span><span class="sxs-lookup"><span data-stu-id="8f6df-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="8f6df-230">Het bevat app-instellingen met waarden uit webapp2.</span><span class="sxs-lookup"><span data-stu-id="8f6df-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="8f6df-231">configuratie voor webapp2, is afhankelijk van webapp1 en webapp2.</span><span class="sxs-lookup"><span data-stu-id="8f6df-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="8f6df-232">Het bevat app-instellingen met waarden uit webapp1.</span><span class="sxs-lookup"><span data-stu-id="8f6df-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8f6df-233">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f6df-233">Next steps</span></span>
* <span data-ttu-id="8f6df-234">Zie voor oplossingen toocommon implementatiefouten, [oplossen van veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="8f6df-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="8f6df-235">toolearn over het controleren van acties, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="8f6df-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="8f6df-236">Zie toolearn over acties toodetermine Hallo fouten tijdens de implementatie van [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="8f6df-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
