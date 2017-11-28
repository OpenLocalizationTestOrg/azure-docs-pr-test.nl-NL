---
title: Beheren van op rollen gebaseerde toegangsbeheer (RBAC) met Azure CLI | Microsoft Docs
description: Informatie over het beheren van op rollen gebaseerde toegangsbeheer (RBAC) met de Azure-opdrachtregelinterface lijst met functies en functie acties en rollen toewijzen aan de scopes abonnement en de toepassing.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 3483ee01-8177-49e7-b337-4d5cb14f5e32
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: ad644de6d23950e699d99042d27381336626caab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-azure-command-line-interface"></a><span data-ttu-id="90f43-103">Toegangsbeheer op basis van rollen met de Azure-opdrachtregelinterface beheren</span><span class="sxs-lookup"><span data-stu-id="90f43-103">Manage Role-Based Access Control with the Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="90f43-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90f43-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="90f43-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="90f43-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="90f43-106">REST API</span><span class="sxs-lookup"><span data-stu-id="90f43-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="90f43-107">U kunt op rollen gebaseerde toegangsbeheer (RBAC) in de Azure portal en Azure Resource Manager-API gebruiken voor het beheren van toegang tot uw abonnement en bronnen op een heel nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="90f43-107">You can use Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API to manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="90f43-108">Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door sommige rollen toewijzen aan deze bij een bepaald bereik.</span><span class="sxs-lookup"><span data-stu-id="90f43-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

<span data-ttu-id="90f43-109">Voordat u de Azure-opdrachtregelinterface (CLI) gebruiken kunt voor het beheren van RBAC, hebt u de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="90f43-109">Before you can use the Azure command-line interface (CLI) to manage RBAC, you must have the following prerequisites:</span></span>

* <span data-ttu-id="90f43-110">Azure CLI versie 0.8.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="90f43-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="90f43-111">Zie voor het installeren van de meest recente versie en deze koppelen aan uw Azure-abonnement, [installeren en configureren van de Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="90f43-111">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="90f43-112">Azure Resource Manager in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="90f43-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="90f43-113">Ga naar [met de Azure CLI met Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="90f43-113">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="90f43-114">Lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="90f43-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="90f43-115">Lijst van alle beschikbare rollen</span><span class="sxs-lookup"><span data-stu-id="90f43-115">List all available roles</span></span>
<span data-ttu-id="90f43-116">U kunt alle beschikbare rollen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-116">To list all available roles, use:</span></span>

        azure role list

<span data-ttu-id="90f43-117">Het volgende voorbeeld ziet u de lijst met *alle beschikbare rollen*.</span><span class="sxs-lookup"><span data-stu-id="90f43-117">The following example shows the list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="90f43-119">Van Lijstacties van een rol</span><span class="sxs-lookup"><span data-stu-id="90f43-119">List actions of a role</span></span>
<span data-ttu-id="90f43-120">U kunt de acties van een rol gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-120">To list the actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="90f43-121">Het volgende voorbeeld ziet u de acties van de *Inzender* en *Virtual Machine Contributor* rollen.</span><span class="sxs-lookup"><span data-stu-id="90f43-121">The following example shows the actions of the *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Azure RBAC opdrachtregel - functie van azure weergeven - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="90f43-123">Lijst met toegang</span><span class="sxs-lookup"><span data-stu-id="90f43-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="90f43-124">Roltoewijzingen lijst effectieve op een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="90f43-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="90f43-125">U kunt de roltoewijzingen die aanwezig zijn in een resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-125">To list the role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="90f43-126">Het volgende voorbeeld ziet u de roltoewijzingen in de *pharma-verkoop-projecforcast* groep.</span><span class="sxs-lookup"><span data-stu-id="90f43-126">The following example shows the role assignments in the *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzing-lijst per groep functie van azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="90f43-128">Lijst roltoewijzingen voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="90f43-128">List role assignments for a user</span></span>
<span data-ttu-id="90f43-129">U kunt de roltoewijzingen voor een specifieke gebruiker en de toewijzingen die zijn toegewezen aan een gebruiker groepen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-129">To list the role assignments for a specific user and the assignments that are assigned to a user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="90f43-130">U ziet ook roltoewijzingen die zijn overgenomen van groepen doordat de opdracht:</span><span class="sxs-lookup"><span data-stu-id="90f43-130">You can also see role assignments that are inherited from groups by modifying the command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="90f43-131">Het volgende voorbeeld ziet u de roltoewijzingen die zijn verleend aan de  *sameert@aaddemo.com*  gebruiker.</span><span class="sxs-lookup"><span data-stu-id="90f43-131">The following example shows the role assignments that are granted to the *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="90f43-132">Dit omvat functies die rechtstreeks aan de gebruiker zijn toegewezen en functies die zijn overgenomen van groepen.</span><span class="sxs-lookup"><span data-stu-id="90f43-132">This includes roles that are assigned directly to the user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzingslijst azure rol door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="90f43-134">Toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="90f43-134">Grant access</span></span>
<span data-ttu-id="90f43-135">Om toegang te verlenen nadat u hebt aangegeven dat de rol die u wilt toewijzen, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-135">To grant access after you have identified the role that you want to assign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-to-group-at-the-subscription-scope"></a><span data-ttu-id="90f43-136">Een rol toewijzen aan de groep in het abonnementsbereik</span><span class="sxs-lookup"><span data-stu-id="90f43-136">Assign a role to group at the subscription scope</span></span>
<span data-ttu-id="90f43-137">Als u wilt een rol toewijzen aan een groep in het abonnementsbereik, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-137">To assign a role to a group at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="90f43-138">Het volgende voorbeeld wordt de *lezer* rol *van Christine Koch Team* op de *abonnement* bereik.</span><span class="sxs-lookup"><span data-stu-id="90f43-138">The following example assigns the *Reader* role to *Christine Koch's Team* at the *subscription* scope.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-to-an-application-at-the-subscription-scope"></a><span data-ttu-id="90f43-140">Een rol toewijzen aan een toepassing op het abonnementsbereik</span><span class="sxs-lookup"><span data-stu-id="90f43-140">Assign a role to an application at the subscription scope</span></span>
<span data-ttu-id="90f43-141">Als u wilt een rol toewijzen aan een toepassing op het abonnementsbereik, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-141">To assign a role to an application at the subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="90f43-142">Het volgende voorbeeld verleent de *Inzender* role in een *Azure AD* toepassing op het geselecteerde abonnement.</span><span class="sxs-lookup"><span data-stu-id="90f43-142">The following example grants the *Contributor* role to an *Azure AD* application on the selected subscription.</span></span>

 ![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door toepassing](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-to-a-user-at-the-resource-group-scope"></a><span data-ttu-id="90f43-144">Een rol toewijzen aan een gebruiker op het groepsbereik resource</span><span class="sxs-lookup"><span data-stu-id="90f43-144">Assign a role to a user at the resource group scope</span></span>
<span data-ttu-id="90f43-145">Als u wilt een rol toewijzen aan een gebruiker op het groepsbereik resource, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-145">To assign a role to a user at the resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="90f43-146">Het volgende voorbeeld verleent de *Virtual Machine Contributor* rol  *samert@aaddemo.com*  gebruiker op de *Pharma-verkoop-ProjectForcast* resource groepsbereik.</span><span class="sxs-lookup"><span data-stu-id="90f43-146">The following example grants the *Virtual Machine Contributor* role to *samert@aaddemo.com* user at the *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-to-a-group-at-the-resource-scope"></a><span data-ttu-id="90f43-148">Een rol toewijzen aan een groep in het bereik van de resource</span><span class="sxs-lookup"><span data-stu-id="90f43-148">Assign a role to a group at the resource scope</span></span>
<span data-ttu-id="90f43-149">Als u wilt een rol toewijzen aan een groep voor de resource-scope, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-149">To assign a role to a group at the resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="90f43-150">Het volgende voorbeeld verleent de *Virtual Machine Contributor* role in een *Azure AD* groep op een *subnet*.</span><span class="sxs-lookup"><span data-stu-id="90f43-150">The following example grants the *Virtual Machine Contributor* role to an *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="90f43-152">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="90f43-152">Remove access</span></span>
<span data-ttu-id="90f43-153">Als u wilt verwijderen een roltoewijzing, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90f43-153">To remove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id to from which to remove role> --roleName "<role name>"

<span data-ttu-id="90f43-154">Het volgende voorbeeld verwijdert u de *Virtual Machine Contributor* functietoewijzing uit de  *sammert@aaddemo.com*  gebruiker op de *Pharma-verkoop-ProjectForcast* resource groep.</span><span class="sxs-lookup"><span data-stu-id="90f43-154">The following example removes the *Virtual Machine Contributor* role assignment from the *sammert@aaddemo.com* user on the *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="90f43-155">Het voorbeeld wordt de roltoewijzing vervolgens verwijderd uit een groep op het abonnement.</span><span class="sxs-lookup"><span data-stu-id="90f43-155">The example then removes the role assignment from a group on the subscription.</span></span>

![Azure RBAC opdrachtregel - azure-functie toewijzing delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="90f43-157">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="90f43-157">Create a custom role</span></span>
<span data-ttu-id="90f43-158">Gebruik het volgende voor het maken van een aangepaste rol:</span><span class="sxs-lookup"><span data-stu-id="90f43-158">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="90f43-159">Het volgende voorbeeld wordt een aangepaste beveiligingsrol aangeroepen *virtuele Machine Operator*.</span><span class="sxs-lookup"><span data-stu-id="90f43-159">The following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="90f43-160">Deze aangepaste rol verleent toegang tot alle leesbewerkingen van *Microsoft.Compute*, *Microsoft.Storage*, en *Microsoft.Network* resourceproviders en verleent toegang tot Start, opnieuw opstarten en controleren van de virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="90f43-160">This custom role grants access to all read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access to start, restart, and monitor virtual machines.</span></span> <span data-ttu-id="90f43-161">Deze aangepaste rol kan worden gebruikt in twee abonnementen.</span><span class="sxs-lookup"><span data-stu-id="90f43-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="90f43-162">Dit voorbeeld wordt een JSON-bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="90f43-162">This example uses a JSON file as an input.</span></span>

![JSON - aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure vanaf de opdrachtregel - azure-functie maken - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="90f43-165">Een aangepaste rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="90f43-165">Modify a custom role</span></span>
<span data-ttu-id="90f43-166">Voor het wijzigen van een aangepaste rol voor het eerst gebruiken de `azure role show` opdracht roldefinitie ophalen.</span><span class="sxs-lookup"><span data-stu-id="90f43-166">To modify a custom role, first use the `azure role show` command to retrieve role definition.</span></span> <span data-ttu-id="90f43-167">Controleer vervolgens de gewenste wijzigingen aan in het definitiebestand voor de rol.</span><span class="sxs-lookup"><span data-stu-id="90f43-167">Second, make the desired changes to the role definition file.</span></span> <span data-ttu-id="90f43-168">Gebruik tot slot `azure role set` de gewijzigde roldefinitie opslaan.</span><span class="sxs-lookup"><span data-stu-id="90f43-168">Finally, use `azure role set` to save the modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="90f43-169">Het volgende voorbeeld wordt de *Microsoft.Insights/diagnosticSettings/* bewerking is de **acties**, en een Azure-abonnement de **AssignableScopes** van de De aangepaste rol virtuele Machine-Operator.</span><span class="sxs-lookup"><span data-stu-id="90f43-169">The following example adds the *Microsoft.Insights/diagnosticSettings/* operation to the **Actions**, and an Azure subscription to the **AssignableScopes** of the Virtual Machine Operator custom role.</span></span>

![JSON - wijzigen aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Azure RBAC opdrachtregel - azure-functie set - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="90f43-172">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="90f43-172">Delete a custom role</span></span>
<span data-ttu-id="90f43-173">U verwijdert een aangepaste rol door eerst gebruiken de `azure role show` opdracht om te bepalen de **ID** van de rol.</span><span class="sxs-lookup"><span data-stu-id="90f43-173">To delete a custom role, first use the `azure role show` command to determine the **ID** of the role.</span></span> <span data-ttu-id="90f43-174">Gebruik vervolgens de `azure role delete` opdracht voor het verwijderen van de rol door op te geven de **ID**.</span><span class="sxs-lookup"><span data-stu-id="90f43-174">Then, use the `azure role delete` command to delete the role by specifying the **ID**.</span></span>

<span data-ttu-id="90f43-175">Het volgende voorbeeld verwijdert u de *virtuele Machine Operator* aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="90f43-175">The following example removes the *Virtual Machine Operator* custom role.</span></span>

![Azure RBAC opdrachtregel - azure-functie delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="90f43-177">Lijst met aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="90f43-177">List custom roles</span></span>
<span data-ttu-id="90f43-178">Als de functies die beschikbaar voor toewijzing op een scope zijn wilt weergeven, gebruikt de `azure role list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="90f43-178">To list the roles that are available for assignment at a scope, use the `azure role list` command.</span></span>

<span data-ttu-id="90f43-179">De volgende opdracht worden alle functies die beschikbaar voor toewijzing in het geselecteerde abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="90f43-179">The following command lists all roles that are available for assignment in the selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="90f43-181">In het volgende voorbeeld wordt de *virtuele Machine Operator* aangepaste rol is niet beschikbaar in de *Production4* abonnement omdat dat abonnement bevindt zich niet in de **AssignableScopes** van de rol.</span><span class="sxs-lookup"><span data-stu-id="90f43-181">In the following example, the *Virtual Machine Operator* custom role isn’t available in the *Production4* subscription because that subscription isn’t in the **AssignableScopes** of the role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Azure RBAC opdrachtregel - lijst met azure-functie voor aangepaste rollen - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="90f43-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90f43-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

