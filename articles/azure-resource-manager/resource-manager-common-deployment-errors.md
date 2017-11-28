---
title: Veelvoorkomende fouten van de Azure-implementatie oplossen | Microsoft Docs
description: Beschrijft hoe u veelvoorkomende fouten oplossen wanneer u resources in Azure met Azure Resource Manager implementeert.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren in azure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="7f612-104">Veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager oplossen</span><span class="sxs-lookup"><span data-stu-id="7f612-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="7f612-105">Dit onderwerp wordt beschreven hoe u een aantal gemeenschappelijke kunt oplossen Azure-implementatiefouten kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="7f612-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="7f612-106">De volgende foutcodes worden beschreven in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="7f612-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="7f612-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="7f612-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="7f612-108">Verificatie mislukt</span><span class="sxs-lookup"><span data-stu-id="7f612-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="7f612-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="7f612-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="7f612-110">Implementatie mislukt</span><span class="sxs-lookup"><span data-stu-id="7f612-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="7f612-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="7f612-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="7f612-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="7f612-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="7f612-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="7f612-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="7f612-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="7f612-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="7f612-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="7f612-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="7f612-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="7f612-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="7f612-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="7f612-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="7f612-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="7f612-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="7f612-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="7f612-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="7f612-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="7f612-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="7f612-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="7f612-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="7f612-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="7f612-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="7f612-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="7f612-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="7f612-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="7f612-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="7f612-125">Implementatie mislukt</span><span class="sxs-lookup"><span data-stu-id="7f612-125">DeploymentFailed</span></span>

<span data-ttu-id="7f612-126">Deze foutcode geeft een algemene implementatiefout, maar het is niet de foutcode die u wilt beginnen met het oplossen.</span><span class="sxs-lookup"><span data-stu-id="7f612-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="7f612-127">De foutcode die daadwerkelijk helpt u los het probleem is meestal één niveau onder deze fout.</span><span class="sxs-lookup"><span data-stu-id="7f612-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="7f612-128">Bijvoorbeeld de volgende afbeelding toont de **RequestDisallowedByPolicy** foutcode die zich in de implementatiefout.</span><span class="sxs-lookup"><span data-stu-id="7f612-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![foutcode weergeven](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="7f612-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="7f612-130">SkuNotAvailable</span></span>

<span data-ttu-id="7f612-131">Bij het implementeren van een resource (meestal een virtuele machine), wordt de volgende foutcode en een foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7f612-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="7f612-132">U ontvangt deze foutmelding wanneer de SKU die u hebt geselecteerd (zoals VM-grootte) van de resource is niet beschikbaar voor de locatie die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="7f612-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="7f612-133">U lost dit probleem, moet u bepalen welke SKU's zijn beschikbaar in een regio.</span><span class="sxs-lookup"><span data-stu-id="7f612-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="7f612-134">U kunt PowerShell, de portal of REST-bewerking gebruiken om te zoeken naar beschikbare SKU's.</span><span class="sxs-lookup"><span data-stu-id="7f612-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="7f612-135">Gebruik voor PowerShell [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) en filteren op locatie.</span><span class="sxs-lookup"><span data-stu-id="7f612-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="7f612-136">U kunt de nieuwste versie van PowerShell voor deze opdracht moet hebben.</span><span class="sxs-lookup"><span data-stu-id="7f612-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="7f612-137">De resultaten bevatten een lijst van SKU's voor de locatie en beperkingen voor deze SKU.</span><span class="sxs-lookup"><span data-stu-id="7f612-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="7f612-138">Gebruik de [portal](https://portal.azure.com), aanmelden bij de portal en toevoegen van een bron via de interface.</span><span class="sxs-lookup"><span data-stu-id="7f612-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="7f612-139">Als u de waarden instelt, ziet u de beschikbare SKU's voor die bron.</span><span class="sxs-lookup"><span data-stu-id="7f612-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="7f612-140">U hoeft niet om de implementatie te vervolledigen.</span><span class="sxs-lookup"><span data-stu-id="7f612-140">You do not need to complete the deployment.</span></span>

    ![beschikbare SKU 's](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="7f612-142">Voor het gebruik van de REST-API voor virtuele machines, moet u de volgende aanvraag verzenden:</span><span class="sxs-lookup"><span data-stu-id="7f612-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="7f612-143">Deze retourneert beschikbare SKU's en regio's in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="7f612-143">It returns available SKUs and regions in the following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="7f612-144">Als u niet een geschikte SKU gevonden in deze regio of een alternatieve regio die voldoet aan uw bedrijf moet, dienen een [SKU aanvraag](https://aka.ms/skurestriction) voor ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="7f612-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="7f612-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="7f612-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="7f612-146">Als deze fout wordt weergegeven, gebruikt u een abonnement dat is niet toegestaan voor toegang tot alle Azure-services dan Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f612-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="7f612-147">Dit type abonnement wellicht op wanneer u moet toegang hebben tot de klassieke portal, maar zijn niet toegestaan voor het implementeren van resources.</span><span class="sxs-lookup"><span data-stu-id="7f612-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="7f612-148">U lost dit probleem, moet u een abonnement dat gemachtigd is om resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="7f612-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="7f612-149">Als u wilt weergeven van de beschikbare abonnementen met PowerShell, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="7f612-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="7f612-150">En u kunt het huidige abonnement instellen met:</span><span class="sxs-lookup"><span data-stu-id="7f612-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="7f612-151">Als u wilt weergeven van de beschikbare abonnementen met Azure CLI 2.0, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7f612-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="7f612-152">En u kunt het huidige abonnement instellen met:</span><span class="sxs-lookup"><span data-stu-id="7f612-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="7f612-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="7f612-153">InvalidTemplate</span></span>
<span data-ttu-id="7f612-154">Deze fout kan leiden tot verschillende typen fouten.</span><span class="sxs-lookup"><span data-stu-id="7f612-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="7f612-155">Syntaxisfout</span><span class="sxs-lookup"><span data-stu-id="7f612-155">Syntax error</span></span>

   <span data-ttu-id="7f612-156">Als u een foutbericht dat aangeeft de validatie van de sjabloon is mislukt ontvangt dat, hebt u mogelijk een probleem met de syntaxis in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7f612-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="7f612-157">Dit is een fout gemakkelijk maken omdat sjabloonexpressies kunnen ingewikkeld zijn.</span><span class="sxs-lookup"><span data-stu-id="7f612-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="7f612-158">De naamtoewijzing van de volgende voor een opslagaccount bevat bijvoorbeeld een reeks vierkante haken, drie functies drie sets van haakjes, één set met enkele aanhalingstekens en één eigenschap:</span><span class="sxs-lookup"><span data-stu-id="7f612-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="7f612-159">Als u de syntaxis van de overeenkomende niet opgeeft, wordt in de sjabloon een waarde die is anders dan uw bedoeling produceert.</span><span class="sxs-lookup"><span data-stu-id="7f612-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="7f612-160">Wanneer u dit type fout ontvangt, zorgvuldig door de expressiesyntaxis van de.</span><span class="sxs-lookup"><span data-stu-id="7f612-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="7f612-161">Overweeg het gebruik van een JSON-editor, zoals [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) of [Visual Studio Code](resource-manager-vs-code.md), die u kunt gewaarschuwd over syntaxisfouten.</span><span class="sxs-lookup"><span data-stu-id="7f612-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="7f612-162">Onjuiste segment lengten</span><span class="sxs-lookup"><span data-stu-id="7f612-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="7f612-163">Een andere ongeldige sjabloon-fout treedt op wanneer de resourcenaam niet de juiste indeling is.</span><span class="sxs-lookup"><span data-stu-id="7f612-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="7f612-164">Een bron voor het niveau van hoofdmap moet één minder segment hebben van de naam dan in het brontype.</span><span class="sxs-lookup"><span data-stu-id="7f612-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="7f612-165">Elk segment wordt onderscheiden door een slash.</span><span class="sxs-lookup"><span data-stu-id="7f612-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="7f612-166">In het volgende voorbeeld wordt het type heeft twee segmenten en de naam van de één segment dus is het een **geldige naam**.</span><span class="sxs-lookup"><span data-stu-id="7f612-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="7f612-167">Maar het volgende voorbeeld is **niet de naam van een geldige** omdat er hetzelfde aantal segmenten als het type.</span><span class="sxs-lookup"><span data-stu-id="7f612-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="7f612-168">Hebben hetzelfde aantal segmenten voor onderliggende resources, het type en de naam.</span><span class="sxs-lookup"><span data-stu-id="7f612-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="7f612-169">Dit aantal segmenten zin omdat de volledige naam en type voor het onderliggende element bevat de naam van het bovenliggende en het type.</span><span class="sxs-lookup"><span data-stu-id="7f612-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="7f612-170">Daarom heeft de volledige naam nog steeds één minder segment dan het volledige type.</span><span class="sxs-lookup"><span data-stu-id="7f612-170">Therefore, the full name still has one less segment than the full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="7f612-171">Ophalen van de segmenten rechts is lastig met Resource Manager-typen die worden toegepast op de resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="7f612-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="7f612-172">Bijvoorbeeld, een resource-vergrendeling wordt toegepast op een website, is een type met vier segmenten vereist.</span><span class="sxs-lookup"><span data-stu-id="7f612-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="7f612-173">Daarom is de naam van de drie segmenten:</span><span class="sxs-lookup"><span data-stu-id="7f612-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="7f612-174">Index van de kopie wordt niet verwacht.</span><span class="sxs-lookup"><span data-stu-id="7f612-174">Copy index is not expected</span></span>

   <span data-ttu-id="7f612-175">U tegenkomt dit **InvalidTemplate** fout wanneer u hebt toegepast de **kopie** element een deel van de sjabloon die geen ondersteuning biedt voor dit element.</span><span class="sxs-lookup"><span data-stu-id="7f612-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="7f612-176">U kunt het element kopiëren alleen toepassen op een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="7f612-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="7f612-177">U kunt kopiëren niet toepassen op een eigenschap binnen een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="7f612-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="7f612-178">Bijvoorbeeld, u kopie toepassen op een virtuele machine, maar u kunt deze toepassen op de OS-schijven voor een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7f612-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="7f612-179">In sommige gevallen kunt u een onderliggende resource niet converteren naar een bovenliggende resource voor het maken van een kopie-lus.</span><span class="sxs-lookup"><span data-stu-id="7f612-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="7f612-180">Zie voor meer informatie over het gebruik van kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="7f612-181">Parameter is niet geldig</span><span class="sxs-lookup"><span data-stu-id="7f612-181">Parameter is not valid</span></span>

   <span data-ttu-id="7f612-182">Als de sjabloon toegestane waarden voor een parameter worden, en u een waarde die niet een van deze waarden opgeven, ontvangt u een bericht dat lijkt op de volgende fout:</span><span class="sxs-lookup"><span data-stu-id="7f612-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="7f612-183">Dubbele de toegestane waarden in de sjabloon en geef een tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="7f612-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="7f612-184">Kringafhankelijkheid gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="7f612-184">Circular dependency detected</span></span>

   <span data-ttu-id="7f612-185">U ontvangt deze foutmelding wanneer resources afhankelijk van elkaar op een manier waardoor de implementatie zijn niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="7f612-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="7f612-186">Een combinatie van afhankelijkheden maakt twee of meer resources, wacht u totdat de andere bronnen die ook wachten.</span><span class="sxs-lookup"><span data-stu-id="7f612-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="7f612-187">Bijvoorbeeld resource1 is afhankelijk van resource3, resource2, is afhankelijk van resource1 en resource3 is afhankelijk van resource2.</span><span class="sxs-lookup"><span data-stu-id="7f612-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="7f612-188">Meestal kunt u dit probleem oplossen door het verwijderen van onnodige afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="7f612-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="7f612-189">NotFound en ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="7f612-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="7f612-190">Wanneer de sjabloon de naam van een resource die niet kan worden omgezet bevat, wordt een foutbericht zoals:</span><span class="sxs-lookup"><span data-stu-id="7f612-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="7f612-191">Als u probeert de ontbrekende resource in de sjabloon te implementeren, controleert u of u moet een afhankelijkheid toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7f612-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="7f612-192">Resource Manager optimaliseert implementatie door het maken van resources parallel indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="7f612-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="7f612-193">Als een resource moet worden geïmplementeerd nadat een andere resource, moet u de **dependsOn** element in de sjabloon voor het maken van een afhankelijkheid op de andere resource.</span><span class="sxs-lookup"><span data-stu-id="7f612-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="7f612-194">Bijvoorbeeld, wanneer u een web-app implementeert, moet de App Service-abonnement bestaan.</span><span class="sxs-lookup"><span data-stu-id="7f612-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="7f612-195">Als de web-app is afhankelijk van de App Service-abonnement is niet opgegeven, wordt met Resource Manager beide resources maakt op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="7f612-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="7f612-196">U ontvangt een foutmelding weergegeven dat de resource voor de App Service-abonnement kan niet worden gevonden, omdat deze niet bestaat nog bij een poging tot een eigenschap instellen voor de web-app.</span><span class="sxs-lookup"><span data-stu-id="7f612-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="7f612-197">U kunt deze fout voorkomen door het instellen van de afhankelijkheid in de web-app.</span><span class="sxs-lookup"><span data-stu-id="7f612-197">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="7f612-198">Zie voor suggesties over het oplossen van afhankelijkheidsfouten [volgorde van de implementatie controleren](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="7f612-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="7f612-199">Deze fout wordt ook zien wanneer de bron bestaat in een andere resourcegroep dan de versie die wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7f612-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="7f612-200">In dat geval gebruiken de [resourceId functie](resource-group-template-functions-resource.md#resourceid) ophalen van de volledig gekwalificeerde naam van de resource.</span><span class="sxs-lookup"><span data-stu-id="7f612-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="7f612-201">Als u probeert te gebruiken de [verwijzing](resource-group-template-functions-resource.md#reference) of [listKeys](resource-group-template-functions-resource.md#listkeys) werkt in combinatie met een resource die niet kunnen worden omgezet, het volgende foutbericht:</span><span class="sxs-lookup"><span data-stu-id="7f612-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="7f612-202">Zoek naar een expressie met de **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="7f612-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="7f612-203">Controleer of de parameterwaarden juist zijn.</span><span class="sxs-lookup"><span data-stu-id="7f612-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="7f612-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="7f612-204">ParentResourceNotFound</span></span>

<span data-ttu-id="7f612-205">Wanneer een bron een bovenliggend item naar een andere bron is, moet de bovenliggende resource bestaan voordat u de onderliggende resource maakt.</span><span class="sxs-lookup"><span data-stu-id="7f612-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="7f612-206">Als deze nog niet bestaat, wordt het volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7f612-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="7f612-207">De naam van de onderliggende resource bevat de naam van de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="7f612-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="7f612-208">Bijvoorbeeld, kunnen een SQL-Database worden gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="7f612-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="7f612-209">Maar als u een afhankelijkheid op de bovenliggende resource niet opgeeft, de onderliggende resource kan ophalen geïmplementeerd voordat u de bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="7f612-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="7f612-210">U lost deze fout, bevatten een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="7f612-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="7f612-211">StorageAccountAlreadyExists en StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="7f612-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="7f612-212">U moet een naam voor de resource die uniek is voor alle Azure opgeven voor de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="7f612-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="7f612-213">Als u niet een unieke naam opgeeft, wordt een fout als volgt:</span><span class="sxs-lookup"><span data-stu-id="7f612-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="7f612-214">U kunt een unieke naam maken door het samenvoegen van de naamconventie met het resultaat van de [uniqueString](resource-group-template-functions-string.md#uniquestring) functie.</span><span class="sxs-lookup"><span data-stu-id="7f612-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="7f612-215">Als u een opslagaccount met dezelfde naam als een bestaand opslagaccount in uw abonnement implementeren, maar een andere locatie opgeven, ontvangt u een foutbericht retourneren over dat de storage-account bestaat al in een andere locatie.</span><span class="sxs-lookup"><span data-stu-id="7f612-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="7f612-216">Verwijder de bestaande opslagaccount of geef dezelfde locatie als het bestaande opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7f612-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="7f612-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="7f612-217">AccountNameInvalid</span></span>
<span data-ttu-id="7f612-218">U ziet de **AccountNameInvalid** fout bij poging een storage-account een naam te geven met tekens verboden.</span><span class="sxs-lookup"><span data-stu-id="7f612-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="7f612-219">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7f612-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="7f612-220">De [uniqueString](resource-group-template-functions-string.md#uniquestring) functie retourneert 13 tekens.</span><span class="sxs-lookup"><span data-stu-id="7f612-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="7f612-221">Als het samenvoegen van een voorvoegsel van de **uniqueString** leiden, geeft u een voorvoegsel 11 tekens of minder.</span><span class="sxs-lookup"><span data-stu-id="7f612-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="7f612-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="7f612-222">BadRequest</span></span>

<span data-ttu-id="7f612-223">De status van een BadRequest kunnen optreden wanneer u een ongeldige waarde voor een eigenschap opgeeft.</span><span class="sxs-lookup"><span data-stu-id="7f612-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="7f612-224">Bijvoorbeeld, als u een onjuiste waarde voor de SKU voor een opslagaccount opgeeft, mislukt de implementatie.</span><span class="sxs-lookup"><span data-stu-id="7f612-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="7f612-225">Kijken om te bepalen van geldige waarden voor de eigenschap, de [REST-API](/rest/api) voor het brontype dat u implementeert.</span><span class="sxs-lookup"><span data-stu-id="7f612-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="7f612-226">NoRegisteredProviderFound en MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="7f612-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="7f612-227">Bij het implementeren van de resource wordt de volgende foutcode en het bericht:</span><span class="sxs-lookup"><span data-stu-id="7f612-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="7f612-228">Of een vergelijkbaar bericht waarin wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="7f612-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="7f612-229">U ontvangt deze fouten voor een van drie redenen:</span><span class="sxs-lookup"><span data-stu-id="7f612-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="7f612-230">De resourceprovider is niet geregistreerd voor uw abonnement</span><span class="sxs-lookup"><span data-stu-id="7f612-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="7f612-231">API-versie niet ondersteund voor het brontype</span><span class="sxs-lookup"><span data-stu-id="7f612-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="7f612-232">Locatie niet ondersteund voor het brontype</span><span class="sxs-lookup"><span data-stu-id="7f612-232">Location not supported for the resource type</span></span>

<span data-ttu-id="7f612-233">Het foutbericht geeft suggesties voor de ondersteunde locaties en API-versies.</span><span class="sxs-lookup"><span data-stu-id="7f612-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="7f612-234">U kunt uw sjabloon wijzigen in een van de voorgestelde waarden.</span><span class="sxs-lookup"><span data-stu-id="7f612-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="7f612-235">De meeste providers zijn geregistreerde automatisch door de Azure-portal of de opdrachtregelinterface die u gebruikt, maar niet alle.</span><span class="sxs-lookup"><span data-stu-id="7f612-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="7f612-236">Als u niet een bepaalde bron-provider voorafgaand aan hebt gebruikt, moet u wellicht dat de provider te registreren.</span><span class="sxs-lookup"><span data-stu-id="7f612-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="7f612-237">U kunt meer informatie over resourceproviders via PowerShell of Azure CLI detecteren.</span><span class="sxs-lookup"><span data-stu-id="7f612-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="7f612-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="7f612-238">**Portal**</span></span>

<span data-ttu-id="7f612-239">U kunt de registratiestatus zien en de naamruimte via de portal een resourceprovider registreren.</span><span class="sxs-lookup"><span data-stu-id="7f612-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="7f612-240">Selecteer voor uw abonnement, **resourceproviders**.</span><span class="sxs-lookup"><span data-stu-id="7f612-240">For your subscription, select **Resource providers**.</span></span>

   ![resourceproviders selecteren](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="7f612-242">Bekijk de lijst met resourceproviders en selecteer indien nodig de **registreren** koppeling naar de registerbronprovider is van het type dat u probeert te implementeren.</span><span class="sxs-lookup"><span data-stu-id="7f612-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![resourceproviders vermelden](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="7f612-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="7f612-244">**PowerShell**</span></span>

<span data-ttu-id="7f612-245">Als de registratiestatus van uw wilt weergeven, gebruikt **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="7f612-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="7f612-246">Gebruik voor het registreren van een provider **registreren AzureRmResourceProvider** en geef de naam van de resourceprovider die u wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="7f612-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="7f612-247">Als u de ondersteunde locaties voor een bepaald type resource, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="7f612-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="7f612-248">Als u de ondersteunde API-versies voor een bepaald type resource, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="7f612-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="7f612-249">**Azure-CLI**</span><span class="sxs-lookup"><span data-stu-id="7f612-249">**Azure CLI**</span></span>

<span data-ttu-id="7f612-250">U kunt controleren of de provider is geregistreerd, gebruiken de `azure provider list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="7f612-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="7f612-251">Voor het registreren van een resourceprovider, gebruiken de `azure provider register` opdracht in en geef de *naamruimte* te registreren.</span><span class="sxs-lookup"><span data-stu-id="7f612-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="7f612-252">Overzicht van de ondersteunde locaties en API-versies voor een brontype gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7f612-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="7f612-253">QuotaExceeded en OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="7f612-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="7f612-254">Mogelijk hebt u problemen als implementatie groter is dan een quotum die kan per resourcegroep, abonnementen, accounts en andere bereiken worden.</span><span class="sxs-lookup"><span data-stu-id="7f612-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="7f612-255">Uw abonnement kan bijvoorbeeld worden geconfigureerd om te beperken het aantal kernen voor een regio.</span><span class="sxs-lookup"><span data-stu-id="7f612-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="7f612-256">Als u een virtuele machine met meer cores dan de toegestane hoeveelheid implementeren probeert, ontvangt u een foutmelding weergegeven dat het quotum is overschreden.</span><span class="sxs-lookup"><span data-stu-id="7f612-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="7f612-257">Zie voor informatie voltooid quotum [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="7f612-258">Als u wilt onderzoeken quota's voor uw abonnement voor kernen, kunt u de `azure vm list-usage` opdracht in de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7f612-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="7f612-259">Het volgende voorbeeld ziet u dat de kerngeheugenquotum voor een gratis proefaccount 4 is:</span><span class="sxs-lookup"><span data-stu-id="7f612-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="7f612-260">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7f612-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="7f612-261">Als u een sjabloon die meer dan vier kernen in de regio VS-West maakt implementeert, kunt u een implementatiefout dat lijkt op krijgen:</span><span class="sxs-lookup"><span data-stu-id="7f612-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="7f612-262">In PowerShell kunt u de **Get-AzureRmVMUsage** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7f612-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="7f612-263">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="7f612-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="7f612-264">In dergelijke gevallen moet u gaat u naar de portal en het bestand een probleem met ondersteuning voor het genereren van uw quotum voor de regio waarin u wilt implementeren.</span><span class="sxs-lookup"><span data-stu-id="7f612-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="7f612-265">Vergeet niet dat voor de resourcegroepen het quotum voor elke afzonderlijke regio, niet voor het hele abonnement.</span><span class="sxs-lookup"><span data-stu-id="7f612-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="7f612-266">Als u implementeren, 30 kernen in VS-West wilt, hebt u vragen om 30 Resource Manager kernen in VS-West.</span><span class="sxs-lookup"><span data-stu-id="7f612-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="7f612-267">Als u implementeren, 30 kernen in een van de regio's waartoe u toegang hebt wilt, vraagt u 30 Resource Manager kernen in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="7f612-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="7f612-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="7f612-268">InvalidContentLink</span></span>
<span data-ttu-id="7f612-269">Wanneer u ontvangt het foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="7f612-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="7f612-270">U hebt waarschijnlijk geprobeerd om te koppelen aan een geneste sjabloon die niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="7f612-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="7f612-271">Controleer de URI die u hebt opgegeven voor de geneste sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7f612-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="7f612-272">Als de sjabloon in een opslagaccount bestaat, zorg er dan voor dat de URI is toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="7f612-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="7f612-273">U moet mogelijk een SAS-token doorgeven.</span><span class="sxs-lookup"><span data-stu-id="7f612-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="7f612-274">Zie voor meer informatie [Gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="7f612-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="7f612-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="7f612-276">U ontvangt deze foutmelding wanneer uw abonnement bevat een bronbeleid een actie die u probeert uit te voeren tijdens de implementatie wordt verhinderd.</span><span class="sxs-lookup"><span data-stu-id="7f612-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="7f612-277">Zoek naar de beleids-id in het foutbericht.</span><span class="sxs-lookup"><span data-stu-id="7f612-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="7f612-278">In **PowerShell**, bieden die beleids-id als de **Id** parameter voor het ophalen van informatie over het beleid dat uw implementatie geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="7f612-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="7f612-279">In **Azure CLI**, geef de naam van de definitie voor:</span><span class="sxs-lookup"><span data-stu-id="7f612-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="7f612-280">Raadpleeg voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="7f612-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="7f612-281">RequestDisallowedByPolicy-fout</span><span class="sxs-lookup"><span data-stu-id="7f612-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="7f612-282">[Beleid gebruiken voor het beheren van resources en toegangsbeheer](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="7f612-283">Verificatie mislukt</span><span class="sxs-lookup"><span data-stu-id="7f612-283">Authorization failed</span></span>
<span data-ttu-id="7f612-284">Wordt een fout opgetreden tijdens de implementatie omdat het account of de service-principal het implementeren van de bronnen geen toegang heeft tot het uitvoeren van deze acties.</span><span class="sxs-lookup"><span data-stu-id="7f612-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="7f612-285">Azure Active Directory kunt u of uw beheerder om te bepalen welke identiteiten hebben toegang tot welke bronnen in grote mate van precisie.</span><span class="sxs-lookup"><span data-stu-id="7f612-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="7f612-286">Bijvoorbeeld, als uw account is toegewezen aan de rol Lezer, zich u niet om resources te maken.</span><span class="sxs-lookup"><span data-stu-id="7f612-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="7f612-287">In dat geval ziet u een foutmelding autorisatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="7f612-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="7f612-288">Zie voor meer informatie over op rollen gebaseerde toegangsbeheer [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="7f612-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f612-289">Next steps</span></span>
* <span data-ttu-id="7f612-290">Zie voor meer informatie over het controleren van acties, [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="7f612-291">Zie voor meer informatie over acties om de fouten tijdens de implementatie, [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="7f612-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
