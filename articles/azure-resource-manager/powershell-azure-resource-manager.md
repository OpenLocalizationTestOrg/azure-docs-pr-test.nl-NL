---
title: Beheren van Azure-oplossingen met PowerShell | Microsoft Docs
description: Azure PowerShell en Resource Manager gebruiken voor het beheren van uw resources.
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: ff42e5cb29005c5f4b97babdae58bef9382071f0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="e53a0-103">Resources beheren met Azure PowerShell en Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e53a0-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e53a0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="e53a0-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="e53a0-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e53a0-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="e53a0-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53a0-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="e53a0-107">REST API</span><span class="sxs-lookup"><span data-stu-id="e53a0-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="e53a0-108">In dit artikel leert u hoe u uw oplossingen met Azure PowerShell en Azure Resource Manager beheert.</span><span class="sxs-lookup"><span data-stu-id="e53a0-108">In this article, you learn how to manage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="e53a0-109">Als u niet bekend met Resource Manager, Zie [overzicht van Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="e53a0-110">Dit onderwerp richt zich op beheertaken.</span><span class="sxs-lookup"><span data-stu-id="e53a0-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="e53a0-111">U gaat het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="e53a0-111">You will:</span></span>

1. <span data-ttu-id="e53a0-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e53a0-112">Create a resource group</span></span>
2. <span data-ttu-id="e53a0-113">Een resource toevoegen aan de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e53a0-113">Add a resource to the resource group</span></span>
3. <span data-ttu-id="e53a0-114">Een label toevoegen aan de bron</span><span class="sxs-lookup"><span data-stu-id="e53a0-114">Add a tag to the resource</span></span>
4. <span data-ttu-id="e53a0-115">Een query uitvoeren op basis van namen of labelwaarden resources</span><span class="sxs-lookup"><span data-stu-id="e53a0-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="e53a0-116">Toepassen en verwijderen van een vergrendeling op de bron</span><span class="sxs-lookup"><span data-stu-id="e53a0-116">Apply and remove a lock on the resource</span></span>
6. <span data-ttu-id="e53a0-117">Verwijderen van een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e53a0-117">Delete a resource group</span></span>

<span data-ttu-id="e53a0-118">In dit artikel wordt niet weergegeven voor het implementeren van een Resource Manager-sjabloon aan uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e53a0-118">This article does not show how to deploy a Resource Manager template to your subscription.</span></span> <span data-ttu-id="e53a0-119">Zie voor die informatie [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="e53a0-120">Aan de slag met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e53a0-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="e53a0-121">Als u Azure PowerShell nog niet hebt geïnstalleerd, raadpleegt u [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e53a0-121">If you have not installed Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="e53a0-122">Als u Azure PowerShell in het verleden hebt geïnstalleerd, maar hebben niet het onlangs bijgewerkt, kunt u de nieuwste versie installeert.</span><span class="sxs-lookup"><span data-stu-id="e53a0-122">If you have installed Azure PowerShell in the past but have not updated it recently, consider installing the latest version.</span></span> <span data-ttu-id="e53a0-123">U kunt de versie bijwerken met de dezelfde methode die u hebt gebruikt om deze te installeren.</span><span class="sxs-lookup"><span data-stu-id="e53a0-123">You can update the version through the same method you used to install it.</span></span> <span data-ttu-id="e53a0-124">Als u het Webplatforminstallatieprogramma gebruikt, bijvoorbeeld opnieuw te starten en zoekt u een update.</span><span class="sxs-lookup"><span data-stu-id="e53a0-124">For example, if you used the Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="e53a0-125">Gebruik de volgende cmdlet te controleren van uw versie van de module voor Azure-Resources:</span><span class="sxs-lookup"><span data-stu-id="e53a0-125">To check your version of the Azure Resources module, use the following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="e53a0-126">In dit onderwerp is bijgewerkt voor versie 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="e53a0-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="e53a0-127">Als u een eerdere versie hebt, uw ervaring mogelijk niet overeen met de stappen in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e53a0-127">If you have an earlier version, your experience might not match the steps shown in this topic.</span></span> <span data-ttu-id="e53a0-128">Zie voor documentatie over de cmdlets in deze versie [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="e53a0-128">For documentation about the cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-to-your-azure-account"></a><span data-ttu-id="e53a0-129">Aanmelden bij uw Azure-account</span><span class="sxs-lookup"><span data-stu-id="e53a0-129">Log in to your Azure account</span></span>
<span data-ttu-id="e53a0-130">Voordat u aan uw oplossing werkt, moet u zich aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="e53a0-130">Before working on your solution, you must log in to your account.</span></span>

<span data-ttu-id="e53a0-131">Voor het aanmelden bij uw Azure-account, gebruiken de **Login-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e53a0-131">To log in to your Azure account, use the **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="e53a0-132">De cmdlet vraagt u om de aanmeldingsreferenties voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e53a0-132">The cmdlet prompts you for the login credentials for your Azure account.</span></span> <span data-ttu-id="e53a0-133">Na het aanmelden, worden de instellingen van uw account gedownload zodat ze beschikbaar zijn voor Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e53a0-133">After logging in, it downloads your account settings so they are available to Azure PowerShell.</span></span>

<span data-ttu-id="e53a0-134">De cmdlet retourneert informatie over uw account en het abonnement moet worden gebruikt voor de taken.</span><span class="sxs-lookup"><span data-stu-id="e53a0-134">The cmdlet returns information about your account and the subscription to use for the tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="e53a0-135">Als u meer dan één abonnement hebt, kunt u overschakelen naar een ander abonnement.</span><span class="sxs-lookup"><span data-stu-id="e53a0-135">If you have more than one subscription, you can switch to a different subscription.</span></span> <span data-ttu-id="e53a0-136">Eerst gaan we kijken alle abonnementen voor uw account.</span><span class="sxs-lookup"><span data-stu-id="e53a0-136">First, let's see all the subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="e53a0-137">Het resultaat van ingeschakelde en uitgeschakelde abonnementen.</span><span class="sxs-lookup"><span data-stu-id="e53a0-137">It returns enabled and disabled subscriptions.</span></span>

```powershell
SubscriptionName : Example Subscription One
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Two
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Enabled

SubscriptionName : Example Subscription Three
SubscriptionId   : {guid}
TenantId         : {guid}
State            : Disabled
```

<span data-ttu-id="e53a0-138">Als u wilt overschakelen naar een ander abonnement, geef de naam van het abonnement met de **Set-AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e53a0-138">To switch to a different subscription, provide the subscription name with the **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="e53a0-139">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="e53a0-139">Create a resource group</span></span>
<span data-ttu-id="e53a0-140">Voordat u implementeert geen bronnen aan uw abonnement, moet u een resourcegroep met de bronnen.</span><span class="sxs-lookup"><span data-stu-id="e53a0-140">Before deploying any resources to your subscription, you must create a resource group that will contain the resources.</span></span>

<span data-ttu-id="e53a0-141">Voor het maken van een resourcegroep gebruikt de **New-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e53a0-141">To create a resource group, use the **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="e53a0-142">Gebruikt de opdracht de **naam** parameter om een naam voor de resourcegroep en de **locatie** parameter om de locatie.</span><span class="sxs-lookup"><span data-stu-id="e53a0-142">The command uses the **Name** parameter to specify a name for the resource group and the **Location** parameter to specify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="e53a0-143">De uitvoer is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="e53a0-143">The output is in the following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="e53a0-144">Als u de resourcegroep later nodig, gebruikt u de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e53a0-144">If you need to retrieve the resource group later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="e53a0-145">Geef een naam niet voor alle resourcegroepen in uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="e53a0-145">To get all the resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-to-a-resource-group"></a><span data-ttu-id="e53a0-146">Resources toevoegen aan een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e53a0-146">Add resources to a resource group</span></span>
<span data-ttu-id="e53a0-147">Als u wilt een resource toevoegen aan de resourcegroep, kunt u de **nieuw AzureRmResource** cmdlet of een cmdlet die specifiek is voor het type resource dat u maakt (zoals **nieuw AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="e53a0-147">To add a resource to the resource group, you can use the **New-AzureRmResource** cmdlet or a cmdlet that is specific to the type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="e53a0-148">Wellicht eenvoudiger te gebruiken van een cmdlet die specifiek is voor een resourcetype omdat deze parameters voor de eigenschappen die nodig zijn voor de nieuwe resource bevat.</span><span class="sxs-lookup"><span data-stu-id="e53a0-148">You might find it easier to use a cmdlet that is specific to a resource type because it includes parameters for the properties that are needed for the new resource.</span></span> <span data-ttu-id="e53a0-149">Gebruik **nieuw AzureRmResource**, moet u de eigenschappen in te stellen zonder te worden gevraagd voor hen kennen.</span><span class="sxs-lookup"><span data-stu-id="e53a0-149">To use **New-AzureRmResource**, you must know all the properties to set without being prompted for them.</span></span>

<span data-ttu-id="e53a0-150">Echter, toevoegen van een resource via cmdlets kan veroorzaken toekomstige verwarring omdat de nieuwe resource niet in een Resource Manager-sjabloon bestaat.</span><span class="sxs-lookup"><span data-stu-id="e53a0-150">However, adding a resource through cmdlets might cause future confusion because the new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="e53a0-151">Microsoft raadt u aan het definiëren van de infrastructuur voor uw Azure-oplossing in Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="e53a0-151">Microsoft recommends defining the infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="e53a0-152">Sjablonen kunnen u op betrouwbare wijze en herhaaldelijk implementeren van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="e53a0-152">Templates enable you to reliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="e53a0-153">Voor dit onderwerp, hebt u een opslagaccount met een PowerShell-cmdlet, maar later het genereren van een sjabloon uit de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e53a0-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="e53a0-154">De volgende cmdlet maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e53a0-154">The following cmdlet creates a storage account.</span></span> <span data-ttu-id="e53a0-155">In plaats van de naam die wordt weergegeven in het voorbeeld, Geef een unieke naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e53a0-155">Instead of using the name shown in the example, provide a unique name for the storage account.</span></span> <span data-ttu-id="e53a0-156">De naam moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e53a0-156">The name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="e53a0-157">Als u de naam die wordt weergegeven in het voorbeeld gebruikt, ontvangt u een fout opgetreden omdat deze naam al gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="e53a0-157">If you use the name shown in the example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="e53a0-158">Als u deze bron later nodig, gebruikt u de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e53a0-158">If you need to retrieve this resource later, use the following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="e53a0-159">Een label toevoegen</span><span class="sxs-lookup"><span data-stu-id="e53a0-159">Add a tag</span></span>

<span data-ttu-id="e53a0-160">Labels kunnen u om uw resources op basis van andere eigenschappen te organiseren.</span><span class="sxs-lookup"><span data-stu-id="e53a0-160">Tags enable you to organize your resources according to different properties.</span></span> <span data-ttu-id="e53a0-161">Bijvoorbeeld wellicht verschillende resources in verschillende resourcegroepen die deel uitmaken van dezelfde afdeling.</span><span class="sxs-lookup"><span data-stu-id="e53a0-161">For example, you may have several resources in different resource groups that belong to the same department.</span></span> <span data-ttu-id="e53a0-162">U kunt een label voor afdeling en de waarde toepassen op deze resources om deze te markeren als onderdeel van dezelfde categorie.</span><span class="sxs-lookup"><span data-stu-id="e53a0-162">You can apply a department tag and value to those resources to mark them as belonging to the same category.</span></span> <span data-ttu-id="e53a0-163">Of u kunt markeren of een resource wordt gebruikt in een productie- of testomgeving.</span><span class="sxs-lookup"><span data-stu-id="e53a0-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="e53a0-164">In dit onderwerp leert u tags toepassen op slechts één resource, maar in uw omgeving is het waarschijnlijk wel zinvol tags toepassen op al uw resources.</span><span class="sxs-lookup"><span data-stu-id="e53a0-164">In this topic, you apply tags to only one resource, but in your environment it most likely makes sense to apply tags to all your resources.</span></span>

<span data-ttu-id="e53a0-165">De volgende cmdlet geldt twee tags voor uw opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="e53a0-165">The following cmdlet applies two tags to your storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="e53a0-166">Labels zijn als een enkel object bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="e53a0-166">Tags are updated as a single object.</span></span> <span data-ttu-id="e53a0-167">Als u wilt een code toevoegt aan een resource die al tags bevat, moet u eerst de bestaande labels ophalen.</span><span class="sxs-lookup"><span data-stu-id="e53a0-167">To add a tag to a resource that already includes tags, first retrieve the existing tags.</span></span> <span data-ttu-id="e53a0-168">Nieuw label toevoegen aan het object dat de bestaande labels bevat en alle tags toepassen op de resource.</span><span class="sxs-lookup"><span data-stu-id="e53a0-168">Add the new tag to the object that contains the existing tags, and reapply all the tags to the resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="e53a0-169">Zoeken naar resources</span><span class="sxs-lookup"><span data-stu-id="e53a0-169">Search for resources</span></span>

<span data-ttu-id="e53a0-170">Gebruik de **zoeken AzureRmResource** cmdlet voor het ophalen van bronnen voor verschillende zoekcriteria.</span><span class="sxs-lookup"><span data-stu-id="e53a0-170">Use the **Find-AzureRmResource** cmdlet to retrieve resources for different search conditions.</span></span>

* <span data-ttu-id="e53a0-171">Als u een resource met de naam, bieden de **ResourceNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="e53a0-171">To get a resource by name, provide the **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="e53a0-172">Als u alle resources in een resourcegroep, bieden de **ResourceGroupNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="e53a0-172">To get all the resources in a resource group, provide the **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="e53a0-173">Als u de resources met een naam en waarde, bieden de **TagName** en **TagValue** parameters:</span><span class="sxs-lookup"><span data-stu-id="e53a0-173">To get all the resources with a tag name and value, provide the **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="e53a0-174">Alle resources met een bepaald resourcetype, geeft u de **ResourceType** parameter:</span><span class="sxs-lookup"><span data-stu-id="e53a0-174">To all the resources with a particular resource type, provide the **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="e53a0-175">Vergrendelen van een resource</span><span class="sxs-lookup"><span data-stu-id="e53a0-175">Lock a resource</span></span>

<span data-ttu-id="e53a0-176">Als u controleren of een essentiële resource niet per ongeluk is verwijderd of gewijzigd wilt, moet u een vergrendeling toegepast op de resource.</span><span class="sxs-lookup"><span data-stu-id="e53a0-176">When you need to make sure a critical resource is not accidentally deleted or modified, apply a lock to the resource.</span></span> <span data-ttu-id="e53a0-177">U kunt opgeven dat ofwel een **CanNotDelete** of **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="e53a0-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="e53a0-178">Als u wilt maken of verwijderen van management vergrendelingen, u moet toegang hebben tot `Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties.</span><span class="sxs-lookup"><span data-stu-id="e53a0-178">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="e53a0-179">Van de ingebouwde rollen worden alleen de eigenaar en de beheerder voor gebruikerstoegang die acties verleend.</span><span class="sxs-lookup"><span data-stu-id="e53a0-179">Of the built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="e53a0-180">Als u wilt toepassen op een vergrendeling, gebruikt u de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="e53a0-180">To apply a lock, use the following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="e53a0-181">De vergrendelde resource in het vorige voorbeeld kan niet worden verwijderd, totdat de vergrendeling wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e53a0-181">The locked resource in the preceding example cannot be deleted until the lock is removed.</span></span> <span data-ttu-id="e53a0-182">Gebruik voor het verwijderen van een vergrendeling:</span><span class="sxs-lookup"><span data-stu-id="e53a0-182">To remove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="e53a0-183">Zie voor meer informatie over de instelling vergrendelingen [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="e53a0-184">Verwijder resources of resourcegroep</span><span class="sxs-lookup"><span data-stu-id="e53a0-184">Remove resources or resource group</span></span>
<span data-ttu-id="e53a0-185">U kunt een resource of resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="e53a0-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="e53a0-186">Wanneer u een resourcegroep verwijdert, verwijdert u ook alle resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e53a0-186">When you remove a resource group, you also remove all the resources within that resource group.</span></span>

* <span data-ttu-id="e53a0-187">Als u wilt een bron verwijdert uit de resourcegroep, gebruiken de **verwijderen AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e53a0-187">To delete a resource from the resource group, use the **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="e53a0-188">Deze cmdlet de resource wordt verwijderd, maar de resourcegroep niet verwijdert.</span><span class="sxs-lookup"><span data-stu-id="e53a0-188">This cmdlet deletes the resource, but does not delete the resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="e53a0-189">U een resourcegroep en de bijhorende resources verwijderen met de **Remove-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e53a0-189">To delete a resource group and all its resources, use the **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="e53a0-190">Voor beide cmdlets, wordt u gevraagd te bevestigen dat u wilt verwijderen van de resource of resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e53a0-190">For both cmdlets, you are asked to confirm that you wish to remove the resource or resource group.</span></span> <span data-ttu-id="e53a0-191">Als de bewerking is Hiermee verwijdert u de resource of resourcegroep, retourneert **True**.</span><span class="sxs-lookup"><span data-stu-id="e53a0-191">If the operation successfully deletes the resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="e53a0-192">Resource Manager-scripts uitvoeren met Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e53a0-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="e53a0-193">Dit onderwerp leest u hoe u basisbewerkingen op uw resources met Azure PowerShell uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e53a0-193">This topic shows you how to perform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="e53a0-194">Voor meer geavanceerde scenario's voor beheer wilt u waarschijnlijk een script maken en hergebruiken script naar behoefte of volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="e53a0-194">For more advanced management scenarios, you typically want to create a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="e53a0-195">[Azure Automation](../automation/automation-intro.md) biedt een manier om u te vaak automatiseren gebruikt scripts waarmee uw Azure-oplossingen kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="e53a0-195">[Azure Automation](../automation/automation-intro.md) provides a way for you to automate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="e53a0-196">De volgende onderwerpen beschreven hoe u met Azure Automation, Resource Manager en PowerShell effectief beheertaken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e53a0-196">The following topics show you how to use Azure Automation, Resource Manager, and PowerShell to effectively perform management tasks:</span></span>

- <span data-ttu-id="e53a0-197">Zie voor meer informatie over het maken van een runbook [Mijn eerste PowerShell-runbook](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="e53a0-198">Zie voor meer informatie over het werken met galerieën scripts [galerieën Runbook en de module voor Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="e53a0-199">Zie voor runbooks die starten en stoppen van virtuele machines, [Azure Automation-scenario: labels met behulp van JSON-indeling voor het maken van een planning voor de virtuele machine van Azure opstarten en afsluiten](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags to create a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="e53a0-200">Zie voor runbooks die starten en stoppen van virtuele machines rustige uren, [starten/stoppen virtuele machines tijdens rustige uren oplossing in Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e53a0-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e53a0-201">Next steps</span></span>
* <span data-ttu-id="e53a0-202">Zie voor meer informatie over het maken van Resource Manager-sjablonen, [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-202">To learn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="e53a0-203">Zie voor meer informatie over het implementeren van sjablonen, [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-203">To learn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="e53a0-204">U kunt bestaande resources verplaatsen naar een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e53a0-204">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="e53a0-205">Zie voor voorbeelden [Resources verplaatsen naar de nieuwe resourcegroep of abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-205">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="e53a0-206">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e53a0-206">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

