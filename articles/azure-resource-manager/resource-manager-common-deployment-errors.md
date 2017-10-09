---
title: aaaTroubleshoot algemene Azure-implementatiefouten | Microsoft Docs
description: Hierin wordt beschreven hoe tooresolve veelvoorkomende fouten bij het implementeren van resources tooAzure met Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Fout in de implementatie, azure-implementatie implementeren tooazure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="a6b96-104">Veelvoorkomende fouten voor Azure-implementatie met Azure Resource Manager oplossen</span><span class="sxs-lookup"><span data-stu-id="a6b96-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="a6b96-105">Dit onderwerp wordt beschreven hoe u een aantal gemeenschappelijke kunt oplossen Azure-implementatiefouten kunnen optreden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="a6b96-106">Hallo volgende foutcodes worden beschreven in dit onderwerp:</span><span class="sxs-lookup"><span data-stu-id="a6b96-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="a6b96-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a6b96-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="a6b96-108">Verificatie mislukt</span><span class="sxs-lookup"><span data-stu-id="a6b96-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="a6b96-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a6b96-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="a6b96-110">Implementatie mislukt</span><span class="sxs-lookup"><span data-stu-id="a6b96-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="a6b96-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a6b96-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="a6b96-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a6b96-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="a6b96-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a6b96-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="a6b96-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a6b96-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a6b96-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="a6b96-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="a6b96-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a6b96-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="a6b96-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="a6b96-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="a6b96-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="a6b96-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a6b96-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="a6b96-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="a6b96-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a6b96-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="a6b96-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="a6b96-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="a6b96-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a6b96-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="a6b96-125">Implementatie mislukt</span><span class="sxs-lookup"><span data-stu-id="a6b96-125">DeploymentFailed</span></span>

<span data-ttu-id="a6b96-126">Deze foutcode geeft een algemene implementatiefout, maar is geen foutcode Hallo moet u toostart het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="a6b96-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="a6b96-127">Hallo-foutcode die u kunt Hallo probleem oplossen door daadwerkelijk helpt is meestal één niveau onder deze fout.</span><span class="sxs-lookup"><span data-stu-id="a6b96-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="a6b96-128">Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **RequestDisallowedByPolicy** foutcode die onder Hallo implementatiefout optreedt.</span><span class="sxs-lookup"><span data-stu-id="a6b96-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![foutcode weergeven](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="a6b96-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="a6b96-130">SkuNotAvailable</span></span>

<span data-ttu-id="a6b96-131">Bij het implementeren van een resource (meestal een virtuele machine), wordt het foutbericht Hallo foutbericht code en de fout te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6b96-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="a6b96-132">U ontvangt deze foutmelding wanneer Hallo resource SKU die u hebt geselecteerd (zoals VM-grootte) is niet beschikbaar voor Hallo locatie die u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a6b96-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="a6b96-133">tooresolve dit probleem, moet u toodetermine die SKU's beschikbaar in een regio zijn.</span><span class="sxs-lookup"><span data-stu-id="a6b96-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="a6b96-134">U kunt PowerShell, Hallo portal of een REST-bewerking toofind beschikbare SKU's.</span><span class="sxs-lookup"><span data-stu-id="a6b96-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="a6b96-135">Gebruik voor PowerShell [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) en filteren op locatie.</span><span class="sxs-lookup"><span data-stu-id="a6b96-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="a6b96-136">U kunt Hallo meest recente versie van PowerShell voor deze opdracht moet hebben.</span><span class="sxs-lookup"><span data-stu-id="a6b96-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="a6b96-137">Hallo resultaten bevatten een lijst van SKU's voor de locatie van Hallo en eventuele beperkingen voor deze SKU.</span><span class="sxs-lookup"><span data-stu-id="a6b96-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="a6b96-138">Hallo toouse [portal](https://portal.azure.com), toohello portal aanmelden en toevoegen van een resource via Hallo-interface.</span><span class="sxs-lookup"><span data-stu-id="a6b96-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="a6b96-139">Als u Hallo waarden instelt, ziet u Hallo beschikbare SKU's voor die bron.</span><span class="sxs-lookup"><span data-stu-id="a6b96-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="a6b96-140">U hoeft niet toocomplete Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="a6b96-140">You do not need toocomplete hello deployment.</span></span>

    ![beschikbare SKU 's](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="a6b96-142">toouse hello REST-API voor virtuele machines, Hallo na aanvraag verzenden:</span><span class="sxs-lookup"><span data-stu-id="a6b96-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="a6b96-143">Het resulteert beschikbare SKU's en regio's in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="a6b96-143">It returns available SKUs and regions in hello following format:</span></span>

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

<span data-ttu-id="a6b96-144">Als u toofind een geschikte SKU in deze regio of een alternatieve regio die voldoet aan de behoeften van uw bedrijf bent, dient u een [SKU aanvraag](https://aka.ms/skurestriction) tooAzure ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="a6b96-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="a6b96-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="a6b96-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="a6b96-146">Als deze fout wordt weergegeven, gebruikt u een abonnement dat is niet toegestaan tooaccess alle Azure-services dan Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a6b96-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="a6b96-147">Dit type abonnement wellicht op als u tooaccess Hallo klassieke portal moet maar zijn niet toegestaan voor toodeploy resources.</span><span class="sxs-lookup"><span data-stu-id="a6b96-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="a6b96-148">tooresolve dit probleem, moet u een abonnement dat machtiging toodeploy bronnen heeft.</span><span class="sxs-lookup"><span data-stu-id="a6b96-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="a6b96-149">tooview uw beschikbare abonnementen met PowerShell kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a6b96-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="a6b96-150">En tooset Hallo huidige abonnement, gebruik:</span><span class="sxs-lookup"><span data-stu-id="a6b96-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="a6b96-151">tooview uw beschikbare abonnementen met Azure CLI 2.0, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a6b96-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="a6b96-152">En tooset Hallo huidige abonnement, gebruik:</span><span class="sxs-lookup"><span data-stu-id="a6b96-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="a6b96-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="a6b96-153">InvalidTemplate</span></span>
<span data-ttu-id="a6b96-154">Deze fout kan leiden tot verschillende typen fouten.</span><span class="sxs-lookup"><span data-stu-id="a6b96-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="a6b96-155">Syntaxisfout</span><span class="sxs-lookup"><span data-stu-id="a6b96-155">Syntax error</span></span>

   <span data-ttu-id="a6b96-156">Als u een foutbericht dat aangeeft dat de validatie van Hallo-sjabloon is mislukt ontvangt, hebt u mogelijk een probleem met de syntaxis in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a6b96-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="a6b96-157">Dit is een fout eenvoudig toomake omdat sjabloonexpressies kunnen ingewikkeld zijn.</span><span class="sxs-lookup"><span data-stu-id="a6b96-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="a6b96-158">Hallo bevat naamtoewijzing van de volgende voor een opslagaccount bijvoorbeeld een reeks vierkante haken, drie functies drie sets van haakjes, één set met enkele aanhalingstekens en één eigenschap:</span><span class="sxs-lookup"><span data-stu-id="a6b96-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="a6b96-159">Als u geen overeenkomende Hallo-syntaxis, produceert Hallo sjabloon een waarde die anders is dan uw bedoeling is.</span><span class="sxs-lookup"><span data-stu-id="a6b96-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="a6b96-160">Wanneer u dit type fout ontvangt, moet u zorgvuldig Hallo-expressiesyntaxis controleren.</span><span class="sxs-lookup"><span data-stu-id="a6b96-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="a6b96-161">Overweeg het gebruik van een JSON-editor, zoals [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) of [Visual Studio Code](resource-manager-vs-code.md), die u kunt gewaarschuwd over syntaxisfouten.</span><span class="sxs-lookup"><span data-stu-id="a6b96-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="a6b96-162">Onjuiste segment lengten</span><span class="sxs-lookup"><span data-stu-id="a6b96-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="a6b96-163">Een andere ongeldige sjabloon-fout treedt op wanneer Hallo resourcenaam niet de juiste indeling Hallo is.</span><span class="sxs-lookup"><span data-stu-id="a6b96-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="a6b96-164">Een bron voor het niveau van hoofdmap moet één minder segment in Hallo naam heeft dan in brontype Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="a6b96-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="a6b96-165">Elk segment wordt onderscheiden door een slash.</span><span class="sxs-lookup"><span data-stu-id="a6b96-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="a6b96-166">In de Hallo voorbeeld te volgen, Hallo type twee segmenten Hallo heeft en één segment dus is het een **geldige naam**.</span><span class="sxs-lookup"><span data-stu-id="a6b96-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a6b96-167">Maar is het volgende voorbeeld Hallo **niet de naam van een geldige** omdat hieraan Hallo hetzelfde aantal segmenten als Hallo-type.</span><span class="sxs-lookup"><span data-stu-id="a6b96-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="a6b96-168">Voor onderliggende resources Hallo type en de naam Hallo hebben hetzelfde aantal segmenten.</span><span class="sxs-lookup"><span data-stu-id="a6b96-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="a6b96-169">Dit aantal segmenten zin omdat Hallo volledige naam en type op voor de onderliggende hello omvat Hallo bovenliggende naam en type.</span><span class="sxs-lookup"><span data-stu-id="a6b96-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="a6b96-170">Volledige naam Hallo heeft daarom nog steeds één minder segment dan volledige Hallo-type.</span><span class="sxs-lookup"><span data-stu-id="a6b96-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

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

   <span data-ttu-id="a6b96-171">Ophalen Hallo segmenten rechts is lastig met Resource Manager-typen die worden toegepast op de resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="a6b96-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="a6b96-172">Bijvoorbeeld, vereist een type met vier segmenten toepassen van de website van een resource vergrendeling tooa.</span><span class="sxs-lookup"><span data-stu-id="a6b96-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="a6b96-173">Daarom is de naam van de Hallo drie segmenten:</span><span class="sxs-lookup"><span data-stu-id="a6b96-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="a6b96-174">Index van de kopie wordt niet verwacht.</span><span class="sxs-lookup"><span data-stu-id="a6b96-174">Copy index is not expected</span></span>

   <span data-ttu-id="a6b96-175">U tegenkomt dit **InvalidTemplate** fout bij het toepassen van Hallo **kopie** element tooa deel van Hallo-sjabloon die geen ondersteuning biedt voor dit element.</span><span class="sxs-lookup"><span data-stu-id="a6b96-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="a6b96-176">U kunt alleen Hallo kopiëren tooa resource elementtype toepassen.</span><span class="sxs-lookup"><span data-stu-id="a6b96-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="a6b96-177">U kunt kopiëren tooa eigenschap binnen een brontype niet toepassen.</span><span class="sxs-lookup"><span data-stu-id="a6b96-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="a6b96-178">Bijvoorbeeld, u kopiëren tooa virtuele machine hebt toegepast, maar u toohello OS-schijven voor een virtuele machine niet toepassen.</span><span class="sxs-lookup"><span data-stu-id="a6b96-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="a6b96-179">In sommige gevallen kunt u een onderliggende resource tooa bovenliggende resource toocreate een lus exemplaar converteren.</span><span class="sxs-lookup"><span data-stu-id="a6b96-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="a6b96-180">Zie voor meer informatie over het gebruik van kopiëren [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="a6b96-181">Parameter is niet geldig</span><span class="sxs-lookup"><span data-stu-id="a6b96-181">Parameter is not valid</span></span>

   <span data-ttu-id="a6b96-182">Als het Hallo-sjabloon bevat de toegestane waarden voor een parameter, en u een waarde die niet een van deze waarden opgeven, ontvangt u een bericht vergelijkbaar toohello volgende fout:</span><span class="sxs-lookup"><span data-stu-id="a6b96-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="a6b96-183">Controleer Hallo toegestane waarden in de sjabloon Hallo en bieden een tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a6b96-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="a6b96-184">Kringafhankelijkheid gedetecteerd</span><span class="sxs-lookup"><span data-stu-id="a6b96-184">Circular dependency detected</span></span>

   <span data-ttu-id="a6b96-185">U ontvangt deze foutmelding wanneer resources afhankelijk van elkaar op een manier waardoor het Hallo-implementatie zijn niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="a6b96-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="a6b96-186">Een combinatie van afhankelijkheden maakt twee of meer resources, wacht u totdat de andere bronnen die ook wachten.</span><span class="sxs-lookup"><span data-stu-id="a6b96-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="a6b96-187">Bijvoorbeeld resource1 is afhankelijk van resource3, resource2, is afhankelijk van resource1 en resource3 is afhankelijk van resource2.</span><span class="sxs-lookup"><span data-stu-id="a6b96-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="a6b96-188">Meestal kunt u dit probleem oplossen door het verwijderen van onnodige afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="a6b96-189">NotFound en ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="a6b96-190">Wanneer de sjabloon Hallo-naam van een resource die niet kan worden omgezet bevat, wordt een foutbericht zoals:</span><span class="sxs-lookup"><span data-stu-id="a6b96-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="a6b96-191">Als u toodeploy Hallo resource in de sjabloon Hallo ontbreekt probeert, controleert u of u een afhankelijkheid tooadd moet.</span><span class="sxs-lookup"><span data-stu-id="a6b96-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="a6b96-192">Resource Manager optimaliseert implementatie door het maken van resources parallel indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="a6b96-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="a6b96-193">Als een resource moet worden geïmplementeerd nadat een andere resource, moet u toouse hello **dependsOn** -element in de sjabloon toocreate een afhankelijkheid van Hallo andere resource.</span><span class="sxs-lookup"><span data-stu-id="a6b96-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="a6b96-194">Bijvoorbeeld, wanneer u een web-app implementeert, moet Hallo App Service-abonnement bestaan.</span><span class="sxs-lookup"><span data-stu-id="a6b96-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="a6b96-195">Als u niet hebt opgegeven dat Hallo web-app, is afhankelijk van Hallo App Service-abonnement, Resource Manager beide resources maakt op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="a6b96-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="a6b96-196">U ontvangt een foutmelding weergegeven dat Hallo App Service plan bron kan niet worden gevonden, omdat deze niet bestaat nog tijdens een poging de tooset een eigenschap op Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="a6b96-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="a6b96-197">U kunt deze fout voorkomen door in te stellen Hallo afhankelijkheid in Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="a6b96-197">You prevent this error by setting hello dependency in hello web app.</span></span>

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

<span data-ttu-id="a6b96-198">Zie voor suggesties over het oplossen van afhankelijkheidsfouten [volgorde van de implementatie controleren](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="a6b96-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="a6b96-199">Deze fout wordt ook zien wanneer Hallo resource bestaat in een andere resourcegroep dan Hallo een wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a6b96-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="a6b96-200">Gebruik in dat geval Hallo [resourceId functie](resource-group-template-functions-resource.md#resourceid) tooget Hallo volledig gekwalificeerde naam van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="a6b96-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="a6b96-201">Als u toouse hello probeert [verwijzing](resource-group-template-functions-resource.md#reference) of [listKeys](resource-group-template-functions-resource.md#listkeys) werkt in combinatie met een resource die niet kunnen worden omgezet, u Hallo volgende fout ontvangen:</span><span class="sxs-lookup"><span data-stu-id="a6b96-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="a6b96-202">Zoek naar een expressie met Hallo **verwijzing** functie.</span><span class="sxs-lookup"><span data-stu-id="a6b96-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="a6b96-203">Controleer of de parameterwaarden Hallo juist zijn.</span><span class="sxs-lookup"><span data-stu-id="a6b96-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="a6b96-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="a6b96-204">ParentResourceNotFound</span></span>

<span data-ttu-id="a6b96-205">Wanneer een bron een bovenliggende tooanother resource is, moet Hallo bovenliggende resource bestaan voordat u Hallo onderliggende resource maakt.</span><span class="sxs-lookup"><span data-stu-id="a6b96-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="a6b96-206">Als deze nog niet bestaat, ontvangt u Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="a6b96-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="a6b96-207">Hallo-naam van Hallo onderliggende resource bevat de naam van de bovenliggende Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6b96-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="a6b96-208">Bijvoorbeeld, kunnen een SQL-Database worden gedefinieerd als:</span><span class="sxs-lookup"><span data-stu-id="a6b96-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="a6b96-209">Maar als u een afhankelijkheid op Hallo bovenliggende resource niet opgeeft, Hallo onderliggende resource kan ophalen geïmplementeerd voordat u Hallo bovenliggende.</span><span class="sxs-lookup"><span data-stu-id="a6b96-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="a6b96-210">tooresolve deze fout, bevatten een afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="a6b96-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="a6b96-211">StorageAccountAlreadyExists en StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="a6b96-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="a6b96-212">U moet een naam voor het Hallo-resource die uniek is voor alle Azure opgeven voor de storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="a6b96-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="a6b96-213">Als u niet een unieke naam opgeeft, wordt een fout als volgt:</span><span class="sxs-lookup"><span data-stu-id="a6b96-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="a6b96-214">U kunt een unieke naam maken met de naamgevingsconventie met Hallo resultaat Hallo cookievalidatie [uniqueString](resource-group-template-functions-string.md#uniquestring) functie.</span><span class="sxs-lookup"><span data-stu-id="a6b96-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="a6b96-215">Als u een opslagaccount met Hallo implementeert dezelfde naam als een bestaand opslagaccount in uw abonnement, maar bieden een andere locatie, er een foutbericht die duiden Hallo storage-account al in een andere locatie bestaat.</span><span class="sxs-lookup"><span data-stu-id="a6b96-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="a6b96-216">Verwijder de bestaande opslagaccount Hallo of bieden Hallo dezelfde locatie als Hallo bestaand opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="a6b96-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="a6b96-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="a6b96-217">AccountNameInvalid</span></span>
<span data-ttu-id="a6b96-218">U ziet Hallo **AccountNameInvalid** fout bij poging een storage account een naam met toogive tekens verboden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="a6b96-219">Namen van opslagaccounts moeten tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6b96-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="a6b96-220">Hallo [uniqueString](resource-group-template-functions-string.md#uniquestring) functie retourneert 13 tekens.</span><span class="sxs-lookup"><span data-stu-id="a6b96-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="a6b96-221">Als u een voorvoegsel toohello samenvoegen **uniqueString** leiden, geeft u een voorvoegsel 11 tekens of minder.</span><span class="sxs-lookup"><span data-stu-id="a6b96-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="a6b96-222">BadRequest</span><span class="sxs-lookup"><span data-stu-id="a6b96-222">BadRequest</span></span>

<span data-ttu-id="a6b96-223">De status van een BadRequest kunnen optreden wanneer u een ongeldige waarde voor een eigenschap opgeeft.</span><span class="sxs-lookup"><span data-stu-id="a6b96-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="a6b96-224">Bijvoorbeeld, als u een onjuiste waarde voor de SKU voor een opslagaccount, Hallo-implementatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a6b96-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="a6b96-225">geldige waarden voor de eigenschap toodetermine bekijkt hello [REST-API](/rest/api) voor Hallo brontype u implementeert.</span><span class="sxs-lookup"><span data-stu-id="a6b96-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="a6b96-226">NoRegisteredProviderFound en MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="a6b96-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="a6b96-227">Bij het implementeren van de resource kan u ontvangt Hallo foutcode te volgen en bericht:</span><span class="sxs-lookup"><span data-stu-id="a6b96-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="a6b96-228">Of een vergelijkbaar bericht waarin wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="a6b96-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="a6b96-229">U ontvangt deze fouten voor een van drie redenen:</span><span class="sxs-lookup"><span data-stu-id="a6b96-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="a6b96-230">Hallo-resourceprovider is niet geregistreerd voor uw abonnement</span><span class="sxs-lookup"><span data-stu-id="a6b96-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="a6b96-231">API-versie niet ondersteund voor het brontype Hallo</span><span class="sxs-lookup"><span data-stu-id="a6b96-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="a6b96-232">Locatie niet ondersteund voor het brontype Hallo</span><span class="sxs-lookup"><span data-stu-id="a6b96-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="a6b96-233">Fout bij het Hallo-bericht geeft suggesties voor Hallo ondersteund locaties en API-versies.</span><span class="sxs-lookup"><span data-stu-id="a6b96-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="a6b96-234">U kunt uw sjabloon tooone Hallo wijzigen voorgestelde waarden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="a6b96-235">De meeste providers worden automatisch door hello Azure portal of Hallo-opdrachtregelinterface u gebruikt, maar niet alle geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="a6b96-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="a6b96-236">Als u niet een bepaalde bron-provider voorafgaand aan hebt gebruikt, moet u mogelijk tooregister die provider.</span><span class="sxs-lookup"><span data-stu-id="a6b96-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="a6b96-237">U kunt meer informatie over resourceproviders via PowerShell of Azure CLI detecteren.</span><span class="sxs-lookup"><span data-stu-id="a6b96-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="a6b96-238">**Portal**</span><span class="sxs-lookup"><span data-stu-id="a6b96-238">**Portal**</span></span>

<span data-ttu-id="a6b96-239">U kunt zien Hallo registratiestatus en de naamruimte via Hallo portal een resourceprovider registreren.</span><span class="sxs-lookup"><span data-stu-id="a6b96-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="a6b96-240">Selecteer voor uw abonnement, **resourceproviders**.</span><span class="sxs-lookup"><span data-stu-id="a6b96-240">For your subscription, select **Resource providers**.</span></span>

   ![resourceproviders selecteren](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="a6b96-242">Bekijkt hello lijst met resourceproviders en indien nodig, selecteer Hallo **registreren** koppeling tooregister Hallo resourceprovider van het type Hallo u toodeploy probeert.</span><span class="sxs-lookup"><span data-stu-id="a6b96-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![resourceproviders vermelden](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="a6b96-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="a6b96-244">**PowerShell**</span></span>

<span data-ttu-id="a6b96-245">toosee uw registratiestatus, gebruik **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="a6b96-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="a6b96-246">tooregister een provider, gebruik **registreren AzureRmResourceProvider** en geef de naam Hallo Hallo resourceprovider dat u wenst dat tooregister.</span><span class="sxs-lookup"><span data-stu-id="a6b96-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="a6b96-247">tooget hello ondersteunde locaties voor een bepaald type resource, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a6b96-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="a6b96-248">tooget hello ondersteunde API-versies voor een bepaald type resource, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a6b96-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="a6b96-249">**Azure-CLI**</span><span class="sxs-lookup"><span data-stu-id="a6b96-249">**Azure CLI**</span></span>

<span data-ttu-id="a6b96-250">toosee of Hallo-provider is geregistreerd, gebruikt u Hallo `azure provider list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a6b96-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="a6b96-251">een resourceprovider tooregister gebruiken Hallo `azure provider register` opdracht in en geef Hallo *naamruimte* tooregister.</span><span class="sxs-lookup"><span data-stu-id="a6b96-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="a6b96-252">Gebruik toosee Hallo ondersteund locaties en API-versies voor een brontype:</span><span class="sxs-lookup"><span data-stu-id="a6b96-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="a6b96-253">QuotaExceeded en OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a6b96-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="a6b96-254">Mogelijk hebt u problemen als implementatie groter is dan een quotum die kan per resourcegroep, abonnementen, accounts en andere bereiken worden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="a6b96-255">Bijvoorbeeld, uw abonnement mogelijk geconfigureerd toolimit Hallo aantal kernen voor een regio.</span><span class="sxs-lookup"><span data-stu-id="a6b96-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="a6b96-256">Als u een virtuele machine met meer cores dan Hallo toegestaan bedrag toodeploy probeert, foutbericht er een waarin Hallo quotum is overschreden.</span><span class="sxs-lookup"><span data-stu-id="a6b96-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="a6b96-257">Zie voor informatie voltooid quotum [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="a6b96-258">tooexamine quota's voor uw abonnement voor kernen, kunt u Hallo `azure vm list-usage` opdracht in hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6b96-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="a6b96-259">Hallo volgende voorbeeld illustreert Hallo core quotum voor een gratis proefaccount 4 is:</span><span class="sxs-lookup"><span data-stu-id="a6b96-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="a6b96-260">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a6b96-260">Which returns:</span></span>

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

<span data-ttu-id="a6b96-261">Als u een sjabloon die meer dan vier kernen in de regio VS-West Hallo maakt implementeert, kunt u een implementatiefout dat lijkt op krijgen:</span><span class="sxs-lookup"><span data-stu-id="a6b96-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="a6b96-262">In PowerShell kunt u Hallo **Get-AzureRmVMUsage** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a6b96-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="a6b96-263">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a6b96-263">Which returns:</span></span>

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

<span data-ttu-id="a6b96-264">In dergelijke gevallen moet u toohello portal gaan en het bestand een probleem ondersteuning tooraise het quotum voor Hallo regio waarin u toodeploy wilt.</span><span class="sxs-lookup"><span data-stu-id="a6b96-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="a6b96-265">Vergeet niet dat voor de resourcegroepen Hallo quotum voor elke afzonderlijke regio, niet voor de hele abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="a6b96-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="a6b96-266">Als u nodig hebt toodeploy 30 kernen in VS-West, hebt u tooask voor 30 Resource Manager kernen in VS-West.</span><span class="sxs-lookup"><span data-stu-id="a6b96-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="a6b96-267">Als u toodeploy 30 kernen in een Hallo regio's toowhich moet hebt u toegang, moet u de vragen voor 30 Resource Manager kernen in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="a6b96-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="a6b96-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="a6b96-268">InvalidContentLink</span></span>
<span data-ttu-id="a6b96-269">Wanneer u wordt Hallo foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a6b96-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="a6b96-270">U hebt waarschijnlijk geprobeerd toolink tooa geneste sjabloon die niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a6b96-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="a6b96-271">Controleer hello URI die u hebt opgegeven voor geneste Hallo-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a6b96-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="a6b96-272">Als Hallo sjabloon in een opslagaccount bestaat, zorg er dan voor dat Hallo URI toegankelijk is.</span><span class="sxs-lookup"><span data-stu-id="a6b96-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="a6b96-273">Mogelijk moet u toopass een SAS-token.</span><span class="sxs-lookup"><span data-stu-id="a6b96-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="a6b96-274">Zie voor meer informatie [Gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="a6b96-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="a6b96-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="a6b96-276">U ontvangt deze foutmelding wanneer uw abonnement bevat een bronbeleid een actie die u probeert tooperform tijdens de implementatie wordt verhinderd.</span><span class="sxs-lookup"><span data-stu-id="a6b96-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="a6b96-277">In het foutbericht hello, zoekt u Hallo beleids-id.</span><span class="sxs-lookup"><span data-stu-id="a6b96-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="a6b96-278">In **PowerShell**, bieden die beleids-id als Hallo **Id** parameter tooretrieve details over Hallo-beleid dat uw implementatie geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="a6b96-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="a6b96-279">In **Azure CLI**, Hallo-naam van de beleidsdefinitie Hallo bieden:</span><span class="sxs-lookup"><span data-stu-id="a6b96-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="a6b96-280">Zie voor meer informatie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6b96-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="a6b96-281">RequestDisallowedByPolicy-fout</span><span class="sxs-lookup"><span data-stu-id="a6b96-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="a6b96-282">[Gebruik beleid toomanage bronnen en toegangsbeheer](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="a6b96-283">Verificatie mislukt</span><span class="sxs-lookup"><span data-stu-id="a6b96-283">Authorization failed</span></span>
<span data-ttu-id="a6b96-284">Wordt een fout opgetreden tijdens de implementatie omdat Hallo-account of service-principal probeert toodeploy Hallo bronnen geen toegang tooperform die acties heeft.</span><span class="sxs-lookup"><span data-stu-id="a6b96-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="a6b96-285">Azure Active Directory kunt u of uw beheerder toocontrol welke identiteiten toegang welke bronnen in grote mate van precisie tot.</span><span class="sxs-lookup"><span data-stu-id="a6b96-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="a6b96-286">Bijvoorbeeld, als uw account is toegewezen met de rol Lezer toohello, bent u niet kunt toocreate resources.</span><span class="sxs-lookup"><span data-stu-id="a6b96-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="a6b96-287">In dat geval ziet u een foutmelding autorisatie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="a6b96-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="a6b96-288">Zie voor meer informatie over op rollen gebaseerde toegangsbeheer [rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a6b96-289">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6b96-289">Next steps</span></span>
* <span data-ttu-id="a6b96-290">toolearn over het controleren van acties, Zie [bewerkingen met Resource Manager controleren](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="a6b96-291">Zie toolearn over acties toodetermine Hallo fouten tijdens de implementatie van [implementatiebewerkingen weergeven](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a6b96-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
