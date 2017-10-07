---
title: aaaManage op rollen gebaseerde toegangsbeheer (RBAC) met Azure PowerShell | Microsoft Docs
description: Hoe toomanage RBAC met Azure PowerShell, met inbegrip van de aanbieding rollen, rollen toewijzen en het verwijderen van roltoewijzingen.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 9e225dba-9044-4b13-b573-2f30d77925a9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: fa44991113e75b345177867b0bede38de4373e04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-azure-powershell"></a><span data-ttu-id="5bc2e-103">Toegangsbeheer op basis van rollen beheren met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bc2e-103">Manage Role-Based Access Control with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bc2e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5bc2e-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="5bc2e-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="5bc2e-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="5bc2e-106">REST API</span><span class="sxs-lookup"><span data-stu-id="5bc2e-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="5bc2e-107">In hello Azure-portal en Azure Resource Management-API toomanage toegang tooyour abonnement heel nauwkeurig kunt u rollen gebaseerd toegangsbeheer (RBAC).</span><span class="sxs-lookup"><span data-stu-id="5bc2e-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Management API toomanage access tooyour subscription at a fine-grained level.</span></span> <span data-ttu-id="5bc2e-108">Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="5bc2e-109">Voordat u PowerShell toomanage RBAC gebruiken kunt, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-109">Before you can use PowerShell toomanage RBAC, you need hello following prerequisites:</span></span>

* <span data-ttu-id="5bc2e-110">Azure PowerShell versie 0.8.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-110">Azure PowerShell version 0.8.8 or later.</span></span> <span data-ttu-id="5bc2e-111">meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5bc2e-111">tooinstall hello latest version and associate it with your Azure subscription, see [how tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="5bc2e-112">Azure Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-112">Azure Resource Manager cmdlets.</span></span> <span data-ttu-id="5bc2e-113">Hallo installeren [Azure Resource Manager-cmdlets](/powershell/azure/overview) in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-113">Install hello [Azure Resource Manager cmdlets](/powershell/azure/overview) in PowerShell.</span></span>

## <a name="list-roles"></a><span data-ttu-id="5bc2e-114">Lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="5bc2e-115">Lijst van alle beschikbare rollen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-115">List all available roles</span></span>
<span data-ttu-id="5bc2e-116">toolist RBAC functies die beschikbaar zijn voor toewijzing en tooinspect Hallo operations toowhich ze toegang, gebruik `Get-AzureRmRoleDefinition`.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-116">toolist RBAC roles that are available for assignment and tooinspect hello operations toowhich they grant access, use `Get-AzureRmRoleDefinition`.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, Description
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition1.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="5bc2e-118">Van Lijstacties van een rol</span><span class="sxs-lookup"><span data-stu-id="5bc2e-118">List actions of a role</span></span>
<span data-ttu-id="5bc2e-119">Gebruik toolist Hallo acties voor een specifieke rol `Get-AzureRmRoleDefinition <role name>`.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-119">toolist hello actions for a specific role, use `Get-AzureRmRoleDefinition <role name>`.</span></span>

```
Get-AzureRmRoleDefinition Contributor | FL Actions, NotActions

(Get-AzureRmRoleDefinition "Virtual Machine Contributor").Actions
```

![RBAC PowerShell-Get AzureRmRoleDefinition voor een specifieke rol - schermafbeelding](./media/role-based-access-control-manage-access-powershell/1-get-azure-rm-role-definition2.png)

## <a name="see-who-has-access"></a><span data-ttu-id="5bc2e-121">Zien wie toegang heeft</span><span class="sxs-lookup"><span data-stu-id="5bc2e-121">See who has access</span></span>
<span data-ttu-id="5bc2e-122">toolist RBAC toegangstoewijzingen gebruiken `Get-AzureRmRoleAssignment`.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-122">toolist RBAC access assignments, use `Get-AzureRmRoleAssignment`.</span></span>

### <a name="list-role-assignments-at-a-specific-scope"></a><span data-ttu-id="5bc2e-123">Roltoewijzingen lijst op een specifiek bereik</span><span class="sxs-lookup"><span data-stu-id="5bc2e-123">List role assignments at a specific scope</span></span>
<span data-ttu-id="5bc2e-124">Hier ziet u alle toewijzingen van Hallo toegang voor een opgegeven abonnement, resourcegroep of resource.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-124">You can see all hello access assignments for a specified subscription, resource group, or resource.</span></span> <span data-ttu-id="5bc2e-125">Bijvoorbeeld, toosee alle actieve Hallo-toewijzingen voor een resourcegroep of gebruik Hallo `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-125">For example, toosee hello all hello active assignments for a resource group, use `Get-AzureRmRoleAssignment -ResourceGroupName <resource group name>`.</span></span>

```
Get-AzureRmRoleAssignment -ResourceGroupName Pharma-Sales-ProjectForcast | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment voor een resourcegroep - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment1.png)

### <a name="list-roles-assigned-tooa-user"></a><span data-ttu-id="5bc2e-127">Lijst met rollen toegewezen tooa gebruiker</span><span class="sxs-lookup"><span data-stu-id="5bc2e-127">List roles assigned tooa user</span></span>
<span data-ttu-id="5bc2e-128">alle Hallo rollen die zijn toegewezen tooa opgegeven gebruikers- en Hallo-rollen die zijn toegewezen toohello groepen toowhich Hallo gebruiker behoort, toolist gebruik `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-128">toolist all hello roles that are assigned tooa specified user and hello roles that are assigned toohello groups toowhich hello user belongs, use `Get-AzureRmRoleAssignment -SignInName <User email> -ExpandPrincipalGroups`.</span></span>

```
Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com | FL DisplayName, RoleDefinitionName, Scope

Get-AzureRmRoleAssignment -SignInName sameert@aaddemo.com -ExpandPrincipalGroups | FL DisplayName, RoleDefinitionName, Scope
```

![RBAC PowerShell - Get-AzureRmRoleAssignment voor een gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-get-azure-rm-role-assignment2.png)

### <a name="list-classic-service-administrator-and-coadmin-role-assignments"></a><span data-ttu-id="5bc2e-130">Lijst met klassieke servicebeheerder en coadmin roltoewijzingen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-130">List classic service administrator and coadmin role assignments</span></span>
<span data-ttu-id="5bc2e-131">toolist toegangstoewijzingen voor de klassieke abonnementsbeheerder Hallo en coadministrators, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-131">toolist access assignments for hello classic subscription administrator and coadministrators, use:</span></span>

    Get-AzureRmRoleAssignment -IncludeClassicAdministrators

## <a name="grant-access"></a><span data-ttu-id="5bc2e-132">Toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-132">Grant access</span></span>
### <a name="search-for-object-ids"></a><span data-ttu-id="5bc2e-133">Zoeken naar object-id 's</span><span class="sxs-lookup"><span data-stu-id="5bc2e-133">Search for object IDs</span></span>
<span data-ttu-id="5bc2e-134">tooassign een rol, moet u tooidentify zowel Hallo-object (gebruiker, groep of toepassing) en Hallo bereik.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-134">tooassign a role, you need tooidentify both hello object (user, group, or application) and hello scope.</span></span>

<span data-ttu-id="5bc2e-135">Als u Hallo abonnements-ID niet weet, kunt u deze vinden in Hallo **abonnementen** blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-135">If you don't know hello subscription ID, you can find it in hello **Subscriptions** blade on hello Azure portal.</span></span> <span data-ttu-id="5bc2e-136">hoe tooquery voor Hallo abonnements-ID, Zie toolearn [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) op MSDN.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-136">toolearn how tooquery for hello subscription ID, see [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) on MSDN.</span></span>

<span data-ttu-id="5bc2e-137">tooget Hallo-object-ID voor een Azure AD-groep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-137">tooget hello object ID for an Azure AD group, use:</span></span>

    Get-AzureRmADGroup -SearchString <group name in quotes>

<span data-ttu-id="5bc2e-138">tooget Hallo-object-ID voor een Azure AD-service-principal of toepassing, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-138">tooget hello object ID for an Azure AD service principal or application, use:</span></span>

    Get-AzureRmADServicePrincipal -SearchString <service name in quotes>

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="5bc2e-139">Een rol tooan toepassing in het bereik van Hallo abonnement toewijzen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-139">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="5bc2e-140">toogrant toegang tooan-toepassing op Hallo abonnementsbereik gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-140">toogrant access tooan application at hello subscription scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <application id> -RoleDefinitionName <role name> -Scope <subscription id>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="5bc2e-142">Een gebruiker van de rol tooa op Hallo resource groepsbereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-142">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="5bc2e-143">toogrant toegang tooa gebruiker op Hallo resource groepsbereik gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-143">toogrant access tooa user at hello resource group scope, use:</span></span>

    New-AzureRmRoleAssignment -SignInName <email of user> -RoleDefinitionName <role name in quotes> -ResourceGroupName <resource group name>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="5bc2e-145">Een groep rol tooa bij Hallo resource bereik worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-145">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="5bc2e-146">toogrant tooa toegangsgroep op Hallo resource bereik gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-146">toogrant access tooa group at hello resource scope, use:</span></span>

    New-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name in quotes> -ResourceName <resource name> -ResourceType <resource type> -ParentResource <parent resource> -ResourceGroupName <resource group name>

![RBAC PowerShell - nieuwe AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azure-rm-role-assignment4.png)

## <a name="remove-access"></a><span data-ttu-id="5bc2e-148">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-148">Remove access</span></span>
<span data-ttu-id="5bc2e-149">tooremove toegang voor gebruikers, groepen en toepassingen, gebruik:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-149">tooremove access for users, groups, and applications, use:</span></span>

    Remove-AzureRmRoleAssignment -ObjectId <object id> -RoleDefinitionName <role name> -Scope <scope such as subscription id>

![RBAC PowerShell-Remove AzureRmRoleAssignment - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-remove-azure-rm-role-assignment.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="5bc2e-151">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="5bc2e-151">Create a custom role</span></span>
<span data-ttu-id="5bc2e-152">een aangepaste beveiligingsrol toocreate gebruiken Hallo ```New-AzureRmRoleDefinition``` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-152">toocreate a custom role, use hello ```New-AzureRmRoleDefinition``` command.</span></span> <span data-ttu-id="5bc2e-153">Er zijn twee methoden voor het structureren Hallo-rol, met behulp van PSRoleDefinitionObject of een JSON-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-153">There are two methods of structuring hello role, using PSRoleDefinitionObject or a JSON template.</span></span> 

## <a name="get-actions-for-a-resource-provider"></a><span data-ttu-id="5bc2e-154">Acties voor een Resourceprovider ophalen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-154">Get Actions for a Resource Provider</span></span>
<span data-ttu-id="5bc2e-155">Tijdens het maken van aangepaste rollen maken, het is belangrijk tooknow alle mogelijke bewerkingen van de resourceproviders Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-155">When You are creating custom roles from scratch, it is important tooknow all hello possible operations from hello resource providers.</span></span>
<span data-ttu-id="5bc2e-156">Gebruik Hallo ```Get-AzureRMProviderOperation``` opdracht tooget deze informatie.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-156">Use hello ```Get-AzureRMProviderOperation``` command tooget this information.</span></span>
<span data-ttu-id="5bc2e-157">Als u wilt dat toocheck gebruiken alle beschikbare Hallo-bewerkingen voor de virtuele Machine met deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-157">For example, if you want toocheck all hello available operations for virtual Machine use this command:</span></span>

```
Get-AzureRMProviderOperation "Microsoft.Compute/virtualMachines/*" | FT OperationName, Operation , Description -AutoSize
```

### <a name="create-role-with-psroledefinitionobject"></a><span data-ttu-id="5bc2e-158">Rol maken met PSRoleDefinitionObject</span><span class="sxs-lookup"><span data-stu-id="5bc2e-158">Create role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="5bc2e-159">Wanneer u PowerShell toocreate een aangepaste beveiligingsrol gebruikt, kunt u helemaal opnieuw begint of gebruik een van de Hallo [ingebouwde rollen](role-based-access-built-in-roles.md) als uitgangspunt.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-159">When you use PowerShell toocreate a custom role, you can start from scratch or use one of hello [built-in roles](role-based-access-built-in-roles.md) as a starting point.</span></span> <span data-ttu-id="5bc2e-160">Hallo-voorbeeld in deze sectie begint met een ingebouwde rol en past deze met meer bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-160">hello example in this section starts with a built-in role and then customizes it with more privileges.</span></span> <span data-ttu-id="5bc2e-161">Hallo kenmerken tooadd Hallo bewerken *acties*, *notActions*, of *scopes* die u wilt gebruiken en dan Hallo wijzigingen opslaan als een nieuwe rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-161">Edit hello attributes tooadd hello *Actions*, *notActions*, or *scopes* that you want, and then save hello changes as a new role.</span></span>

<span data-ttu-id="5bc2e-162">Hallo volgende voorbeeld wordt gestart met de Hallo *Virtual Machine Contributor* rol en gebruikt die toocreate een aangepaste beveiligingsrol aangeroepen *virtuele Machine Operator*.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-162">hello following example starts with hello *Virtual Machine Contributor* role and uses that toocreate a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="5bc2e-163">de nieuwe rol Hallo verleent toegang tooall leesbewerkingen van *Microsoft.Compute*, *Microsoft.Storage*, en *Microsoft.Network* providers en verleent toegang tot bedrijfsbronnen toostart, opnieuw opstarten en virtuele machines bewaken.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-163">hello new role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="5bc2e-164">Hallo aangepaste rol kan worden gebruikt in twee abonnementen.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-164">hello custom role can be used in two subscriptions.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Contributor"
$role.Id = $null
$role.Name = "Virtual Machine Operator"
$role.Description = "Can monitor and restart virtual machines."
$role.Actions.Clear()
$role.Actions.Add("Microsoft.Storage/*/read")
$role.Actions.Add("Microsoft.Network/*/read")
$role.Actions.Add("Microsoft.Compute/*/read")
$role.Actions.Add("Microsoft.Compute/virtualMachines/start/action")
$role.Actions.Add("Microsoft.Compute/virtualMachines/restart/action")
$role.Actions.Add("Microsoft.Authorization/*/read")
$role.Actions.Add("Microsoft.Resources/subscriptions/resourceGroups/read")
$role.Actions.Add("Microsoft.Insights/alertRules/*")
$role.Actions.Add("Microsoft.Support/*")
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add("/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e")
$role.AssignableScopes.Add("/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624")
New-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/2-new-azurermroledefinition.png)

### <a name="create-role-with-json-template"></a><span data-ttu-id="5bc2e-166">Rol met JSON-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="5bc2e-166">Create role with JSON template</span></span>
<span data-ttu-id="5bc2e-167">Een JSON-sjabloon kan worden gebruikt als de brondefinitie Hallo voor Hallo aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-167">A JSON template can be used as hello source definition for hello custom role.</span></span> <span data-ttu-id="5bc2e-168">Hallo volgende voorbeeld maakt u een aangepaste rol die leestoegang toostorage kunt rekenresources, toegang tot toosupport en voegt die rol tootwo abonnementen.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-168">hello following example creates a custom role that allows read access toostorage and compute resources, access toosupport, and adds that role tootwo subscriptions.</span></span> <span data-ttu-id="5bc2e-169">Maak een nieuw bestand `C:\CustomRoles\customrole1.json` Hello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-169">Create a new file `C:\CustomRoles\customrole1.json` with hello following example.</span></span> <span data-ttu-id="5bc2e-170">Hallo-Id moet worden ingesteld te`null` op het eerste rol maken als een nieuwe ID automatisch wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-170">hello Id should be set too`null` on initial role creation as a new ID is generated automatically.</span></span> 

```
{
  "Name": "Custom Role 1",
  "Id": null,
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```
<span data-ttu-id="5bc2e-171">tooadd hello rol toohello abonnementen Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-171">tooadd hello role toohello subscriptions, run hello following PowerShell command:</span></span>
```
New-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="modify-a-custom-role"></a><span data-ttu-id="5bc2e-172">Een aangepaste rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-172">Modify a custom role</span></span>
<span data-ttu-id="5bc2e-173">Vergelijkbare toocreating een aangepaste beveiligingsrol, kunt u een bestaande aangepaste rol met behulp van Hallo PSRoleDefinitionObject of een JSON-sjabloon wijzigen.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-173">Similar toocreating a custom role, you can modify an existing custom role using either hello PSRoleDefinitionObject or a JSON template.</span></span>

### <a name="modify-role-with-psroledefinitionobject"></a><span data-ttu-id="5bc2e-174">Rol met PSRoleDefinitionObject wijzigen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-174">Modify role with PSRoleDefinitionObject</span></span>
<span data-ttu-id="5bc2e-175">Hallo eerst met behulp van een aangepaste beveiligingsrol toomodify `Get-AzureRmRoleDefinition` tooretrieve Hallo roldefinitie opdracht.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-175">toomodify a custom role, first, use hello `Get-AzureRmRoleDefinition` command tooretrieve hello role definition.</span></span> <span data-ttu-id="5bc2e-176">Ten tweede aanbrengen Hallo gewenst toohello roldefinitie.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-176">Second, make hello desired changes toohello role definition.</span></span> <span data-ttu-id="5bc2e-177">Gebruik tot slot Hallo `Set-AzureRmRoleDefinition` opdracht toosave Hallo roldefinitie gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-177">Finally, use hello `Set-AzureRmRoleDefinition` command toosave hello modified role definition.</span></span>

<span data-ttu-id="5bc2e-178">Hallo volgende voorbeeld wordt toegevoegd Hallo `Microsoft.Insights/diagnosticSettings/*` bewerking toohello *virtuele Machine Operator* aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-178">hello following example adds hello `Microsoft.Insights/diagnosticSettings/*` operation toohello *Virtual Machine Operator* custom role.</span></span>

```
$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.Actions.Add("Microsoft.Insights/diagnosticSettings/*")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-1.png)

<span data-ttu-id="5bc2e-180">Hallo volgende voorbeeld wordt een Azure-abonnement toohello toewijsbare bereiken Hallo *virtuele Machine Operator* aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-180">hello following example adds an Azure subscription toohello assignable scopes of hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmSubscription - SubscriptionName Production3

$role = Get-AzureRmRoleDefinition "Virtual Machine Operator"
$role.AssignableScopes.Add("/subscriptions/34370e90-ac4a-4bf9-821f-85eeedead1a2")
Set-AzureRmRoleDefinition -Role $role
```

![RBAC PowerShell - Set-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/3-set-azurermroledefinition-2.png)

### <a name="modify-role-with-json-template"></a><span data-ttu-id="5bc2e-182">Rol met JSON-sjabloon wijzigen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-182">Modify role with JSON template</span></span>
<span data-ttu-id="5bc2e-183">Hallo vorige JSON-sjabloon gebruikt, kunt u eenvoudig een bestaande aangepaste rol tooadd wijzigen of verwijderen van acties.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-183">Using hello previous JSON template, you can easily modify an existing custom role tooadd or remove Actions.</span></span> <span data-ttu-id="5bc2e-184">Hallo JSON-sjabloon bijwerken en toevoegen van Hallo lezen actie die netwerken, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-184">Update hello JSON template and add hello read action for networking as shown in hello following example.</span></span> <span data-ttu-id="5bc2e-185">Hallo-definities op Hallo sjabloon zijn niet cumulatief toegepaste tooan bestaande definitie, wat betekent dat die rol Hallo verschijnt precies zoals u in de sjabloon Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-185">hello definitions listed in hello template are not cumulatively applied tooan existing definition, meaning that hello role appears exactly as you specify in hello template.</span></span> <span data-ttu-id="5bc2e-186">U moet ook tooupdate Hallo-Id-veld met Hallo Hallo rol-ID.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-186">You also need tooupdate hello Id field with hello ID of hello role.</span></span> <span data-ttu-id="5bc2e-187">Als u niet zeker weet wat deze waarde is, kunt u Hallo `Get-AzureRmRoleDefinition` cmdlet tooget deze informatie.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-187">If you aren't sure what this value is, you can use hello `Get-AzureRmRoleDefinition` cmdlet tooget this information.</span></span>

```
{
  "Name": "Custom Role 1",
  "Id": "acce7ded-2559-449d-bcd5-e9604e50bad1",
  "IsCustom": true,
  "Description": "Allows for read access tooAzure storage and compute resources and access toosupport",
  "Actions": [
    "Microsoft.Compute/*/read",
    "Microsoft.Storage/*/read",
    "Microsoft.Network/*/read",
    "Microsoft.Support/*"
  ],
  "NotActions": [
  ],
  "AssignableScopes": [
    "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "/subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624"
  ]
}
```

<span data-ttu-id="5bc2e-188">tooupdate hello bestaande rol, Hallo volgende PowerShell-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5bc2e-188">tooupdate hello existing role, run hello following PowerShell command:</span></span>
```
Set-AzureRmRoleDefinition -InputFile "C:\CustomRoles\customrole1.json"
```

## <a name="delete-a-custom-role"></a><span data-ttu-id="5bc2e-189">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-189">Delete a custom role</span></span>
<span data-ttu-id="5bc2e-190">een aangepaste beveiligingsrol toodelete gebruiken Hallo `Remove-AzureRmRoleDefinition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-190">toodelete a custom role, use hello `Remove-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="5bc2e-191">Hallo volgende voorbeeld wordt verwijderd Hallo *virtuele Machine Operator* aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-191">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

```
Get-AzureRmRoleDefinition "Virtual Machine Operator"

Get-AzureRmRoleDefinition "Virtual Machine Operator" | Remove-AzureRmRoleDefinition
```

![RBAC PowerShell - Remove-AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/4-remove-azurermroledefinition.png)

## <a name="list-custom-roles"></a><span data-ttu-id="5bc2e-193">Lijst met aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="5bc2e-193">List custom roles</span></span>
<span data-ttu-id="5bc2e-194">toolist hello functies die beschikbaar zijn voor toewijzing op een scope gebruiken Hallo `Get-AzureRmRoleDefinition` opdracht.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-194">toolist hello roles that are available for assignment at a scope, use hello `Get-AzureRmRoleDefinition` command.</span></span>

<span data-ttu-id="5bc2e-195">Hallo volgende voorbeeld worden alle functies die beschikbaar voor toewijzing in Hallo geselecteerde abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-195">hello following example lists all roles that are available for assignment in hello selected subscription.</span></span>

```
Get-AzureRmRoleDefinition | FT Name, IsCustom
```

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition-1.png)

<span data-ttu-id="5bc2e-197">Hallo in Hallo voorbeeld te volgen, *virtuele Machine Operator* aangepaste rol is niet beschikbaar in Hallo *Production4* abonnement omdat dat abonnement niet Hallo  **AssignableScopes** van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="5bc2e-197">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

![RBAC PowerShell-Get AzureRmRoleDefinition - schermafbeelding](./media/role-based-access-control-manage-access-powershell/5-get-azurermroledefinition2.png)

## <a name="see-also"></a><span data-ttu-id="5bc2e-199">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5bc2e-199">See also</span></span>
* <span data-ttu-id="5bc2e-200">[Azure PowerShell gebruiken met Azure Resource Manager](../powershell-azure-resource-manager.md)
  [!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span><span class="sxs-lookup"><span data-stu-id="5bc2e-200">[Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md)
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]</span></span>

