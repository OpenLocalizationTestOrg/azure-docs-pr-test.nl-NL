---
title: aaaAzure resourceproviders en brontypen | Microsoft Docs
description: Beschrijft Hallo resourceproviders die ondersteuning bieden voor Resource Manager, hun schema's en de beschikbare API-versies en Hallo-regio's die kunnen Hallo-bronnen hosten.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 3c7a6fe4-371a-40da-9ebe-b574f583305b
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: tomfitz
ms.openlocfilehash: 23db1d3808a20166f3b44ec801e1bcc46fbb9bd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-providers-and-types"></a><span data-ttu-id="3f051-103">Resourceproviders en typen</span><span class="sxs-lookup"><span data-stu-id="3f051-103">Resource providers and types</span></span>

<span data-ttu-id="3f051-104">Bij het implementeren van resources, moet u vaak tooretrieve informatie over de resourceproviders hello en typen.</span><span class="sxs-lookup"><span data-stu-id="3f051-104">When deploying resources, you frequently need tooretrieve information about hello resource providers and types.</span></span> <span data-ttu-id="3f051-105">In dit artikel leert hoe u u kunt:</span><span class="sxs-lookup"><span data-stu-id="3f051-105">In this article, you learn to:</span></span>

* <span data-ttu-id="3f051-106">Alle resourceproviders bekijken in Azure</span><span class="sxs-lookup"><span data-stu-id="3f051-106">View all resource providers in Azure</span></span>
* <span data-ttu-id="3f051-107">Controleer de status van de registratie van een resourceprovider</span><span class="sxs-lookup"><span data-stu-id="3f051-107">Check registration status of a resource provider</span></span>
* <span data-ttu-id="3f051-108">Een resourceprovider registreren</span><span class="sxs-lookup"><span data-stu-id="3f051-108">Register a resource provider</span></span>
* <span data-ttu-id="3f051-109">Weergave brontypen die voor een resourceprovider</span><span class="sxs-lookup"><span data-stu-id="3f051-109">View resource types for a resource provider</span></span>
* <span data-ttu-id="3f051-110">Geldige locaties van de weergave voor een brontype</span><span class="sxs-lookup"><span data-stu-id="3f051-110">View valid locations for a resource type</span></span>
* <span data-ttu-id="3f051-111">Geldige API-versies voor een resourcetype weergeven</span><span class="sxs-lookup"><span data-stu-id="3f051-111">View valid API versions for a resource type</span></span>

<span data-ttu-id="3f051-112">U kunt deze stappen via Hallo-portal, PowerShell of Azure CLI kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3f051-112">You can perform these steps through hello portal, PowerShell, or Azure CLI.</span></span>

## <a name="powershell"></a><span data-ttu-id="3f051-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f051-113">PowerShell</span></span>

<span data-ttu-id="3f051-114">toosee gebruiken voor alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="3f051-114">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable | Select-Object ProviderNamespace, RegistrationState
```

<span data-ttu-id="3f051-115">Die resultaten weer die vergelijkbaar is met:</span><span class="sxs-lookup"><span data-stu-id="3f051-115">Which returns results similar to:</span></span>

```powershell
ProviderNamespace                RegistrationState
-------------------------------- ------------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="3f051-116">Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-116">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="3f051-117">Hallo-bereik voor de registratie is altijd Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f051-117">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="3f051-118">Veel resourceproviders worden standaard automatisch geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3f051-118">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="3f051-119">Echter, moet u mogelijk toomanually sommige resourceproviders registreren.</span><span class="sxs-lookup"><span data-stu-id="3f051-119">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="3f051-120">een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-120">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="3f051-121">Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen.</span><span class="sxs-lookup"><span data-stu-id="3f051-121">This operation is included in hello Contributor and Owner roles.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="3f051-122">Die resultaten weer die vergelijkbaar is met:</span><span class="sxs-lookup"><span data-stu-id="3f051-122">Which returns results similar to:</span></span>

```powershell
ProviderNamespace : Microsoft.Batch
RegistrationState : Registering
ResourceTypes     : {batchAccounts, operations, locations, locations/quotas}
Locations         : {West Europe, East US, East US 2, West US...}
```

<span data-ttu-id="3f051-123">U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="3f051-123">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="3f051-124">toosee-informatie voor een bepaalde bron-provider, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-124">toosee information for a particular resource provider, use:</span></span>

```powershell
Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
```

<span data-ttu-id="3f051-125">Die resultaten weer die vergelijkbaar is met:</span><span class="sxs-lookup"><span data-stu-id="3f051-125">Which returns results similar to:</span></span>

```powershell
{ProviderNamespace : Microsoft.Batch
RegistrationState : Registered
ResourceTypes     : {batchAccounts}
Locations         : {West Europe, East US, East US 2, West US...}

...
```

<span data-ttu-id="3f051-126">toosee hello brontypen die voor een resourceprovider gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-126">toosee hello resource types for a resource provider, use:</span></span>

```powershell
(Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes.ResourceTypeName
```

<span data-ttu-id="3f051-127">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-127">Which returns:</span></span>

```powershell
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="3f051-128">Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-128">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="3f051-129">Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="3f051-129">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="3f051-130">tooget hello beschikbare API-versies voor een brontype gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-130">tooget hello available API versions for a resource type, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).ApiVersions
```

<span data-ttu-id="3f051-131">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-131">Which returns:</span></span>

```powershell
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="3f051-132">Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="3f051-132">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="3f051-133">Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f051-133">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="3f051-134">tooget hello ondersteunde locaties voor een resourcetype gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f051-134">tooget hello supported locations for a resource type, use.</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

<span data-ttu-id="3f051-135">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-135">Which returns:</span></span>

```powershell
West Europe
East US
East US 2
West US
...
```

## <a name="azure-cli"></a><span data-ttu-id="3f051-136">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3f051-136">Azure CLI</span></span>
<span data-ttu-id="3f051-137">toosee gebruiken voor alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="3f051-137">toosee all resource providers in Azure, and hello registration status for your subscription, use:</span></span>

```azurecli
az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table
```

<span data-ttu-id="3f051-138">Die resultaten weer die vergelijkbaar is met:</span><span class="sxs-lookup"><span data-stu-id="3f051-138">Which returns results similar to:</span></span>

```azurecli
Provider                         Status
-------------------------------- ----------------
Microsoft.ClassicCompute         Registered
Microsoft.ClassicNetwork         Registered
Microsoft.ClassicStorage         Registered
Microsoft.CognitiveServices      Registered
...
```

<span data-ttu-id="3f051-139">Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-139">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="3f051-140">Hallo-bereik voor de registratie is altijd Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f051-140">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="3f051-141">Veel resourceproviders worden standaard automatisch geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3f051-141">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="3f051-142">Echter, moet u mogelijk toomanually sommige resourceproviders registreren.</span><span class="sxs-lookup"><span data-stu-id="3f051-142">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="3f051-143">een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-143">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="3f051-144">Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen.</span><span class="sxs-lookup"><span data-stu-id="3f051-144">This operation is included in hello Contributor and Owner roles.</span></span>

```azurecli
az provider register --namespace Microsoft.Batch
```

<span data-ttu-id="3f051-145">Retourneert het bericht van deze inschrijving is continu.</span><span class="sxs-lookup"><span data-stu-id="3f051-145">Which returns a message that registration is on-going.</span></span>

<span data-ttu-id="3f051-146">U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="3f051-146">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="3f051-147">toosee-informatie voor een bepaalde bron-provider, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-147">toosee information for a particular resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch
```

<span data-ttu-id="3f051-148">Die resultaten weer die vergelijkbaar is met:</span><span class="sxs-lookup"><span data-stu-id="3f051-148">Which returns results similar to:</span></span>

```azurecli
{
    "id": "/subscriptions/####-####/providers/Microsoft.Batch",
    "namespace": "Microsoft.Batch",
    "registrationsState": "Registering",
    "resourceTypes:" [
        ...
    ]
}
```

<span data-ttu-id="3f051-149">toosee hello brontypen die voor een resourceprovider gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-149">toosee hello resource types for a resource provider, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[*].resourceType" --out table
```

<span data-ttu-id="3f051-150">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-150">Which returns:</span></span>

```azurecli
Result
---------------
batchAccounts
operations
locations
locations/quotas
```

<span data-ttu-id="3f051-151">Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-151">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="3f051-152">Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="3f051-152">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> 

<span data-ttu-id="3f051-153">tooget hello beschikbare API-versies voor een brontype gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3f051-153">tooget hello available API versions for a resource type, use:</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].apiVersions | [0]" --out table
```

<span data-ttu-id="3f051-154">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-154">Which returns:</span></span>

```azurecli
Result
---------------
2017-05-01
2017-01-01
2015-12-01
2015-09-01
2015-07-01
```

<span data-ttu-id="3f051-155">Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="3f051-155">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="3f051-156">Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f051-156">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> 

<span data-ttu-id="3f051-157">tooget hello ondersteunde locaties voor een resourcetype gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f051-157">tooget hello supported locations for a resource type, use.</span></span>

```azurecli
az provider show --namespace Microsoft.Batch --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" --out table
```

<span data-ttu-id="3f051-158">Die wordt geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="3f051-158">Which returns:</span></span>

```azurecli
Result
---------------
West Europe
East US
East US 2
West US
...
```

## <a name="portal"></a><span data-ttu-id="3f051-159">Portal</span><span class="sxs-lookup"><span data-stu-id="3f051-159">Portal</span></span>

<span data-ttu-id="3f051-160">alle resourceproviders in Azure en Hallo Registratiestatus voor uw abonnement, selecteert u toosee **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="3f051-160">toosee all resource providers in Azure, and hello registration status for your subscription, select **Subscriptions**.</span></span>

![Selecteer abonnementen](./media/resource-manager-supported-services/select-subscriptions.png)

<span data-ttu-id="3f051-162">Hallo abonnement tooview kiezen.</span><span class="sxs-lookup"><span data-stu-id="3f051-162">Choose hello subscription tooview.</span></span>

![abonnement opgeven](./media/resource-manager-supported-services/subscription.png)

<span data-ttu-id="3f051-164">Selecteer **resourceproviders** en Hallo lijst met beschikbare resourceproviders bekijken.</span><span class="sxs-lookup"><span data-stu-id="3f051-164">Select **Resource providers** and view hello list of available resource providers.</span></span>

![resourceproviders weergeven](./media/resource-manager-supported-services/show-resource-providers.png)

<span data-ttu-id="3f051-166">Een resourceprovider registreren, configureert uw abonnement toowork met Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-166">Registering a resource provider configures your subscription toowork with hello resource provider.</span></span> <span data-ttu-id="3f051-167">Hallo-bereik voor de registratie is altijd Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3f051-167">hello scope for registration is always hello subscription.</span></span> <span data-ttu-id="3f051-168">Veel resourceproviders worden standaard automatisch geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3f051-168">By default, many resource providers are automatically registered.</span></span> <span data-ttu-id="3f051-169">Echter, moet u mogelijk toomanually sommige resourceproviders registreren.</span><span class="sxs-lookup"><span data-stu-id="3f051-169">However, you may need toomanually register some resource providers.</span></span> <span data-ttu-id="3f051-170">een resourceprovider tooregister, hebt u toestemming tooperform hello `/register/action` bewerking voor het Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-170">tooregister a resource provider, you must have permission tooperform hello `/register/action` operation for hello resource provider.</span></span> <span data-ttu-id="3f051-171">Deze bewerking is opgenomen in Hallo Inzender en de eigenaar van rollen.</span><span class="sxs-lookup"><span data-stu-id="3f051-171">This operation is included in hello Contributor and Owner roles.</span></span> <span data-ttu-id="3f051-172">Selecteer tooregister een resourceprovider **registreren**.</span><span class="sxs-lookup"><span data-stu-id="3f051-172">tooregister a resource provider, select **Register**.</span></span>

![de registerbronprovider](./media/resource-manager-supported-services/register-provider.png)

<span data-ttu-id="3f051-174">U kunt de registratie ongedaan een resourceprovider kan niet maken wanneer u nog steeds brontypen van die resourceprovider in uw abonnement hebt.</span><span class="sxs-lookup"><span data-stu-id="3f051-174">You cannot unregister a resource provider when you still have resource types from that resource provider in your subscription.</span></span>

<span data-ttu-id="3f051-175">toosee-informatie voor een bepaalde bron-provider, selecteer **meer services**.</span><span class="sxs-lookup"><span data-stu-id="3f051-175">toosee information for a particular resource provider, select **More services**.</span></span>

![meer services selecteren](./media/resource-manager-supported-services/more-services.png)

<span data-ttu-id="3f051-177">Zoeken naar **Resource Explorer** en selecteer het uit de beschikbare opties Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f051-177">Search for **Resource Explorer** and select it from hello available options.</span></span>

![Selecteer resource explorer](./media/resource-manager-supported-services/select-resource-explorer.png)

<span data-ttu-id="3f051-179">Selecteer **Providers**.</span><span class="sxs-lookup"><span data-stu-id="3f051-179">Select **Providers**.</span></span>

![Providers selecteren](./media/resource-manager-supported-services/select-providers.png)

<span data-ttu-id="3f051-181">Selecteer Hallo resourceprovider en resource typt de gewenste tooview.</span><span class="sxs-lookup"><span data-stu-id="3f051-181">Select hello resource provider and resource type that you want tooview.</span></span>

![Brontype selecteren](./media/resource-manager-supported-services/select-resource-type.png)

<span data-ttu-id="3f051-183">Resource Manager wordt ondersteund in alle regio's, maar het Hallo-resources die u implementeert wordt mogelijk niet ondersteund in alle regio's.</span><span class="sxs-lookup"><span data-stu-id="3f051-183">Resource Manager is supported in all regions, but hello resources you deploy might not be supported in all regions.</span></span> <span data-ttu-id="3f051-184">Bovendien mogelijk zijn er beperkingen met betrekking tot uw abonnement die voorkomen dat u sommige regio's die ondersteuning bieden voor Hallo resource gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f051-184">In addition, there may be limitations on your subscription that prevent you from using some regions that support hello resource.</span></span> <span data-ttu-id="3f051-185">Hallo resource explorer weergegeven geldige locaties voor Hallo brontype.</span><span class="sxs-lookup"><span data-stu-id="3f051-185">hello resource explorer displays valid locations for hello resource type.</span></span>

![Locaties weergeven](./media/resource-manager-supported-services/show-locations.png)

<span data-ttu-id="3f051-187">Hallo-API-versie komt overeen tooa versie van de REST-API-bewerkingen die zijn vrijgegeven door Hallo-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="3f051-187">hello API version corresponds tooa version of REST API operations that are released by hello resource provider.</span></span> <span data-ttu-id="3f051-188">Als een resourceprovider kunt nieuwe functies, geeft dit een nieuwe versie van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="3f051-188">As a resource provider enables new features, it releases a new version of hello REST API.</span></span> <span data-ttu-id="3f051-189">Hallo resource explorer geeft geldige API-versies voor het brontype Hallo weer.</span><span class="sxs-lookup"><span data-stu-id="3f051-189">hello resource explorer displays valid API versions for hello resource type.</span></span>

![API-versies weergeven](./media/resource-manager-supported-services/show-api-versions.png)

## <a name="next-steps"></a><span data-ttu-id="3f051-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f051-191">Next steps</span></span>
* <span data-ttu-id="3f051-192">toolearn over het maken van Resource Manager-sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3f051-192">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="3f051-193">toolearn over het implementeren van resources, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3f051-193">toolearn about deploying resources, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="3f051-194">Zie tooview Hallo bewerkingen voor een resourceprovider [REST API van Azure](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="3f051-194">tooview hello operations for a resource provider, see [Azure REST API](/rest/api/).</span></span>

