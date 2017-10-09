---
title: aaaManage Azure oplossingen met PowerShell | Microsoft Docs
description: Gebruik Azure PowerShell en Resource Manager toomanage uw resources.
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
ms.openlocfilehash: 47a91af8d7eb59585bcfd43571ce76b90a0d7971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-with-azure-powershell-and-resource-manager"></a><span data-ttu-id="22703-103">Resources beheren met Azure PowerShell en Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22703-103">Manage resources with Azure PowerShell and Resource Manager</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="22703-104">Portal</span><span class="sxs-lookup"><span data-stu-id="22703-104">Portal</span></span>](resource-group-portal.md)
> * [<span data-ttu-id="22703-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="22703-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="22703-106">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="22703-106">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="22703-107">REST API</span><span class="sxs-lookup"><span data-stu-id="22703-107">REST API</span></span>](resource-manager-rest-api.md)
>
>

<span data-ttu-id="22703-108">In dit artikel leert u hoe toomanage uw oplossingen met Azure PowerShell en Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22703-108">In this article, you learn how toomanage your solutions with Azure PowerShell and Azure Resource Manager.</span></span> <span data-ttu-id="22703-109">Als u niet bekend met Resource Manager, Zie [overzicht van Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="22703-109">If you are not familiar with Resource Manager, see [Resource Manager Overview](resource-group-overview.md).</span></span> <span data-ttu-id="22703-110">Dit onderwerp richt zich op beheertaken.</span><span class="sxs-lookup"><span data-stu-id="22703-110">This topic focuses on management tasks.</span></span> <span data-ttu-id="22703-111">U gaat het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="22703-111">You will:</span></span>

1. <span data-ttu-id="22703-112">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="22703-112">Create a resource group</span></span>
2. <span data-ttu-id="22703-113">Een resourcegroep voor resource toohello toevoegen</span><span class="sxs-lookup"><span data-stu-id="22703-113">Add a resource toohello resource group</span></span>
3. <span data-ttu-id="22703-114">Een label toohello resource toevoegen</span><span class="sxs-lookup"><span data-stu-id="22703-114">Add a tag toohello resource</span></span>
4. <span data-ttu-id="22703-115">Een query uitvoeren op basis van namen of labelwaarden resources</span><span class="sxs-lookup"><span data-stu-id="22703-115">Query resources based on names or tag values</span></span>
5. <span data-ttu-id="22703-116">Toepassen en verwijderen van een vergrendeling op Hallo resource</span><span class="sxs-lookup"><span data-stu-id="22703-116">Apply and remove a lock on hello resource</span></span>
6. <span data-ttu-id="22703-117">Verwijderen van een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="22703-117">Delete a resource group</span></span>

<span data-ttu-id="22703-118">In dit artikel wordt niet weergegeven hoe toodeploy een Resource Manager sjabloon tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="22703-118">This article does not show how toodeploy a Resource Manager template tooyour subscription.</span></span> <span data-ttu-id="22703-119">Zie voor die informatie [implementeren van resources met Resource Manager-sjablonen en Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="22703-119">For that information, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>

## <a name="get-started-with-azure-powershell"></a><span data-ttu-id="22703-120">Aan de slag met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="22703-120">Get started with Azure PowerShell</span></span>

<span data-ttu-id="22703-121">Als u Azure PowerShell nog niet hebt geïnstalleerd, raadpleegt u [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="22703-121">If you have not installed Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="22703-122">Als u Azure PowerShell hebt geïnstalleerd in de afgelopen hello, maar hebben niet het onlangs bijgewerkt, Overweeg de installatie van de meest recente versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="22703-122">If you have installed Azure PowerShell in hello past but have not updated it recently, consider installing hello latest version.</span></span> <span data-ttu-id="22703-123">U kunt bijwerken Hallo-versie via Hallo dezelfde manier waarop u tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="22703-123">You can update hello version through hello same method you used tooinstall it.</span></span> <span data-ttu-id="22703-124">Als u Hallo Web Platform Installer gebruikt, bijvoorbeeld opnieuw te starten en zoekt u een update.</span><span class="sxs-lookup"><span data-stu-id="22703-124">For example, if you used hello Web Platform Installer, launch it again and look for an update.</span></span>

<span data-ttu-id="22703-125">uw versie van hello Azure-Resources-module, gebruikt u toocheck Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="22703-125">toocheck your version of hello Azure Resources module, use hello following cmdlet:</span></span>

```powershell
Get-Module -ListAvailable -Name AzureRm.Resources | Select Version
```

<span data-ttu-id="22703-126">In dit onderwerp is bijgewerkt voor versie 3.3.0.</span><span class="sxs-lookup"><span data-stu-id="22703-126">This topic was updated for version 3.3.0.</span></span> <span data-ttu-id="22703-127">Als u een eerdere versie hebt, uw ervaring mogelijk niet overeen met Hallo stappen in dit onderwerp.</span><span class="sxs-lookup"><span data-stu-id="22703-127">If you have an earlier version, your experience might not match hello steps shown in this topic.</span></span> <span data-ttu-id="22703-128">Zie voor documentatie over cmdlets in deze versie Hallo [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span><span class="sxs-lookup"><span data-stu-id="22703-128">For documentation about hello cmdlets in this version, see [AzureRM.Resources Module](/powershell/module/azurerm.resources).</span></span>

## <a name="log-in-tooyour-azure-account"></a><span data-ttu-id="22703-129">Meld u bij tooyour Azure-account</span><span class="sxs-lookup"><span data-stu-id="22703-129">Log in tooyour Azure account</span></span>
<span data-ttu-id="22703-130">Voordat u aan uw oplossing werkt, moet u tooyour account aanmelden.</span><span class="sxs-lookup"><span data-stu-id="22703-130">Before working on your solution, you must log in tooyour account.</span></span>

<span data-ttu-id="22703-131">toolog in tooyour Azure-account gebruiken Hallo **Login-AzureRmAccount** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22703-131">toolog in tooyour Azure account, use hello **Login-AzureRmAccount** cmdlet.</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="22703-132">Hallo-cmdlet wordt u gevraagd om de aanmeldingsreferenties Hallo voor uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="22703-132">hello cmdlet prompts you for hello login credentials for your Azure account.</span></span> <span data-ttu-id="22703-133">Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22703-133">After logging in, it downloads your account settings so they are available tooAzure PowerShell.</span></span>

<span data-ttu-id="22703-134">Hallo cmdlet retourneert informatie over uw account en Hallo abonnement toouse voor Hallo taken.</span><span class="sxs-lookup"><span data-stu-id="22703-134">hello cmdlet returns information about your account and hello subscription toouse for hello tasks.</span></span>

```powershell
Environment           : AzureCloud
Account               : example@contoso.com
TenantId              : {guid}
SubscriptionId        : {guid}
SubscriptionName      : Example Subscription One
CurrentStorageAccount :

```

<span data-ttu-id="22703-135">Als u meer dan één abonnement hebt, kunt u een ander abonnement tooa overschakelen.</span><span class="sxs-lookup"><span data-stu-id="22703-135">If you have more than one subscription, you can switch tooa different subscription.</span></span> <span data-ttu-id="22703-136">Eerst gaan we kijken alle Hallo abonnementen voor uw account.</span><span class="sxs-lookup"><span data-stu-id="22703-136">First, let's see all hello subscriptions for your account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="22703-137">Het resultaat van ingeschakelde en uitgeschakelde abonnementen.</span><span class="sxs-lookup"><span data-stu-id="22703-137">It returns enabled and disabled subscriptions.</span></span>

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

<span data-ttu-id="22703-138">tooswitch tooa ander abonnement, de naam van een abonnement Hallo voorzien van Hallo **Set-AzureRmContext** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22703-138">tooswitch tooa different subscription, provide hello subscription name with hello **Set-AzureRmContext** cmdlet.</span></span>

```powershell
Set-AzureRmContext -SubscriptionName "Example Subscription Two"
```

## <a name="create-a-resource-group"></a><span data-ttu-id="22703-139">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="22703-139">Create a resource group</span></span>
<span data-ttu-id="22703-140">Voordat u een abonnement van resources tooyour implementeert, moet u een resourcegroep die Hallo resources bevat.</span><span class="sxs-lookup"><span data-stu-id="22703-140">Before deploying any resources tooyour subscription, you must create a resource group that will contain hello resources.</span></span>

<span data-ttu-id="22703-141">een resourcegroep toocreate gebruiken Hallo **New-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22703-141">toocreate a resource group, use hello **New-AzureRmResourceGroup** cmdlet.</span></span> <span data-ttu-id="22703-142">Hallo-opdracht gebruikt Hallo **naam** parameter toospecify een naam voor de resourcegroep Hallo en Hallo **locatie** parameter toospecify de locatie.</span><span class="sxs-lookup"><span data-stu-id="22703-142">hello command uses hello **Name** parameter toospecify a name for hello resource group and hello **Location** parameter toospecify its location.</span></span>

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location "South Central US"
```

<span data-ttu-id="22703-143">Hallo-uitvoer is in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="22703-143">hello output is in hello following format:</span></span>

```powershell
ResourceGroupName : TestRG1
Location          : southcentralus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/{guid}/resourceGroups/TestRG1
```

<span data-ttu-id="22703-144">Als u later nodig tooretrieve Hallo resourcegroep hebt, gebruikt u Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="22703-144">If you need tooretrieve hello resource group later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName TestRG1
```

<span data-ttu-id="22703-145">tooget alle resourcegroepen in uw abonnement Hallo, geen naam opgeeft:</span><span class="sxs-lookup"><span data-stu-id="22703-145">tooget all hello resource groups in your subscription, do not specify a name:</span></span>

```powershell
Get-AzureRmResourceGroup
```

## <a name="add-resources-tooa-resource-group"></a><span data-ttu-id="22703-146">Toevoegen van bronnen tooa resourcegroep</span><span class="sxs-lookup"><span data-stu-id="22703-146">Add resources tooa resource group</span></span>
<span data-ttu-id="22703-147">een resourcegroep voor resource toohello tooadd, kunt u Hallo **nieuw AzureRmResource** cmdlet of een cmdlet die specifieke toohello type resource dat u wilt maken (zoals **nieuw AzureRmStorageAccount**).</span><span class="sxs-lookup"><span data-stu-id="22703-147">tooadd a resource toohello resource group, you can use hello **New-AzureRmResource** cmdlet or a cmdlet that is specific toohello type of resource you are creating (like **New-AzureRmStorageAccount**).</span></span> <span data-ttu-id="22703-148">U vindt het misschien gemakkelijker toouse een cmdlet die specifieke tooa brontype is omdat deze parameters op voor het Hallo-eigenschappen die nodig zijn voor de nieuwe resource Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="22703-148">You might find it easier toouse a cmdlet that is specific tooa resource type because it includes parameters for hello properties that are needed for hello new resource.</span></span> <span data-ttu-id="22703-149">toouse **nieuw AzureRmResource**, moet u alle Hallo eigenschappen tooset zonder te worden gevraagd ze weten.</span><span class="sxs-lookup"><span data-stu-id="22703-149">toouse **New-AzureRmResource**, you must know all hello properties tooset without being prompted for them.</span></span>

<span data-ttu-id="22703-150">Echter, het toevoegen van een resource via cmdlets kan veroorzaken toekomstige verwarring omdat Hallo nieuwe resource niet in een Resource Manager-sjabloon bestaat.</span><span class="sxs-lookup"><span data-stu-id="22703-150">However, adding a resource through cmdlets might cause future confusion because hello new resource does not exist in a Resource Manager template.</span></span> <span data-ttu-id="22703-151">Microsoft raadt het Hallo-infrastructuur voor uw Azure oplossing definiëren in een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="22703-151">Microsoft recommends defining hello infrastructure for your Azure solution in a Resource Manager template.</span></span> <span data-ttu-id="22703-152">Sjablonen kunnen u tooreliably en uw oplossing herhaaldelijk implementeren.</span><span class="sxs-lookup"><span data-stu-id="22703-152">Templates enable you tooreliably and repeatedly deploy your solution.</span></span> <span data-ttu-id="22703-153">Voor dit onderwerp, hebt u een opslagaccount met een PowerShell-cmdlet, maar later het genereren van een sjabloon uit de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="22703-153">For this topic, you create a storage account with a PowerShell cmdlet, but later you generate a template from your resource group.</span></span>

<span data-ttu-id="22703-154">Hallo volgende cmdlet maakt een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="22703-154">hello following cmdlet creates a storage account.</span></span> <span data-ttu-id="22703-155">In plaats van Hallo-naam wordt weergegeven in voorbeeld hello, Geef een unieke naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="22703-155">Instead of using hello name shown in hello example, provide a unique name for hello storage account.</span></span> <span data-ttu-id="22703-156">Hallo naam moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="22703-156">hello name must be between 3 and 24 characters in length, and use only numbers and lower-case letters.</span></span> <span data-ttu-id="22703-157">Als u Hallo-naam wordt weergegeven in Hallo-voorbeeld gebruikt, ontvangt u een fout opgetreden omdat deze naam al gebruikt wordt.</span><span class="sxs-lookup"><span data-stu-id="22703-157">If you use hello name shown in hello example, you receive an error because that name is already in use.</span></span>

```powershell
New-AzureRmStorageAccount -ResourceGroupName TestRG1 -AccountName mystoragename -Type "Standard_LRS" -Location "South Central US"
```

<span data-ttu-id="22703-158">Als u later nodig tooretrieve deze bron hebt, gebruikt u Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="22703-158">If you need tooretrieve this resource later, use hello following cmdlet:</span></span>

```powershell
Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1
```

## <a name="add-a-tag"></a><span data-ttu-id="22703-159">Een label toevoegen</span><span class="sxs-lookup"><span data-stu-id="22703-159">Add a tag</span></span>

<span data-ttu-id="22703-160">Labels kunnen u tooorganize uw resources op basis van toodifferent eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="22703-160">Tags enable you tooorganize your resources according toodifferent properties.</span></span> <span data-ttu-id="22703-161">Bijvoorbeeld wellicht hebt u verschillende resources in verschillende resourcegroepen die deel uitmaken van toohello dezelfde afdeling.</span><span class="sxs-lookup"><span data-stu-id="22703-161">For example, you may have several resources in different resource groups that belong toohello same department.</span></span> <span data-ttu-id="22703-162">U kunt een afdeling tag en waarde toothose resources toomark toepassen als toohello uitmaken van dezelfde categorie.</span><span class="sxs-lookup"><span data-stu-id="22703-162">You can apply a department tag and value toothose resources toomark them as belonging toohello same category.</span></span> <span data-ttu-id="22703-163">Of u kunt markeren of een resource wordt gebruikt in een productie- of testomgeving.</span><span class="sxs-lookup"><span data-stu-id="22703-163">Or, you can mark whether a resource is used in a production or test environment.</span></span> <span data-ttu-id="22703-164">In dit onderwerp leert u labels tooonly één resource toepassen, maar in uw omgeving is het meest waarschijnlijke zinvol tooapply tags tooall uw resources.</span><span class="sxs-lookup"><span data-stu-id="22703-164">In this topic, you apply tags tooonly one resource, but in your environment it most likely makes sense tooapply tags tooall your resources.</span></span>

<span data-ttu-id="22703-165">Hallo cmdlet na geldt twee labels tooyour storage-account:</span><span class="sxs-lookup"><span data-stu-id="22703-165">hello following cmdlet applies two tags tooyour storage account:</span></span>

```powershell
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test" } -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
 ```

<span data-ttu-id="22703-166">Labels zijn als een enkel object bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="22703-166">Tags are updated as a single object.</span></span> <span data-ttu-id="22703-167">tooadd een tag tooa bron die reeds labels bevat, worden eerst Hallo bestaande labels opgehaald.</span><span class="sxs-lookup"><span data-stu-id="22703-167">tooadd a tag tooa resource that already includes tags, first retrieve hello existing tags.</span></span> <span data-ttu-id="22703-168">Hallo nieuwe tag toohello-object met bestaande Hallo-tags toevoegen en alle Hallo labels toohello resource pas.</span><span class="sxs-lookup"><span data-stu-id="22703-168">Add hello new tag toohello object that contains hello existing tags, and reapply all hello tags toohello resource.</span></span>

```powershell
$tags = (Get-AzureRmResource -ResourceName mystoragename -ResourceGroupName TestRG1).Tags
$tags += @{Status="Approved"}
Set-AzureRmResource -Tag $tags -ResourceName mystoragename -ResourceGroupName TestRG1 -ResourceType Microsoft.Storage/storageAccounts
```

## <a name="search-for-resources"></a><span data-ttu-id="22703-169">Zoeken naar resources</span><span class="sxs-lookup"><span data-stu-id="22703-169">Search for resources</span></span>

<span data-ttu-id="22703-170">Gebruik Hallo **zoeken AzureRmResource** cmdlet tooretrieve bronnen voor verschillende zoekcriteria.</span><span class="sxs-lookup"><span data-stu-id="22703-170">Use hello **Find-AzureRmResource** cmdlet tooretrieve resources for different search conditions.</span></span>

* <span data-ttu-id="22703-171">een resource met de naam, tooget bieden Hallo **ResourceNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="22703-171">tooget a resource by name, provide hello **ResourceNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceNameContains mystoragename
  ```

* <span data-ttu-id="22703-172">tooget alle Hallo resources in een resourcegroep bieden Hallo **ResourceGroupNameContains** parameter:</span><span class="sxs-lookup"><span data-stu-id="22703-172">tooget all hello resources in a resource group, provide hello **ResourceGroupNameContains** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceGroupNameContains TestRG1
  ```

* <span data-ttu-id="22703-173">tooget alle Hallo resources met een naam en waarde, bieden Hallo **TagName** en **TagValue** parameters:</span><span class="sxs-lookup"><span data-stu-id="22703-173">tooget all hello resources with a tag name and value, provide hello **TagName** and **TagValue** parameters:</span></span>

  ```powershell
  Find-AzureRmResource -TagName Dept -TagValue IT
  ```

* <span data-ttu-id="22703-174">tooall hello resources met een bepaald brontype bieden Hallo **ResourceType** parameter:</span><span class="sxs-lookup"><span data-stu-id="22703-174">tooall hello resources with a particular resource type, provide hello **ResourceType** parameter:</span></span>

  ```powershell
  Find-AzureRmResource -ResourceType Microsoft.Storage/storageAccounts
  ```

## <a name="lock-a-resource"></a><span data-ttu-id="22703-175">Vergrendelen van een resource</span><span class="sxs-lookup"><span data-stu-id="22703-175">Lock a resource</span></span>

<span data-ttu-id="22703-176">Wanneer u ervoor dat een essentiële resource niet per ongeluk is verwijderd of gewijzigd toomake moet, van toepassing een vergrendeling toohello resource.</span><span class="sxs-lookup"><span data-stu-id="22703-176">When you need toomake sure a critical resource is not accidentally deleted or modified, apply a lock toohello resource.</span></span> <span data-ttu-id="22703-177">U kunt opgeven dat ofwel een **CanNotDelete** of **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="22703-177">You can specify either a **CanNotDelete** or **ReadOnly**.</span></span>

<span data-ttu-id="22703-178">management-vergrendelingen toocreate of verwijderen, moet u beschikken te`Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties.</span><span class="sxs-lookup"><span data-stu-id="22703-178">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="22703-179">Van de ingebouwde rollen hello, worden alleen de eigenaar en de beheerder voor gebruikerstoegang die acties verleend.</span><span class="sxs-lookup"><span data-stu-id="22703-179">Of hello built-in roles, only Owner and User Access Administrator are granted those actions.</span></span>

<span data-ttu-id="22703-180">een vergrendeling tooapply gebruik Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="22703-180">tooapply a lock, use hello following cmdlet:</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="22703-181">worden Hallo vergrendelde bron in het voorgaande voorbeeld Hallo kan niet verwijderd totdat Hallo vergrendeling wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="22703-181">hello locked resource in hello preceding example cannot be deleted until hello lock is removed.</span></span> <span data-ttu-id="22703-182">een vergrendeling tooremove gebruiken:</span><span class="sxs-lookup"><span data-stu-id="22703-182">tooremove a lock, use:</span></span>

```powershell
Remove-AzureRmResourceLock -LockName LockStorage -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
```

<span data-ttu-id="22703-183">Zie voor meer informatie over de instelling vergrendelingen [resources met Azure Resource Manager vergrendelen](resource-group-lock-resources.md).</span><span class="sxs-lookup"><span data-stu-id="22703-183">For more information about setting locks, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="remove-resources-or-resource-group"></a><span data-ttu-id="22703-184">Verwijder resources of resourcegroep</span><span class="sxs-lookup"><span data-stu-id="22703-184">Remove resources or resource group</span></span>
<span data-ttu-id="22703-185">U kunt een resource of resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="22703-185">You can remove a resource or resource group.</span></span> <span data-ttu-id="22703-186">Wanneer u een resourcegroep verwijdert, verwijdert u ook alle Hallo resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="22703-186">When you remove a resource group, you also remove all hello resources within that resource group.</span></span>

* <span data-ttu-id="22703-187">een bron van de resourcegroep hello, gebruik Hallo toodelete **verwijderen AzureRmResource** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22703-187">toodelete a resource from hello resource group, use hello **Remove-AzureRmResource** cmdlet.</span></span> <span data-ttu-id="22703-188">Deze cmdlet Hallo resource wordt verwijderd, maar biedt niet Hallo resourcegroep verwijderen.</span><span class="sxs-lookup"><span data-stu-id="22703-188">This cmdlet deletes hello resource, but does not delete hello resource group.</span></span>

  ```powershell
  Remove-AzureRmResource -ResourceName mystoragename -ResourceType Microsoft.Storage/storageAccounts -ResourceGroupName TestRG1
  ```

* <span data-ttu-id="22703-189">toodelete een resourcegroep en alle bijbehorende resources gebruiken Hallo **Remove-AzureRmResourceGroup** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="22703-189">toodelete a resource group and all its resources, use hello **Remove-AzureRmResourceGroup** cmdlet.</span></span>

  ```powershell
  Remove-AzureRmResourceGroup -Name TestRG1
  ```

<span data-ttu-id="22703-190">Voor beide cmdlets, wordt u gevraagd tooconfirm dat u tooremove Hallo resource of resourcegroep wenst.</span><span class="sxs-lookup"><span data-stu-id="22703-190">For both cmdlets, you are asked tooconfirm that you wish tooremove hello resource or resource group.</span></span> <span data-ttu-id="22703-191">Als wordt Hallo bewerking Hallo resource of resourcegroep is verwijderd, retourneert **True**.</span><span class="sxs-lookup"><span data-stu-id="22703-191">If hello operation successfully deletes hello resource or resource group, it returns **True**.</span></span>

## <a name="run-resource-manager-scripts-with-azure-automation"></a><span data-ttu-id="22703-192">Resource Manager-scripts uitvoeren met Azure Automation</span><span class="sxs-lookup"><span data-stu-id="22703-192">Run Resource Manager scripts with Azure Automation</span></span>

<span data-ttu-id="22703-193">Dit onderwerp leest u hoe tooperform basisbewerkingen op uw resources met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22703-193">This topic shows you how tooperform basic operations on your resources with Azure PowerShell.</span></span> <span data-ttu-id="22703-194">Voor meer geavanceerde scenario's voor beheer, u doorgaans wilt toocreate een script en script opnieuw naar behoefte of volgens een schema.</span><span class="sxs-lookup"><span data-stu-id="22703-194">For more advanced management scenarios, you typically want toocreate a script, and reuse that script as needed or on a schedule.</span></span> <span data-ttu-id="22703-195">[Azure Automation](../automation/automation-intro.md) biedt een manier voor u tooautomate veelgebruikte scripts waarmee uw Azure-oplossingen kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="22703-195">[Azure Automation](../automation/automation-intro.md) provides a way for you tooautomate frequently used scripts that manage your Azure solutions.</span></span>

<span data-ttu-id="22703-196">Hallo volgende onderwerpen bevatten informatie over hoe toouse Azure Automation, Resource Manager en PowerShell tooeffectively beheertaken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="22703-196">hello following topics show you how toouse Azure Automation, Resource Manager, and PowerShell tooeffectively perform management tasks:</span></span>

- <span data-ttu-id="22703-197">Zie voor meer informatie over het maken van een runbook [Mijn eerste PowerShell-runbook](../automation/automation-first-runbook-textual-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="22703-197">For information about creating a runbook, see [My first PowerShell runbook](../automation/automation-first-runbook-textual-powershell.md).</span></span>
- <span data-ttu-id="22703-198">Zie voor meer informatie over het werken met galerieën scripts [galerieën Runbook en de module voor Azure Automation](../automation/automation-runbook-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="22703-198">For information about working with galleries of scripts, see [Runbook and module galleries for Azure Automation](../automation/automation-runbook-gallery.md).</span></span>
- <span data-ttu-id="22703-199">Zie voor runbooks die starten en stoppen van virtuele machines, [Azure Automation-scenario: labels met behulp van JSON-indeling toocreate een planning voor de virtuele machine van Azure opstarten en afsluiten](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span><span class="sxs-lookup"><span data-stu-id="22703-199">For runbooks that start and stop virtual machines, see [Azure Automation scenario: Using JSON-formatted tags toocreate a schedule for Azure VM startup and shutdown](../automation/automation-scenario-start-stop-vm-wjson-tags.md).</span></span>
- <span data-ttu-id="22703-200">Zie voor runbooks die starten en stoppen van virtuele machines rustige uren, [starten/stoppen virtuele machines tijdens rustige uren oplossing in Automation](../automation/automation-solution-vm-management.md).</span><span class="sxs-lookup"><span data-stu-id="22703-200">For runbooks that start and stop virtual machines off-hours, see [Start/Stop VMs during off-hours solution in Automation](../automation/automation-solution-vm-management.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="22703-201">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22703-201">Next steps</span></span>
* <span data-ttu-id="22703-202">toolearn over het maken van Resource Manager-sjablonen, Zie [Azure Resource Manager-sjablonen ontwerpen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="22703-202">toolearn about creating Resource Manager templates, see [Authoring Azure Resource Manager Templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="22703-203">toolearn over het implementeren van sjablonen, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="22703-203">toolearn about deploying templates, see [Deploy an application with Azure Resource Manager Template](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="22703-204">U kunt bestaande resources tooa nieuwe resourcegroep verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="22703-204">You can move existing resources tooa new resource group.</span></span> <span data-ttu-id="22703-205">Zie voor voorbeelden [verplaatsen van Resources tooNew resourcegroep of abonnement](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="22703-205">For examples, see [Move Resources tooNew Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="22703-206">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="22703-206">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

