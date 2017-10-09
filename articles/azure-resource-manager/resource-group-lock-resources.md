---
title: aaaLock Azure-resources tooprevent wijzigingen | Microsoft Docs
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
ms.openlocfilehash: 1f0d8911b2b129069bd2f01a9a4ec0a3cf700118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="lock-resources-tooprevent-unexpected-changes"></a><span data-ttu-id="66941-103">Vergrendelen van resources tooprevent onverwachte wijzigingen</span><span class="sxs-lookup"><span data-stu-id="66941-103">Lock resources tooprevent unexpected changes</span></span> 
<span data-ttu-id="66941-104">Als beheerder moet u mogelijk toolock een abonnement, resourcegroep of resource tooprevent andere gebruikers in uw organisatie per ongeluk worden kritieke bronnen wijzigen of verwijderen.</span><span class="sxs-lookup"><span data-stu-id="66941-104">As an administrator, you may need toolock a subscription, resource group, or resource tooprevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="66941-105">U kunt instellen Hallo vergrendeling te**CanNotDelete** of **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="66941-105">You can set hello lock level too**CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="66941-106">**CanNotDelete** betekent geautoriseerde gebruikers kunnen nog steeds lezen en wijzigen van een resource, maar ze Hallo resource niet verwijderen.</span><span class="sxs-lookup"><span data-stu-id="66941-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete hello resource.</span></span> 
* <span data-ttu-id="66941-107">**Alleen-lezen** betekent geautoriseerde gebruikers kunnen een resource lezen, maar ze niet verwijderen of bijwerken van de bron Hallo.</span><span class="sxs-lookup"><span data-stu-id="66941-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update hello resource.</span></span> <span data-ttu-id="66941-108">Vergelijkbare toorestricting alle gebruikers toohello machtigingen verleend door Hallo geautoriseerd voor het toepassen van deze vergrendeling is **lezer** rol.</span><span class="sxs-lookup"><span data-stu-id="66941-108">Applying this lock is similar toorestricting all authorized users toohello permissions granted by hello **Reader** role.</span></span> 

## <a name="how-locks-are-applied"></a><span data-ttu-id="66941-109">Hoe vergrendelingen worden toegepast</span><span class="sxs-lookup"><span data-stu-id="66941-109">How locks are applied</span></span>

<span data-ttu-id="66941-110">Wanneer u een vergrendeling op een bovenliggend bereik toepast, alle resources binnen dat bereik Hallo overnemen dezelfde vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="66941-110">When you apply a lock at a parent scope, all resources within that scope inherit hello same lock.</span></span> <span data-ttu-id="66941-111">Hallo vergrendeling overnemen zelfs resources die u later toevoegen van bovenliggende Hallo.</span><span class="sxs-lookup"><span data-stu-id="66941-111">Even resources you add later inherit hello lock from hello parent.</span></span> <span data-ttu-id="66941-112">de meest beperkende vergrendeling Hallo in Hallo overname voorrang.</span><span class="sxs-lookup"><span data-stu-id="66941-112">hello most restrictive lock in hello inheritance takes precedence.</span></span>

<span data-ttu-id="66941-113">In tegenstelling tot rollen gebaseerd toegangsbeheer kunt u management vergrendelingen tooapply een beperking voor alle gebruikers en -functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="66941-113">Unlike role-based access control, you use management locks tooapply a restriction across all users and roles.</span></span> <span data-ttu-id="66941-114">toolearn over het instellen van machtigingen voor gebruikers en rollen, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="66941-114">toolearn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="66941-115">Vergrendelingen van Resource Manager alleen toooperations die ontstaan in vlak voor Hallo die uit operations verzonden bestaat toepassen`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="66941-115">Resource Manager locks apply only toooperations that happen in hello management plane, which consists of operations sent too`https://management.azure.com`.</span></span> <span data-ttu-id="66941-116">Hallo vergrendelingen beperken niet hoe resources hun eigen functies uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="66941-116">hello locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="66941-117">Wijzigingen in de resourcedefinitie zijn beperkt, maar de bewerkingen van resources zijn niet beperkt.</span><span class="sxs-lookup"><span data-stu-id="66941-117">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="66941-118">Bijvoorbeeld, een vergrendeling van het kenmerk alleen-lezen voor een SQL-Database, voorkomt u dat verwijderen of wijzigen Hallo-database, maar het verhindert niet dat u maken, bijwerken of verwijderen van gegevens in het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="66941-118">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying hello database, but it does not prevent you from creating, updating, or deleting data in hello database.</span></span> <span data-ttu-id="66941-119">Gegevenstransacties worden toegestaan, omdat deze bewerkingen niet te worden verzonden`https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="66941-119">Data transactions are permitted because those operations are not sent too`https://management.azure.com`.</span></span>

<span data-ttu-id="66941-120">Toepassen van **ReadOnly** toounexpected resultaten kan leiden, omdat bepaalde bewerkingen die lijkt lezen bewerkingen daadwerkelijk extra acties vereist.</span><span class="sxs-lookup"><span data-stu-id="66941-120">Applying **ReadOnly** can lead toounexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="66941-121">Bijvoorbeeld, brengen een **ReadOnly** vergrendeling van een opslagaccount wordt voorkomen dat alle gebruikers aanbieding Hallo sleutels.</span><span class="sxs-lookup"><span data-stu-id="66941-121">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing hello keys.</span></span> <span data-ttu-id="66941-122">Hallo lijst sleutels opnieuw wordt verwerkt door een POST-aanvraag omdat Hallo geretourneerd sleutels zijn beschikbaar voor schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="66941-122">hello list keys operation is handled through a POST request because hello returned keys are available for write operations.</span></span> <span data-ttu-id="66941-123">Voor een ander voorbeeld plaatsen van een **ReadOnly** vergrendelen op een App Service-bron wordt voorkomen dat Visual Studio Server Explorer weergeven van bestanden voor de resource Hallo omdat die interactie voor toegang voor schrijven vereist.</span><span class="sxs-lookup"><span data-stu-id="66941-123">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for hello resource because that interaction requires write access.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="66941-124">Wie kunt maken of verwijderen van vergrendelingen in uw organisatie</span><span class="sxs-lookup"><span data-stu-id="66941-124">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="66941-125">management-vergrendelingen toocreate of verwijderen, moet u beschikken te`Microsoft.Authorization/*` of `Microsoft.Authorization/locks/*` acties.</span><span class="sxs-lookup"><span data-stu-id="66941-125">toocreate or delete management locks, you must have access too`Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="66941-126">Hallo ingebouwde rollen, alleen **eigenaar** en **beheerder voor gebruikerstoegang** deze acties worden verleend.</span><span class="sxs-lookup"><span data-stu-id="66941-126">Of hello built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="portal"></a><span data-ttu-id="66941-127">Portal</span><span class="sxs-lookup"><span data-stu-id="66941-127">Portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="template"></a><span data-ttu-id="66941-128">Template</span><span class="sxs-lookup"><span data-stu-id="66941-128">Template</span></span>
<span data-ttu-id="66941-129">Hallo volgende voorbeeld ziet u een sjabloon die wordt gemaakt van een vergrendeling op een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="66941-129">hello following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="66941-130">Hallo storage-account op welke tooapply Hallo vergrendeling is opgegeven als parameter.</span><span class="sxs-lookup"><span data-stu-id="66941-130">hello storage account on which tooapply hello lock is provided as a parameter.</span></span> <span data-ttu-id="66941-131">Hello naam Hallo vergrendeling wordt gemaakt door Hallo resourcenaam met cookievalidatie **/Microsoft.Authorization/** en de naam van de vergrendeling hello, in dit geval Hallo **myLock**.</span><span class="sxs-lookup"><span data-stu-id="66941-131">hello name of hello lock is created by concatenating hello resource name with **/Microsoft.Authorization/** and hello name of hello lock, in this case **myLock**.</span></span>

<span data-ttu-id="66941-132">Hallo type dat is opgegeven is specifiek toohello resourcetype.</span><span class="sxs-lookup"><span data-stu-id="66941-132">hello type provided is specific toohello resource type.</span></span> <span data-ttu-id="66941-133">Voor opslag, stelt u Hallo type too"Microsoft.Storage/storageaccounts/providers/locks'.</span><span class="sxs-lookup"><span data-stu-id="66941-133">For storage, set hello type too"Microsoft.Storage/storageaccounts/providers/locks".</span></span>

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

## <a name="powershell"></a><span data-ttu-id="66941-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66941-134">PowerShell</span></span>
<span data-ttu-id="66941-135">U vergrendeling resources met Azure PowerShell geïmplementeerd met behulp van Hallo [nieuw AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) opdracht.</span><span class="sxs-lookup"><span data-stu-id="66941-135">You lock deployed resources with Azure PowerShell by using hello [New-AzureRmResourceLock](/powershell/module/azurerm.resources/new-azurermresourcelock) command.</span></span>

<span data-ttu-id="66941-136">een resource toolock bieden Hallo-naam van Hallo resource, het resourcetype en de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="66941-136">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```powershell
New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite `
  -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="66941-137">een resourcegroep toolock bieden Hallo-naam van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="66941-137">toolock a resource group, provide hello name of hello resource group.</span></span>

```powershell
New-AzureRmResourceLock -LockName LockGroup -LockLevel CanNotDelete `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="66941-138">informatie over een vergrendeling, gebruik tooget [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span><span class="sxs-lookup"><span data-stu-id="66941-138">tooget information about a lock, use [Get-AzureRmResourceLock](/powershell/module/azurerm.resources/get-azurermresourcelock).</span></span> <span data-ttu-id="66941-139">tooget alle Hallo vergrendelingen in uw abonnement gebruiken:</span><span class="sxs-lookup"><span data-stu-id="66941-139">tooget all hello locks in your subscription, use:</span></span>

```powershell
Get-AzureRmResourceLock
```

<span data-ttu-id="66941-140">tooget alle vergrendelingen voor een bron gebruiken:</span><span class="sxs-lookup"><span data-stu-id="66941-140">tooget all locks for a resource, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceName examplesite -ResourceType Microsoft.Web/sites `
  -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="66941-141">tooget gebruiken voor alle vergrendelingen voor een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="66941-141">tooget all locks for a resource group, use:</span></span>

```powershell
Get-AzureRmResourceLock -ResourceGroupName exampleresourcegroup
```

<span data-ttu-id="66941-142">Azure PowerShell biedt andere opdrachten voor vergrendelingen werken, zoals [Set AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate een vergrendeling en [verwijderen AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete een vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="66941-142">Azure PowerShell provides other commands for working locks, such as [Set-AzureRmResourceLock](/powershell/module/azurerm.resources/set-azurermresourcelock) tooupdate a lock, and [Remove-AzureRmResourceLock](/powershell/module/azurerm.resources/remove-azurermresourcelock) toodelete a lock.</span></span>

## <a name="azure-cli"></a><span data-ttu-id="66941-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="66941-143">Azure CLI</span></span>

<span data-ttu-id="66941-144">U vergrendeling resources met Azure CLI geïmplementeerd met behulp van Hallo [az vergrendeling maken](/cli/azure/lock#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="66941-144">You lock deployed resources with Azure CLI by using hello [az lock create](/cli/azure/lock#create) command.</span></span>

<span data-ttu-id="66941-145">een resource toolock bieden Hallo-naam van Hallo resource, het resourcetype en de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="66941-145">toolock a resource, provide hello name of hello resource, its resource type, and its resource group name.</span></span>

```azurecli
az lock create --name LockSite --lock-type CanNotDelete \
  --resource-group exampleresourcegroup --resource-name examplesite \
  --resource-type Microsoft.Web/sites
```

<span data-ttu-id="66941-146">een resourcegroep toolock bieden Hallo-naam van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="66941-146">toolock a resource group, provide hello name of hello resource group.</span></span>

```azurecli
az lock create --name LockGroup --lock-type CanNotDelete \
  --resource-group exampleresourcegroup
```

<span data-ttu-id="66941-147">informatie over een vergrendeling, gebruik tooget [az vergrendeling lijst](/cli/azure/lock#list).</span><span class="sxs-lookup"><span data-stu-id="66941-147">tooget information about a lock, use [az lock list](/cli/azure/lock#list).</span></span> <span data-ttu-id="66941-148">tooget alle Hallo vergrendelingen in uw abonnement gebruiken:</span><span class="sxs-lookup"><span data-stu-id="66941-148">tooget all hello locks in your subscription, use:</span></span>

```azurecli
az lock list
```

<span data-ttu-id="66941-149">tooget alle vergrendelingen voor een bron gebruiken:</span><span class="sxs-lookup"><span data-stu-id="66941-149">tooget all locks for a resource, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup --resource-name examplesite \
  --namespace Microsoft.Web --resource-type sites --parent ""
```

<span data-ttu-id="66941-150">tooget gebruiken voor alle vergrendelingen voor een resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="66941-150">tooget all locks for a resource group, use:</span></span>

```azurecli
az lock list --resource-group exampleresourcegroup
```

<span data-ttu-id="66941-151">Azure CLI biedt andere opdrachten voor vergrendelingen werken, zoals [az vergrendeling update](/cli/azure/lock#update) tooupdate een vergrendeling en [az vergrendeling verwijderen](/cli/azure/lock#delete) toodelete een vergrendeling.</span><span class="sxs-lookup"><span data-stu-id="66941-151">Azure CLI provides other commands for working locks, such as [az lock update](/cli/azure/lock#update) tooupdate a lock, and [az lock delete](/cli/azure/lock#delete) toodelete a lock.</span></span>

## <a name="rest-api"></a><span data-ttu-id="66941-152">REST API</span><span class="sxs-lookup"><span data-stu-id="66941-152">REST API</span></span>
<span data-ttu-id="66941-153">U kunt vergrendelen geïmplementeerde resources Hello [REST-API voor beheer van vergrendelingen](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="66941-153">You can lock deployed resources with hello [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="66941-154">Hallo REST-API kunt u toocreate vergrendelingen worden verwijderd en informatie ophalen over bestaande vergrendelingen.</span><span class="sxs-lookup"><span data-stu-id="66941-154">hello REST API enables you toocreate and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="66941-155">toocreate een vergrendeling uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="66941-155">toocreate a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="66941-156">Hallo-scope wordt mogelijk een abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="66941-156">hello scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="66941-157">Hallo-vergrendelingsnaam is elke gewenste toocall Hallo vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="66941-157">hello lock-name is whatever you want toocall hello lock.</span></span> <span data-ttu-id="66941-158">Gebruik voor de api-versie **01-01-2015**.</span><span class="sxs-lookup"><span data-stu-id="66941-158">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="66941-159">Hallo-aanvraag bevatten een JSON-object waarmee Hallo-eigenschappen voor Hallo vergrendelen.</span><span class="sxs-lookup"><span data-stu-id="66941-159">In hello request, include a JSON object that specifies hello properties for hello lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 

## <a name="next-steps"></a><span data-ttu-id="66941-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="66941-160">Next steps</span></span>
* <span data-ttu-id="66941-161">Zie voor meer informatie over het werken met resource vergrendelingen [vergrendeling omlaag Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="66941-161">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="66941-162">Zie toolearn over logisch indelen van uw resources [Using tags tooorganize uw resources](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="66941-162">toolearn about logically organizing your resources, see [Using tags tooorganize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="66941-163">toochange welke resourcegroep een bron zich bevindt, Zie [verplaatsen resources toonew resourcegroep](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="66941-163">toochange which resource group a resource resides in, see [Move resources toonew resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="66941-164">U kunt beperkingen en conventies toepassen voor uw abonnement met aangepast beleid.</span><span class="sxs-lookup"><span data-stu-id="66941-164">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="66941-165">Zie voor meer informatie [beleid toomanage resources en toegang beheren](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="66941-165">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="66941-166">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="66941-166">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

