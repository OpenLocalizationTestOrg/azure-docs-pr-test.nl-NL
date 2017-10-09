---
title: aangepaste rollen voor Azure RBAC aaaCreate | Microsoft Docs
description: Meer informatie over hoe toodefine aangepaste rollen met op rollen gebaseerd toegangsbeheer voor nauwkeurigere identiteitsbeheer in uw Azure-abonnement.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: e4206ea9-52c3-47ee-af29-f6eef7566fa5
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/11/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 60df12632ef6c086d5feeb1809196d7c4ee5e021
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-custom-roles-for-azure-role-based-access-control"></a><span data-ttu-id="cd7a5-103">Aangepaste rollen maken voor op rollen gebaseerd toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="cd7a5-103">Create custom roles for Azure Role-Based Access Control</span></span>
<span data-ttu-id="cd7a5-104">Maak een aangepaste rol in gebaseerd toegangsbeheer (RBAC) als geen van de ingebouwde rollen Hallo voldoet aan de behoeften van uw specifieke toegang.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-104">Create a custom role in Azure Role-Based Access Control (RBAC) if none of hello built-in roles meet your specific access needs.</span></span> <span data-ttu-id="cd7a5-105">Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface](role-based-access-control-manage-access-azure-cli.md) (CLI) en Hallo [REST-API](role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="cd7a5-105">Custom roles can be created using [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface](role-based-access-control-manage-access-azure-cli.md) (CLI), and hello [REST API](role-based-access-control-manage-access-rest.md).</span></span> <span data-ttu-id="cd7a5-106">Net als de ingebouwde rollen kunt u aangepaste rollen toousers, groepen en toepassingen bij het abonnement, resourcegroep en resource bereiken toewijzen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-106">Just like built-in roles, you can assign custom roles toousers, groups, and applications at subscription, resource group, and resource scopes.</span></span> <span data-ttu-id="cd7a5-107">Aangepaste rollen worden opgeslagen in een Azure AD-tenant en kunnen worden gedeeld door abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-107">Custom roles are stored in an Azure AD tenant and can be shared across subscriptions.</span></span>

<span data-ttu-id="cd7a5-108">Elke tenant kunt maken van aangepaste rollen too2000.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-108">Each tenant can create up too2000 custom roles.</span></span> 

<span data-ttu-id="cd7a5-109">Hallo volgende voorbeeld ziet u een aangepaste rol voor het controleren en opnieuw starten van virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="cd7a5-109">hello following example shows a custom role for monitoring and restarting virtual machines:</span></span>

```
{
  "Name": "Virtual Machine Operator",
  "Id": "cadb4a5a-4e7a-47be-84db-05cad13b6769",
  "IsCustom": true,
  "Description": "Can monitor and restart virtual machines.",
  "Actions": [
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Compute/*/read",
    "Microsoft.Compute/virtualMachines/start/action",
    "Microsoft.Compute/virtualMachines/restart/action",
    "Microsoft.Authorization/*/read",
    "Microsoft.Resources/subscriptions/resourceGroups/read",
    "Microsoft.Insights/alertRules/*",
    "Microsoft.Insights/diagnosticSettings/*",
    "Microsoft.Support/*"
  ],
  "NotActions": [

  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624",
    "/subscriptions/34370e90-ac4a-4bf9-821f-85eeedeae1a2"
  ]
}
```
## <a name="actions"></a><span data-ttu-id="cd7a5-110">Acties</span><span class="sxs-lookup"><span data-stu-id="cd7a5-110">Actions</span></span>
<span data-ttu-id="cd7a5-111">Hallo **acties** eigenschap van een aangepaste rol geeft hello Azure-bewerkingen toowhich Hallo rol toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-111">hello **Actions** property of a custom role specifies hello Azure operations toowhich hello role grants access.</span></span> <span data-ttu-id="cd7a5-112">Er is een verzameling van bewerking tekenreeksen waarmee beveiligbare bewerkingen van de Azure-resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-112">It is a collection of operation strings that identify securable operations of Azure resource providers.</span></span> <span data-ttu-id="cd7a5-113">Bewerking tekenreeksen volgt Hallo-indeling van `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-113">Operation strings follow hello format of `Microsoft.<ProviderName>/<ChildResourceType>/<action>`.</span></span> <span data-ttu-id="cd7a5-114">Bewerking tekenreeksen met jokertekens (\*) toegang verlenen tooall-bewerkingen die overeenkomen met de Hallo bewerking tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-114">Operation strings that contain wildcards (\*) grant access tooall operations that match hello operation string.</span></span> <span data-ttu-id="cd7a5-115">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="cd7a5-115">For instance:</span></span>

* <span data-ttu-id="cd7a5-116">`*/read`verleent toegang tot tooread bewerkingen voor alle resourcetypen van alle Azure-resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-116">`*/read` grants access tooread operations for all resource types of all Azure resource providers.</span></span>
* <span data-ttu-id="cd7a5-117">`Microsoft.Compute/*`verleent toegang tot tooall bewerkingen voor alle brontypen in Hallo Microsoft.Compute-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-117">`Microsoft.Compute/*` grants access tooall operations for all resource types in hello Microsoft.Compute resource provider.</span></span>
* <span data-ttu-id="cd7a5-118">`Microsoft.Network/*/read`verleent toegang tot tooread bewerkingen voor alle brontypen in Hallo Microsoft.Network-resourceprovider van Azure.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-118">`Microsoft.Network/*/read` grants access tooread operations for all resource types in hello Microsoft.Network resource provider of Azure.</span></span>
* <span data-ttu-id="cd7a5-119">`Microsoft.Compute/virtualMachines/*`verleent toegang tot tooall bewerkingen van virtuele machines en de onderliggende resourcetypen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-119">`Microsoft.Compute/virtualMachines/*` grants access tooall operations of virtual machines and its child resource types.</span></span>
* <span data-ttu-id="cd7a5-120">`Microsoft.Web/sites/restart/Action`verleent toegang tot toorestart websites.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-120">`Microsoft.Web/sites/restart/Action` grants access toorestart websites.</span></span>

<span data-ttu-id="cd7a5-121">Gebruik `Get-AzureRmProviderOperation` (in PowerShell) of `azure provider operations show` (in de Azure CLI) toolist bewerkingen van de Azure-resourceproviders.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-121">Use `Get-AzureRmProviderOperation` (in PowerShell) or `azure provider operations show` (in Azure CLI) toolist operations of Azure resource providers.</span></span> <span data-ttu-id="cd7a5-122">U kunt ook deze opdrachten tooverify of een tekenreeks bewerking geldig is en tooexpand jokertekens bewerking tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-122">You may also use these commands tooverify that an operation string is valid, and tooexpand wildcard operation strings.</span></span>

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Schermafbeelding van de PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![<span data-ttu-id="cd7a5-124">Azure CLI schermafbeelding - azure-bewerkingen weergeven voor provider "Microsoft.Compute/virtualMachines/ \* /Action"</span><span class="sxs-lookup"><span data-stu-id="cd7a5-124">Azure CLI screenshot - azure provider operations show "Microsoft.Compute/virtualMachines/\*/action"</span></span> ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a><span data-ttu-id="cd7a5-125">NotActions</span><span class="sxs-lookup"><span data-stu-id="cd7a5-125">NotActions</span></span>
<span data-ttu-id="cd7a5-126">Gebruik Hallo **NotActions** eigenschap als Hallo reeks bewerkingen die u wenst dat tooallow eenvoudiger wordt gedefinieerd door het met uitzondering van beperkte bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-126">Use hello **NotActions** property if hello set of operations that you wish tooallow is more easily defined by excluding restricted operations.</span></span> <span data-ttu-id="cd7a5-127">Hallo wordt toegang verleend door een aangepaste beveiligingsrol berekend door af te trekken Hallo **NotActions** bewerkingen van het Hallo **acties** bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-127">hello access granted by a custom role is computed by subtracting hello **NotActions** operations from hello **Actions** operations.</span></span>

> [!NOTE]
> <span data-ttu-id="cd7a5-128">Als een gebruiker een rol heeft die worden uitgesloten van een bewerking in toegewezen **NotActions**, en een tweede rol die toegang verleent is toegewezen toohello dezelfde bewerking, Hallo gebruiker is toegestaan tooperform die voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-128">If a user is assigned a role that excludes an operation in **NotActions**, and is assigned a second role that grants access toohello same operation, hello user is allowed tooperform that operation.</span></span> <span data-ttu-id="cd7a5-129">**NotActions** is niet een weigeren regel – is gewoon de toocreate van een handige manier kan een aantal toegestane bewerkingen wanneer specifieke bewerkingen moeten toobe uitgesloten.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-129">**NotActions** is not a deny rule – it is simply a convenient way toocreate a set of allowed operations when specific operations need toobe excluded.</span></span>
>
>

## <a name="assignablescopes"></a><span data-ttu-id="cd7a5-130">AssignableScopes</span><span class="sxs-lookup"><span data-stu-id="cd7a5-130">AssignableScopes</span></span>
<span data-ttu-id="cd7a5-131">Hallo **AssignableScopes** eigenschap van de aangepaste rol Hallo Hiermee geeft u Hallo scopes (abonnementen, resourcegroepen of bronnen) in welke Hallo aangepaste rol beschikbaar voor toewijzing is.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-131">hello **AssignableScopes** property of hello custom role specifies hello scopes (subscriptions, resource groups, or resources) within which hello custom role is available for assignment.</span></span> <span data-ttu-id="cd7a5-132">U kunt aangepaste rol Hallo beschikbaar voor toewijzing in Hallo-abonnementen of resourcegroepen waarvoor en niet vol gebruiker ervaring voor de rest Hallo van Hallo abonnementen of resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-132">You can make hello custom role available for assignment in only hello subscriptions or resource groups that require it, and not clutter user experience for hello rest of hello subscriptions or resource groups.</span></span>

<span data-ttu-id="cd7a5-133">Voorbeelden van geldige toewijsbare bereiken zijn:</span><span class="sxs-lookup"><span data-stu-id="cd7a5-133">Examples of valid assignable scopes include:</span></span>

* <span data-ttu-id="cd7a5-134">"/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e', '/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624' - maakt Hallo rol beschikbaar voor toewijzing in twee abonnementen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-134">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e”, “/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624” - makes hello role available for assignment in two subscriptions.</span></span>
* <span data-ttu-id="cd7a5-135">'/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e' - maakt Hallo rol beschikbaar voor toewijzing in één abonnement.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-135">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e” - makes hello role available for assignment in a single subscription.</span></span>
* <span data-ttu-id="cd7a5-136">'/ abonnementen/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/netwerk' - zorgt ervoor dat Hallo rol beschikbaar voor toewijzing alleen in de resourcegroep Hallo-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-136">“/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network” - makes hello role available for assignment only in hello Network resource group.</span></span>

> [!NOTE]
> <span data-ttu-id="cd7a5-137">Moet u ten minste één abonnement, resourcegroep of resource-ID.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-137">You must use at least one subscription, resource group, or resource ID.</span></span>
>
>

## <a name="custom-roles-access-control"></a><span data-ttu-id="cd7a5-138">Aangepaste rollen toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="cd7a5-138">Custom roles access control</span></span>
<span data-ttu-id="cd7a5-139">Hallo **AssignableScopes** ook de eigenschap van de aangepaste rol Hallo bepaalt wie kunt weergeven, wijzigen en verwijderen van rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-139">hello **AssignableScopes** property of hello custom role also controls who can view, modify, and delete hello role.</span></span>

* <span data-ttu-id="cd7a5-140">Wie kan een aangepaste beveiligingsrol maken?</span><span class="sxs-lookup"><span data-stu-id="cd7a5-140">Who can create a custom role?</span></span>
    <span data-ttu-id="cd7a5-141">Eigenaars (en beheerders van de gebruiker toegang) van de abonnementen, resourcegroepen en resources kunnen aangepaste rollen maken voor gebruik in deze bereiken.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-141">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can create custom roles for use in those scopes.</span></span>
    <span data-ttu-id="cd7a5-142">Hallo gebruiker maken Hallo rol moet kunnen tooperform toobe `Microsoft.Authorization/roleDefinition/write` bewerking op alle Hallo **AssignableScopes** van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-142">hello user creating hello role needs toobe able tooperform `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of hello role.</span></span>
* <span data-ttu-id="cd7a5-143">Wie kan een aangepaste rol wijzigen?</span><span class="sxs-lookup"><span data-stu-id="cd7a5-143">Who can modify a custom role?</span></span>
    <span data-ttu-id="cd7a5-144">Eigenaars (en beheerders van de gebruiker toegang) van de abonnementen, resourcegroepen en resources aangepaste rollen in deze bereiken kunnen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-144">Owners (and User Access Administrators) of subscriptions, resource groups, and resources can modify custom roles in those scopes.</span></span> <span data-ttu-id="cd7a5-145">Gebruikers moeten toobe kunnen tooperform hello `Microsoft.Authorization/roleDefinition/write` bewerking op alle Hallo **AssignableScopes** van een aangepaste beveiligingsrol.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-145">Users need toobe able tooperform hello `Microsoft.Authorization/roleDefinition/write` operation on all hello **AssignableScopes** of a custom role.</span></span>
* <span data-ttu-id="cd7a5-146">Wie kan aangepaste rollen bekijken?</span><span class="sxs-lookup"><span data-stu-id="cd7a5-146">Who can view custom roles?</span></span>
    <span data-ttu-id="cd7a5-147">Alle ingebouwde rollen in Azure RBAC kunnen bekijken van functies die beschikbaar voor toewijzing zijn.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-147">All built-in roles in Azure RBAC allow viewing of roles that are available for assignment.</span></span> <span data-ttu-id="cd7a5-148">Gebruikers Hallo uitvoeren kunnen `Microsoft.Authorization/roleDefinition/read` bewerking op een scope Hallo RBAC functies die beschikbaar voor toewijzing op dat bereik zijn kunt weergeven.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-148">Users who can perform hello `Microsoft.Authorization/roleDefinition/read` operation at a scope can view hello RBAC roles that are available for assignment at that scope.</span></span>

## <a name="see-also"></a><span data-ttu-id="cd7a5-149">Zie ook</span><span class="sxs-lookup"><span data-stu-id="cd7a5-149">See also</span></span>
* <span data-ttu-id="cd7a5-150">[Op rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-150">[Role Based Access Control](role-based-access-control-configure.md): Get started with RBAC in hello Azure portal.</span></span>
* <span data-ttu-id="cd7a5-151">Meer informatie over hoe toomanage met toegang tot:</span><span class="sxs-lookup"><span data-stu-id="cd7a5-151">Learn how toomanage access with:</span></span>
  * [<span data-ttu-id="cd7a5-152">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd7a5-152">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
  * [<span data-ttu-id="cd7a5-153">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="cd7a5-153">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
  * [<span data-ttu-id="cd7a5-154">REST API</span><span class="sxs-lookup"><span data-stu-id="cd7a5-154">REST API</span></span>](role-based-access-control-manage-access-rest.md)
* <span data-ttu-id="cd7a5-155">[Ingebouwde rollen](role-based-access-built-in-roles.md): meer informatie over het Hallo-functies die standaard in RBAC.</span><span class="sxs-lookup"><span data-stu-id="cd7a5-155">[Built-in roles](role-based-access-built-in-roles.md): Get details about hello roles that come standard in RBAC.</span></span>
