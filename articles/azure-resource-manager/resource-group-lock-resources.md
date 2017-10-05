---
title: Azure-resources om te voorkomen dat wijzigingen vergrendelen | Microsoft Docs
description: "Voorkomen dat gebruikers bijwerken of verwijderen van essentiële Azure-resources door het toepassen van een vergrendeling voor alle gebruikers en rollen."
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: tomfitz
ms.openlocfilehash: 44c87b00f4fc63dbfd45a07d9a8cddc5eaf1a65c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="aca3d-103">Resources om te voorkomen dat onverwachte wijzigingen vergrendelen</span><span class="sxs-lookup"><span data-stu-id="aca3d-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="aca3d-104">Als beheerder, moet u wellicht een abonnement, resourcegroep of resource om te voorkomen dat andere gebruikers in uw organisatie per ongeluk verwijderen of wijzigen van kritieke bronnen vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="aca3d-105">U kunt de vergrendeling op instellen **CanNotDelete** of **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="aca3d-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="aca3d-106">**CanNotDelete** betekent geautoriseerde gebruikers kunnen nog steeds lezen en wijzigen van een resource, maar de resource kan niet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="aca3d-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="aca3d-107">**Alleen-lezen** betekent geautoriseerde gebruikers kunnen een resource lezen, maar ze niet verwijderen of bijwerken van de resource.</span><span class="sxs-lookup"><span data-stu-id="aca3d-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="aca3d-108">Toepassen van deze vergrendeling is vergelijkbaar met alle gemachtigde gebruikers beperken tot de machtigingen verleend door de **lezer** rol.</span><span class="sxs-lookup"><span data-stu-id="aca3d-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="aca3d-109">Hoe vergrendelingen worden toegepast</span><span class="sxs-lookup"><span data-stu-id="aca3d-109">How locks are applied</span></span>

<span data-ttu-id="aca3d-110">Wanneer u een vergrendeling op een bovenliggend bereik toepast, nemen alle resources binnen dat bereik de dezelfde vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="aca3d-110">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="aca3d-111">Zelfs resources die u later toevoegen overnemen de vergrendeling van het bovenliggende item.</span><span class="sxs-lookup"><span data-stu-id="aca3d-111">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="aca3d-112">De meest beperkende vergrendeling in de overname voorrang.</span><span class="sxs-lookup"><span data-stu-id="aca3d-112">The most restrictive lock in the inheritance takes precedence.</span></span>

<span data-ttu-id="aca3d-113">In tegenstelling tot rollen gebaseerd toegangsbeheer kunt u management vergrendelingen toepassen van een beperking voor alle gebruikers en rollen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-113">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="aca3d-114">Zie voor meer informatie over het instellen van machtigingen voor gebruikers en rollen [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="aca3d-114">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="aca3d-115">Vergrendelingen van Resource Manager alleen van toepassing op bewerkingen die in de vlak management, die uit de bewerkingen die worden verzonden optreden bestaat naar `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aca3d-115">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="aca3d-116">De vergrendelingen beperken niet hoe resources hun eigen functies uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="aca3d-116">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="aca3d-117">Wijzigingen in de resourcedefinitie zijn beperkt, maar de bewerkingen van resources zijn niet beperkt.</span><span class="sxs-lookup"><span data-stu-id="aca3d-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="aca3d-118">Bijvoorbeeld, een vergrendeling van het kenmerk alleen-lezen voor een SQL-Database wordt voorkomen dat u de database wijzigen of verwijderen, maar dit voorkomt niet dat u maken, bijwerken of verwijderen van gegevens in de database.</span><span class="sxs-lookup"><span data-stu-id="aca3d-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="aca3d-119">Gegevenstransacties worden toegestaan, omdat deze bewerkingen niet worden verzonden naar `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="aca3d-119">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="aca3d-120">Toepassen van **ReadOnly** kan leiden tot onverwachte resultaten optreden omdat bepaalde bewerkingen die lijkt lezen bewerkingen daadwerkelijk extra acties vereist.</span><span class="sxs-lookup"><span data-stu-id="aca3d-120">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="aca3d-121">Bijvoorbeeld, als een **ReadOnly** vergrendeling van een opslagaccount wordt voorkomen dat alle gebruikers weergeven van de sleutels.</span><span class="sxs-lookup"><span data-stu-id="aca3d-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="aca3d-122">De lijst met sleutels opnieuw wordt verwerkt door een POST-aanvraag omdat de geretourneerde sleutels zijn beschikbaar voor schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-122">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="aca3d-123">Voor een ander voorbeeld plaatsen van een **ReadOnly** vergrendelen op een App Service-bron wordt voorkomen dat Visual Studio Server Explorer-bestanden voor de resource worden weergegeven omdat die interactie voor toegang voor schrijven vereist.</span><span class="sxs-lookup"><span data-stu-id="aca3d-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="aca3d-124">Wie kunt maken of verwijderen van vergrendelingen in uw organisatie</span><span class="sxs-lookup"><span data-stu-id="aca3d-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="aca3d-125">Als u wilt maken of verwijderen van management vergrendelingen, u moet toegang hebben tot `Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties.</span><span class="sxs-lookup"><span data-stu-id="aca3d-125">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="aca3d-126">Van de ingebouwde rollen alleen **eigenaar** en **beheerder voor gebruikerstoegang** deze acties worden verleend.</span><span class="sxs-lookup"><span data-stu-id="aca3d-126">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="aca3d-127">Portal</span><span class="sxs-lookup"><span data-stu-id="aca3d-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="aca3d-128">Template</span><span class="sxs-lookup"><span data-stu-id="aca3d-128">Template</span></span>
<span data-ttu-id="aca3d-129">Het volgende voorbeeld ziet een sjabloon die wordt gemaakt van een vergrendeling op een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="aca3d-129">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="aca3d-130">Het opslagaccount op waarop u wilt toepassen van de vergrendeling is opgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="aca3d-130">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="aca3d-131">De naam van de vergrendeling wordt gemaakt door de naam van de resource met cookievalidatie **/Microsoft.Authorization/** en de naam van de vergrendeling, in dit geval **myLock**.</span><span class="sxs-lookup"><span data-stu-id="aca3d-131">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="aca3d-132">Het opgegeven type is specifiek voor het brontype.</span><span class="sxs-lookup"><span data-stu-id="aca3d-132">The type provided is specific to the resource type.</span></span> <span data-ttu-id="aca3d-133">Voor opslag, stelt u het type 'Microsoft.Storage/storageaccounts/providers/locks'.</span><span class="sxs-lookup"><span data-stu-id="aca3d-133">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="powershell"></a><span data-ttu-id="aca3d-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="aca3d-134">PowerShell</span></span>
<span data-ttu-id="aca3d-135">U vergrendeling resources met Azure PowerShell geïmplementeerd met behulp van de [nieuw AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) opdracht.</span><span class="sxs-lookup"><span data-stu-id="aca3d-135">You lock deployed resources with Azure PowerShell by using the [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="aca3d-136">Als u wilt vergrendelen van een resource, geef de naam van de bron, het resourcetype en de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="aca3d-136">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="aca3d-137">Als u wilt vergrendelen van een resourcegroep, geef de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="aca3d-137">To lock a resource group, provide the name of the resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="aca3d-138">Als u informatie over een vergrendeling, gebruikt [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="aca3d-138">To get information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="aca3d-139">Als u alle vergrendelingen in uw abonnement, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-139">To get all the locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="aca3d-140">Als u alle vergrendelingen voor een resource, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-140">To get all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="aca3d-141">Als u alle vergrendelingen voor een resourcegroep, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-141">To get all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="aca3d-142">Azure PowerShell biedt andere opdrachten voor vergrendelingen werken, zoals [Set AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) bijwerken van een vergrendeling en [verwijderen AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) een vergrendeling te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) to update a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) to delete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="aca3d-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="aca3d-143">Azure CLI</span></span>

<span data-ttu-id="aca3d-144">U vergrendeling resources met Azure CLI geïmplementeerd met behulp van de [az vergrendeling maken](/cli/azure/lock#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="aca3d-144">You lock deployed resources with Azure CLI by using the [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="aca3d-145">Als u wilt vergrendelen van een resource, geef de naam van de bron, het resourcetype en de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="aca3d-145">To lock a resource, provide the name of the resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="aca3d-146">Als u wilt vergrendelen van een resourcegroep, geef de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="aca3d-146">To lock a resource group, provide the name of the resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="aca3d-147">Als u informatie over een vergrendeling, gebruikt [az vergrendeling lijst](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="aca3d-147">To get information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="aca3d-148">Als u alle vergrendelingen in uw abonnement, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-148">To get all the locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="aca3d-149">Als u alle vergrendelingen voor een resource, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-149">To get all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="aca3d-150">Als u alle vergrendelingen voor een resourcegroep, gebruikt u:</span><span class="sxs-lookup"><span data-stu-id="aca3d-150">To get all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="aca3d-151">Azure CLI biedt andere opdrachten voor vergrendelingen werken, zoals [az vergrendeling update](/cli/azure/lock#update) bijwerken van een vergrendeling en [az vergrendeling verwijderen](/cli/azure/lock#delete) een vergrendeling te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) to update a lock, and [az lock delete](/cli/azure/lock#delete) to delete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="aca3d-152">REST API</span><span class="sxs-lookup"><span data-stu-id="aca3d-152">REST API</span></span>
<span data-ttu-id="aca3d-153">U kunt vergrendelen geïmplementeerde resources met de [REST-API voor beheer van vergrendelingen](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="aca3d-153">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="aca3d-154">De REST-API kunt u maken en verwijderen van vergrendelingen en informatie ophalen over bestaande vergrendelingen.</span><span class="sxs-lookup"><span data-stu-id="aca3d-154">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="aca3d-155">Voer voor het maken van een vergrendeling:</span><span class="sxs-lookup"><span data-stu-id="aca3d-155">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="aca3d-156">Het bereik kan worden voor een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="aca3d-156">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="aca3d-157">De naam van de vergrendeling is wat u wilt aanroepen van de vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="aca3d-157">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="aca3d-158">Gebruik voor de api-versie **01-01-2015**.</span><span class="sxs-lookup"><span data-stu-id="aca3d-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="aca3d-159">Opnemen in de aanvraag een JSON-object waarmee de eigenschappen voor de vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="aca3d-159">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="aca3d-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aca3d-160">Next steps</span></span>
* <span data-ttu-id="aca3d-161">Zie voor meer informatie over het werken met resource vergrendelingen [vergrendeling omlaag Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="aca3d-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="aca3d-162">Zie voor meer informatie over het logisch ordenen van uw resources [met labels om uw resources te organiseren](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="aca3d-162">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="aca3d-163">Als u wilt wijzigen welke resourcegroep een resource bevindt zich in, Zie [resources verplaatsen naar een nieuwe resourcegroep](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="aca3d-163">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="aca3d-164">U kunt beperkingen en conventies toepassen voor uw abonnement met aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="aca3d-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="aca3d-165">Zie voor meer informatie [Beleid gebruiken voor het beheren van resources en toegang](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="aca3d-165">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="aca3d-166">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="aca3d-166">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

