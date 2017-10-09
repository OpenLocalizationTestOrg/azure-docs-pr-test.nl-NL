---
title: aaaManage op rollen gebaseerde toegangsbeheer (RBAC) met Azure CLI | Microsoft Docs
description: Meer informatie over hoe toomanage op rollen gebaseerde toegangsbeheer (RBAC) Hello Azure opdrachtregelprogramma interface door functies van de aanbieding en rol acties en door het toewijzen van rollen toohello abonnement en de toepassing bereiken.
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
ms.openlocfilehash: 438418e5f6ee9b98908c9c264d516eb722a4e26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-azure-command-line-interface"></a><span data-ttu-id="74400-103">Toegangsbeheer op basis van rollen met hello Azure-opdrachtregelinterface beheren</span><span class="sxs-lookup"><span data-stu-id="74400-103">Manage Role-Based Access Control with hello Azure command-line interface</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74400-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="74400-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="74400-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="74400-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="74400-106">REST API</span><span class="sxs-lookup"><span data-stu-id="74400-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)


<span data-ttu-id="74400-107">In hello Azure-portal en Azure Resource Manager-API toomanage toegang tooyour abonnement en bronnen op een heel nauwkeurig kunt u rollen gebaseerd toegangsbeheer (RBAC).</span><span class="sxs-lookup"><span data-stu-id="74400-107">You can use Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API toomanage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="74400-108">Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.</span><span class="sxs-lookup"><span data-stu-id="74400-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

<span data-ttu-id="74400-109">Voordat u hello Azure-opdrachtregelinterface (CLI) toomanage RBAC gebruiken kunt, hebt u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="74400-109">Before you can use hello Azure command-line interface (CLI) toomanage RBAC, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="74400-110">Azure CLI versie 0.8.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="74400-110">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="74400-111">meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="74400-111">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="74400-112">Azure Resource Manager in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="74400-112">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="74400-113">Ga te[Using hello Azure CLI Hello Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="74400-113">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

## <a name="list-roles"></a><span data-ttu-id="74400-114">Lijst met rollen</span><span class="sxs-lookup"><span data-stu-id="74400-114">List roles</span></span>
### <a name="list-all-available-roles"></a><span data-ttu-id="74400-115">Lijst van alle beschikbare rollen</span><span class="sxs-lookup"><span data-stu-id="74400-115">List all available roles</span></span>
<span data-ttu-id="74400-116">toolist gebruiken voor alle beschikbare rollen:</span><span class="sxs-lookup"><span data-stu-id="74400-116">toolist all available roles, use:</span></span>

        azure role list

<span data-ttu-id="74400-117">Hallo volgende voorbeeld ziet u Hallo lijst met *alle beschikbare rollen*.</span><span class="sxs-lookup"><span data-stu-id="74400-117">hello following example shows hello list of *all available roles*.</span></span>

```
azure role list --json | jq '.[] | {"roleName":.properties.roleName, "description":.properties.description}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-list.png)

### <a name="list-actions-of-a-role"></a><span data-ttu-id="74400-119">Van Lijstacties van een rol</span><span class="sxs-lookup"><span data-stu-id="74400-119">List actions of a role</span></span>
<span data-ttu-id="74400-120">toolist hello acties van een functie, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74400-120">toolist hello actions of a role, use:</span></span>

    azure role show "<role name>"

<span data-ttu-id="74400-121">Hallo volgende voorbeeld ziet u acties Hallo Hallo *Inzender* en *Virtual Machine Contributor* rollen.</span><span class="sxs-lookup"><span data-stu-id="74400-121">hello following example shows hello actions of hello *Contributor* and *Virtual Machine Contributor* roles.</span></span>

```
azure role show "contributor" --json | jq '.[] | {"Actions":.properties.permissions[0].actions,"NotActions":properties.permissions[0].notActions}'

azure role show "virtual machine contributor" --json | jq '.[] | .properties.permissions[0].actions'
```

![Azure RBAC opdrachtregel - functie van azure weergeven - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/1-azure-role-show.png)

## <a name="list-access"></a><span data-ttu-id="74400-123">Lijst met toegang</span><span class="sxs-lookup"><span data-stu-id="74400-123">List access</span></span>
### <a name="list-role-assignments-effective-on-a-resource-group"></a><span data-ttu-id="74400-124">Roltoewijzingen lijst effectieve op een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="74400-124">List role assignments effective on a resource group</span></span>
<span data-ttu-id="74400-125">toolist hello roltoewijzingen die aanwezig zijn in een resourcegroep of gebruik:</span><span class="sxs-lookup"><span data-stu-id="74400-125">toolist hello role assignments that exist in a resource group, use:</span></span>

    azure role assignment list --resource-group <resource group name>

<span data-ttu-id="74400-126">Hallo in volgende voorbeeld ziet roltoewijzingen Hallo Hallo *pharma-verkoop-projecforcast* groep.</span><span class="sxs-lookup"><span data-stu-id="74400-126">hello following example shows hello role assignments in hello *pharma-sales-projecforcast* group.</span></span>

```
azure role assignment list --resource-group pharma-sales-projecforcast --json | jq '.[] | {"DisplayName":.properties.aADObject.displayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzing-lijst per groep functie van azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-1.png)

### <a name="list-role-assignments-for-a-user"></a><span data-ttu-id="74400-128">Lijst roltoewijzingen voor een gebruiker</span><span class="sxs-lookup"><span data-stu-id="74400-128">List role assignments for a user</span></span>
<span data-ttu-id="74400-129">toolist hello roltoewijzingen voor een specifieke gebruiker en het Hallo-toewijzingen die zijn toegewezen tooa gebruikersgroepen, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74400-129">toolist hello role assignments for a specific user and hello assignments that are assigned tooa user's groups, use:</span></span>

    azure role assignment list --signInName <user email>

<span data-ttu-id="74400-130">U ziet ook roltoewijzingen die zijn overgenomen van groepen doordat Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="74400-130">You can also see role assignments that are inherited from groups by modifying hello command:</span></span>

    azure role assignment list --expandPrincipalGroups --signInName <user email>

<span data-ttu-id="74400-131">Hallo volgende voorbeeld ziet u Hallo roltoewijzingen die worden verleend toohello  *sameert@aaddemo.com*  gebruiker.</span><span class="sxs-lookup"><span data-stu-id="74400-131">hello following example shows hello role assignments that are granted toohello *sameert@aaddemo.com* user.</span></span> <span data-ttu-id="74400-132">Dit omvat functies die rechtstreeks toohello gebruiker zijn toegewezen en functies die zijn overgenomen van groepen.</span><span class="sxs-lookup"><span data-stu-id="74400-132">This includes roles that are assigned directly toohello user and roles that are inherited from groups.</span></span>

```
azure role assignment list --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'

azure role assignment list --expandPrincipalGroups --signInName sameert@aaddemo.com --json | jq '.[] | {"DisplayName":.properties.aADObject.DisplayName,"RoleDefinitionName":.properties.roleName,"Scope":.properties.scope}'
```

![Azure RBAC opdrachtregel - toewijzingslijst azure rol door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-assignment-list-2.png)

## <a name="grant-access"></a><span data-ttu-id="74400-134">Toegang verlenen</span><span class="sxs-lookup"><span data-stu-id="74400-134">Grant access</span></span>
<span data-ttu-id="74400-135">toogrant toegang nadat u hebt aangegeven dat u wilt dat tooassign Hallo-rol, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74400-135">toogrant access after you have identified hello role that you want tooassign, use:</span></span>

    azure role assignment create

### <a name="assign-a-role-toogroup-at-hello-subscription-scope"></a><span data-ttu-id="74400-136">Een rol toogroup op Hallo abonnementsbereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="74400-136">Assign a role toogroup at hello subscription scope</span></span>
<span data-ttu-id="74400-137">een groep rol tooa bij Hallo abonnementsbereik, gebruik tooassign:</span><span class="sxs-lookup"><span data-stu-id="74400-137">tooassign a role tooa group at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <group object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="74400-138">Hallo volgende voorbeeld wordt toegewezen Hallo *lezer* rol te*van Christine Koch Team* op Hallo *abonnement* bereik.</span><span class="sxs-lookup"><span data-stu-id="74400-138">hello following example assigns hello *Reader* role too*Christine Koch's Team* at hello *subscription* scope.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-1.png)

### <a name="assign-a-role-tooan-application-at-hello-subscription-scope"></a><span data-ttu-id="74400-140">Een rol tooan toepassing in het bereik van Hallo abonnement toewijzen</span><span class="sxs-lookup"><span data-stu-id="74400-140">Assign a role tooan application at hello subscription scope</span></span>
<span data-ttu-id="74400-141">een rol tooan toepassing bij Hallo abonnementsbereik, gebruik tooassign:</span><span class="sxs-lookup"><span data-stu-id="74400-141">tooassign a role tooan application at hello subscription scope, use:</span></span>

    azure role assignment create --objectId  <applications object id> --roleName <name of role> --subscription <subscription> --scope <subscription/subscription id>

<span data-ttu-id="74400-142">Hallo volgende voorbeeld verleent Hallo *Inzender* rol tooan *Azure AD* toepassing op Hallo abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="74400-142">hello following example grants hello *Contributor* role tooan *Azure AD* application on hello selected subscription.</span></span>

 ![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door toepassing](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-2.png)

### <a name="assign-a-role-tooa-user-at-hello-resource-group-scope"></a><span data-ttu-id="74400-144">Een gebruiker van de rol tooa op Hallo resource groepsbereik toewijzen</span><span class="sxs-lookup"><span data-stu-id="74400-144">Assign a role tooa user at hello resource group scope</span></span>
<span data-ttu-id="74400-145">een gebruiker van de rol tooa op Hallo resource groepsbereik gebruik tooassign:</span><span class="sxs-lookup"><span data-stu-id="74400-145">tooassign a role tooa user at hello resource group scope, use:</span></span>

    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>

<span data-ttu-id="74400-146">Hallo volgende voorbeeld verleent Hallo *Virtual Machine Contributor* rol te *samert@aaddemo.com*  gebruiker op Hallo *Pharma-verkoop-ProjectForcast* resource groepsbereik.</span><span class="sxs-lookup"><span data-stu-id="74400-146">hello following example grants hello *Virtual Machine Contributor* role too*samert@aaddemo.com* user at hello *Pharma-Sales-ProjectForcast* resource group scope.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door gebruiker - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-3.png)

### <a name="assign-a-role-tooa-group-at-hello-resource-scope"></a><span data-ttu-id="74400-148">Een groep rol tooa bij Hallo resource bereik worden toegewezen</span><span class="sxs-lookup"><span data-stu-id="74400-148">Assign a role tooa group at hello resource scope</span></span>
<span data-ttu-id="74400-149">een groep rol tooa bij Hallo resource bereik, gebruik tooassign:</span><span class="sxs-lookup"><span data-stu-id="74400-149">tooassign a role tooa group at hello resource scope, use:</span></span>

    azure role assignment create --objectId <group id> --role "<name of role>" --resource-name <resource group name> --resource-type <resource group type> --parent <resource group parent> --resource-group <resource group>

<span data-ttu-id="74400-150">Hallo volgende voorbeeld verleent Hallo *Virtual Machine Contributor* rol tooan *Azure AD* groep op een *subnet*.</span><span class="sxs-lookup"><span data-stu-id="74400-150">hello following example grants hello *Virtual Machine Contributor* role tooan *Azure AD* group on a *subnet*.</span></span>

![RBAC Azure vanaf de opdrachtregel - azure roltoewijzing maken door de groep - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-assignment-create-4.png)

## <a name="remove-access"></a><span data-ttu-id="74400-152">Toegang verwijderen</span><span class="sxs-lookup"><span data-stu-id="74400-152">Remove access</span></span>
<span data-ttu-id="74400-153">een roltoewijzing tooremove gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74400-153">tooremove a role assignment, use:</span></span>

    azure role assignment delete --objectId <object id toofrom which tooremove role> --roleName "<role name>"

<span data-ttu-id="74400-154">Hallo volgende voorbeeld wordt verwijderd Hallo *Virtual Machine Contributor* functietoewijzing uit Hallo  *sammert@aaddemo.com*  gebruiker op Hallo *Pharma-verkoop-ProjectForcast* resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="74400-154">hello following example removes hello *Virtual Machine Contributor* role assignment from hello *sammert@aaddemo.com* user on hello *Pharma-Sales-ProjectForcast* resource group.</span></span>
<span data-ttu-id="74400-155">de roltoewijzing Hallo verwijdert Hallo voorbeeld uit een groep op Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="74400-155">hello example then removes hello role assignment from a group on hello subscription.</span></span>

![Azure RBAC opdrachtregel - azure-functie toewijzing delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-assignment-delete.png)

## <a name="create-a-custom-role"></a><span data-ttu-id="74400-157">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="74400-157">Create a custom role</span></span>
<span data-ttu-id="74400-158">een aangepaste beveiligingsrol toocreate gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74400-158">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

<span data-ttu-id="74400-159">Hallo volgende voorbeeld maakt u een aangepaste beveiligingsrol aangeroepen *virtuele Machine Operator*.</span><span class="sxs-lookup"><span data-stu-id="74400-159">hello following example creates a custom role called *Virtual Machine Operator*.</span></span> <span data-ttu-id="74400-160">Deze aangepaste rol verleent toegang tooall leesbewerkingen van *Microsoft.Compute*, *Microsoft.Storage*, en *Microsoft.Network* providers en verleent toegang tot bedrijfsbronnen toostart, opnieuw opstarten en virtuele machines bewaken.</span><span class="sxs-lookup"><span data-stu-id="74400-160">This custom role grants access tooall read operations of *Microsoft.Compute*, *Microsoft.Storage*, and *Microsoft.Network* resource providers and grants access toostart, restart, and monitor virtual machines.</span></span> <span data-ttu-id="74400-161">Deze aangepaste rol kan worden gebruikt in twee abonnementen.</span><span class="sxs-lookup"><span data-stu-id="74400-161">This custom role can be used in two subscriptions.</span></span> <span data-ttu-id="74400-162">Dit voorbeeld wordt een JSON-bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="74400-162">This example uses a JSON file as an input.</span></span>

![JSON - aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-1.png)

![RBAC Azure vanaf de opdrachtregel - azure-functie maken - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/2-azure-role-create-2.png)

## <a name="modify-a-custom-role"></a><span data-ttu-id="74400-165">Een aangepaste rol wijzigen</span><span class="sxs-lookup"><span data-stu-id="74400-165">Modify a custom role</span></span>
<span data-ttu-id="74400-166">een aangepaste beveiligingsrol toomodify Hallo voor het eerst gebruiken `azure role show` opdracht tooretrieve roldefinitie.</span><span class="sxs-lookup"><span data-stu-id="74400-166">toomodify a custom role, first use hello `azure role show` command tooretrieve role definition.</span></span> <span data-ttu-id="74400-167">Controleer vervolgens Hallo gewenste wijzigingen aan toohello rol-definitiebestand.</span><span class="sxs-lookup"><span data-stu-id="74400-167">Second, make hello desired changes toohello role definition file.</span></span> <span data-ttu-id="74400-168">Gebruik tot slot `azure role set` toosave Hallo roldefinitie gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="74400-168">Finally, use `azure role set` toosave hello modified role definition.</span></span>

    azure role set --inputfile <file path>

<span data-ttu-id="74400-169">Hallo volgende voorbeeld wordt toegevoegd Hallo *Microsoft.Insights/diagnosticSettings/* bewerking toohello **acties**, en een Azure-abonnement toohello **AssignableScopes**van aangepaste rol van Hallo Operator van de virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="74400-169">hello following example adds hello *Microsoft.Insights/diagnosticSettings/* operation toohello **Actions**, and an Azure subscription toohello **AssignableScopes** of hello Virtual Machine Operator custom role.</span></span>

![JSON - wijzigen aangepaste roldefinitie - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set-1.png)

![Azure RBAC opdrachtregel - azure-functie set - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/3-azure-role-set2.png)

## <a name="delete-a-custom-role"></a><span data-ttu-id="74400-172">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="74400-172">Delete a custom role</span></span>
<span data-ttu-id="74400-173">een aangepaste beveiligingsrol toodelete Hallo voor het eerst gebruiken `azure role show` opdracht toodetermine hello **ID** van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="74400-173">toodelete a custom role, first use hello `azure role show` command toodetermine hello **ID** of hello role.</span></span> <span data-ttu-id="74400-174">Gebruik vervolgens Hallo `azure role delete` opdracht toodelete Hallo rol door op te geven Hallo **ID**.</span><span class="sxs-lookup"><span data-stu-id="74400-174">Then, use hello `azure role delete` command toodelete hello role by specifying hello **ID**.</span></span>

<span data-ttu-id="74400-175">Hallo volgende voorbeeld wordt verwijderd Hallo *virtuele Machine Operator* aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="74400-175">hello following example removes hello *Virtual Machine Operator* custom role.</span></span>

![Azure RBAC opdrachtregel - azure-functie delete - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/4-azure-role-delete.png)

## <a name="list-custom-roles"></a><span data-ttu-id="74400-177">Lijst met aangepaste rollen</span><span class="sxs-lookup"><span data-stu-id="74400-177">List custom roles</span></span>
<span data-ttu-id="74400-178">toolist hello functies die beschikbaar zijn voor toewijzing op een scope gebruiken Hallo `azure role list` opdracht.</span><span class="sxs-lookup"><span data-stu-id="74400-178">toolist hello roles that are available for assignment at a scope, use hello `azure role list` command.</span></span>

<span data-ttu-id="74400-179">Hallo volgende opdracht geeft een lijst van alle functies die beschikbaar voor toewijzing in Hallo geselecteerde abonnement zijn.</span><span class="sxs-lookup"><span data-stu-id="74400-179">hello following command lists all roles that are available for assignment in hello selected subscription.</span></span>

```
azure role list --json | jq '.[] | {"name":.properties.roleName, type:.properties.type}'
```

![Azure RBAC opdrachtregel - lijst van de functie van de azure - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list1.png)

<span data-ttu-id="74400-181">Hallo in Hallo voorbeeld te volgen, *virtuele Machine Operator* aangepaste rol is niet beschikbaar in Hallo *Production4* abonnement omdat dat abonnement niet Hallo  **AssignableScopes** van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="74400-181">In hello following example, hello *Virtual Machine Operator* custom role isn’t available in hello *Production4* subscription because that subscription isn’t in hello **AssignableScopes** of hello role.</span></span>

```
azure role list --json | jq '.[] | if .properties.type == "CustomRole" then .properties.roleName else empty end'
```

![Azure RBAC opdrachtregel - lijst met azure-functie voor aangepaste rollen - schermafbeelding](./media/role-based-access-control-manage-access-azure-cli/5-azure-role-list2.png)

## <a name="next-steps"></a><span data-ttu-id="74400-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74400-183">Next steps</span></span>
[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]

