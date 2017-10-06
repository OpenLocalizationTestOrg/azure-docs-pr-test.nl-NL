---
title: Toegangsbeheer op basis van aaaRole met REST - Azure AD | Microsoft Docs
description: Toegangsbeheer op basis van rollen met Hallo REST-API beheren
services: active-directory
documentationcenter: na
author: andredm7
manager: femila
editor: 
ms.assetid: 1f90228a-7aac-4ea7-ad82-b57d222ab128
ms.service: active-directory
ms.workload: multiple
ms.tgt_pltfrm: rest-api
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: andredm
ms.openlocfilehash: ccd402fd4fe4583288076cac23753dd067694681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-role-based-access-control-with-hello-rest-api"></a><span data-ttu-id="bc429-103">Toegangsbeheer op basis van rollen met Hallo REST-API beheren</span><span class="sxs-lookup"><span data-stu-id="bc429-103">Manage Role-Based Access Control with hello REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc429-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc429-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="bc429-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="bc429-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="bc429-106">REST API</span><span class="sxs-lookup"><span data-stu-id="bc429-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="bc429-107">Op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure-portal en Azure Resource Manager-API kunt u access tooyour abonnement en bronnen op een heel nauwkeurig beheren.</span><span class="sxs-lookup"><span data-stu-id="bc429-107">Role-Based Access Control (RBAC) in hello Azure portal and Azure Resource Manager API helps you manage access tooyour subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="bc429-108">Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door toe te wijzen van sommige rollen toothem bij een bepaald bereik.</span><span class="sxs-lookup"><span data-stu-id="bc429-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles toothem at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="bc429-109">Lijst van alle roltoewijzingen</span><span class="sxs-lookup"><span data-stu-id="bc429-109">List all role assignments</span></span>
<span data-ttu-id="bc429-110">Een lijst met alle Hallo roltoewijzingen op Hallo opgegeven bereik en subscopes.</span><span class="sxs-lookup"><span data-stu-id="bc429-110">Lists all hello role assignments at hello specified scope and subscopes.</span></span>

<span data-ttu-id="bc429-111">roltoewijzingen toolist, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/read` bewerking bij Hallo bereik.</span><span class="sxs-lookup"><span data-stu-id="bc429-111">toolist role assignments, you must have access too`Microsoft.Authorization/roleAssignments/read` operation at hello scope.</span></span> <span data-ttu-id="bc429-112">Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-112">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="bc429-113">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-114">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-114">Request</span></span>
<span data-ttu-id="bc429-115">Gebruik Hallo **ophalen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-115">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="bc429-116">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-116">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-117">Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="bc429-117">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="bc429-118">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-118">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-119">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-120">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-121">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-122">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="bc429-123">Vervang *{filter}* met Hallo voorwaarde dat u wenst dat tooapply toofilter Hallo rol toewijzingslijst:</span><span class="sxs-lookup"><span data-stu-id="bc429-123">Replace *{filter}* with hello condition that you wish tooapply toofilter hello role assignment list:</span></span>

   * <span data-ttu-id="bc429-124">Lijst roltoewijzingen voor alleen Hallo opgegeven bereik, inclusief niet Hallo roltoewijzingen op subscopes:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="bc429-124">List role assignments for only hello specified scope, not including hello role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="bc429-125">Roltoewijzingen lijst voor een specifieke gebruiker, groep of toepassing:`principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="bc429-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="bc429-126">Lijst van roltoewijzingen voor een specifieke gebruiker, inclusief overgenomen van groepen |`assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="bc429-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="bc429-127">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-127">Response</span></span>
<span data-ttu-id="bc429-128">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-128">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/acdd72a7-3385-48ef-bd42-f606fba81ae7",
        "principalId": "2f9d4375-cbf1-48e8-83c9-2a0be4cb33fb",
        "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
        "createdOn": "2015-10-08T07:28:24.3905077Z",
        "updatedOn": "2015-10-08T07:28:24.3905077Z",
        "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
        "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/baa6e199-ad19-4667-b768-623fde31aedd",
      "type": "Microsoft.Authorization/roleAssignments",
      "name": "baa6e199-ad19-4667-b768-623fde31aedd"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="bc429-129">Informatie ophalen over een roltoewijzing</span><span class="sxs-lookup"><span data-stu-id="bc429-129">Get information about a role assignment</span></span>
<span data-ttu-id="bc429-130">Hiermee haalt u informatie over één roltoewijzing opgegeven Hallo rol toewijzing-id.</span><span class="sxs-lookup"><span data-stu-id="bc429-130">Gets information about a single role assignment specified by hello role assignment identifier.</span></span>

<span data-ttu-id="bc429-131">tooget informatie over een roltoewijzing, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/read` bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-131">tooget information about a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="bc429-132">Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-132">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="bc429-133">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-134">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-134">Request</span></span>
<span data-ttu-id="bc429-135">Gebruik Hallo **ophalen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-135">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="bc429-136">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-136">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-137">Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="bc429-137">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="bc429-138">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-138">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-139">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-140">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-141">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-142">Vervang *{toewijzing-rol-id}* met Hallo GUID-id van de roltoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-142">Replace *{role-assignment-id}* with hello GUID identifier of hello role assignment.</span></span>
3. <span data-ttu-id="bc429-143">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="bc429-144">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-144">Response</span></span>
<span data-ttu-id="bc429-145">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-145">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/b24988ac-6180-42a0-ab88-20f7382dd24c",
    "principalId": "672f1afa-526a-4ef6-819c-975c7cd79022",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e",
    "createdOn": "2015-10-05T08:36:26.4014813Z",
    "updatedOn": "2015-10-05T08:36:26.4014813Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleAssignments/196965ae-6088-4121-a92a-f1e33fdcc73e",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "196965ae-6088-4121-a92a-f1e33fdcc73e"
}

```

## <a name="create-a-role-assignment"></a><span data-ttu-id="bc429-146">Een roltoewijzing maken</span><span class="sxs-lookup"><span data-stu-id="bc429-146">Create a Role Assignment</span></span>
<span data-ttu-id="bc429-147">Een gebruikersrol maakt toewijzing op Hallo opgegeven bereik voor Hallo principal verlenen Hallo opgegeven rol opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bc429-147">Create a role assignment at hello specified scope for hello specified principal granting hello specified role.</span></span>

<span data-ttu-id="bc429-148">een roltoewijzing toocreate, u moet de toegang te hebben`Microsoft.Authorization/roleAssignments/write` bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-148">toocreate a role assignment, you must have access too`Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="bc429-149">Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-149">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="bc429-150">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-151">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-151">Request</span></span>
<span data-ttu-id="bc429-152">Gebruik Hallo **plaatsen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-152">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="bc429-153">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-153">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-154">Vervang *{bereik}* met Hallo bereik op die u toocreate Hallo roltoewijzingen wenst.</span><span class="sxs-lookup"><span data-stu-id="bc429-154">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="bc429-155">Als u een roltoewijzing op een bovenliggend bereik maakt, alle onderliggende bereiken Hallo overgenomen dezelfde roltoewijzing.</span><span class="sxs-lookup"><span data-stu-id="bc429-155">When you create a role assignment at a parent scope, all child scopes inherit hello same role assignment.</span></span> <span data-ttu-id="bc429-156">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-156">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-157">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-158">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="bc429-159">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-160">Vervang *{toewijzing-rol-id}* met een nieuwe GUID die Hallo GUID-id van nieuwe roltoewijzing hello wordt.</span><span class="sxs-lookup"><span data-stu-id="bc429-160">Replace *{role-assignment-id}* with a new GUID, which becomes hello GUID identifier of hello new role assignment.</span></span>
3. <span data-ttu-id="bc429-161">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="bc429-162">Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="bc429-162">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="bc429-163">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="bc429-163">Element Name</span></span> | <span data-ttu-id="bc429-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="bc429-164">Required</span></span> | <span data-ttu-id="bc429-165">Type</span><span class="sxs-lookup"><span data-stu-id="bc429-165">Type</span></span> | <span data-ttu-id="bc429-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc429-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bc429-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="bc429-167">roleDefinitionId</span></span> |<span data-ttu-id="bc429-168">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-168">Yes</span></span> |<span data-ttu-id="bc429-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-169">String</span></span> |<span data-ttu-id="bc429-170">Hallo-id van Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-170">hello identifier of hello role.</span></span> <span data-ttu-id="bc429-171">Hallo-indeling van het Hallo-id is:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="bc429-171">hello format of hello identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="bc429-172">principalId</span><span class="sxs-lookup"><span data-stu-id="bc429-172">principalId</span></span> |<span data-ttu-id="bc429-173">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-173">Yes</span></span> |<span data-ttu-id="bc429-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-174">String</span></span> |<span data-ttu-id="bc429-175">objectId hello Azure AD-principal (gebruiker, groep of service-principal) toowhich Hallo rol wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bc429-175">objectId of hello Azure AD principal (user, group, or service principal) toowhich hello role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="bc429-176">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-176">Response</span></span>
<span data-ttu-id="bc429-177">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="bc429-177">Status code: 201</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-16T00:27:19.6447515Z",
    "updatedOn": "2015-12-16T00:27:19.6447515Z",
    "createdBy": null,
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/2e9e86c8-0e91-4958-b21f-20f51f27bab2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "2e9e86c8-0e91-4958-b21f-20f51f27bab2"
}

```

## <a name="delete-a-role-assignment"></a><span data-ttu-id="bc429-178">Een roltoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="bc429-178">Delete a Role Assignment</span></span>
<span data-ttu-id="bc429-179">Een roltoewijzing bij Hallo verwijderen opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="bc429-179">Delete a role assignment at hello specified scope.</span></span>

<span data-ttu-id="bc429-180">een roltoewijzing toodelete, hebt u toegang toohello `Microsoft.Authorization/roleAssignments/delete` bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-180">toodelete a role assignment, you must have access toohello `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="bc429-181">Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-181">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="bc429-182">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-183">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-183">Request</span></span>
<span data-ttu-id="bc429-184">Gebruik Hallo **verwijderen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-184">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="bc429-185">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-185">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-186">Vervang *{bereik}* met Hallo bereik op die u toocreate Hallo roltoewijzingen wenst.</span><span class="sxs-lookup"><span data-stu-id="bc429-186">Replace *{scope}* with hello scope at which you wish toocreate hello role assignments.</span></span> <span data-ttu-id="bc429-187">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-187">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-188">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-189">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-190">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-191">Vervang *{toewijzing-rol-id}* met Hallo roltoewijzings-id GUID.</span><span class="sxs-lookup"><span data-stu-id="bc429-191">Replace *{role-assignment-id}* with hello role assignment id GUID.</span></span>
3. <span data-ttu-id="bc429-192">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="bc429-193">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-193">Response</span></span>
<span data-ttu-id="bc429-194">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-194">Status code: 200</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b",
    "scope": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND",
    "createdOn": "2015-12-17T23:21:40.8921564Z",
    "updatedOn": "2015-12-17T23:21:40.8921564Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleAssignments/5eec22ee-ea5c-431e-8f41-82c560706fd2",
  "type": "Microsoft.Authorization/roleAssignments",
  "name": "5eec22ee-ea5c-431e-8f41-82c560706fd2"
}

```

## <a name="list-all-roles"></a><span data-ttu-id="bc429-195">Lijst van alle rollen</span><span class="sxs-lookup"><span data-stu-id="bc429-195">List all Roles</span></span>
<span data-ttu-id="bc429-196">Geeft een lijst van alle Hallo-functies die beschikbaar voor toewijzing op Hallo opgegeven zijn bereik.</span><span class="sxs-lookup"><span data-stu-id="bc429-196">Lists all hello roles that are available for assignment at hello specified scope.</span></span>

<span data-ttu-id="bc429-197">toolist rollen, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/read` bewerking bij Hallo bereik.</span><span class="sxs-lookup"><span data-stu-id="bc429-197">toolist roles, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation at hello scope.</span></span> <span data-ttu-id="bc429-198">Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-198">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="bc429-199">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-200">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-200">Request</span></span>
<span data-ttu-id="bc429-201">Gebruik Hallo **ophalen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-201">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="bc429-202">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-202">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-203">Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo rollen.</span><span class="sxs-lookup"><span data-stu-id="bc429-203">Replace *{scope}* with hello scope for which you wish toolist hello roles.</span></span> <span data-ttu-id="bc429-204">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-204">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-205">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-206">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-208">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="bc429-209">Vervang *{filter}* met Hallo voorwaarde dat u wenst dat tooapply toofilter Hallo lijst met rollen:</span><span class="sxs-lookup"><span data-stu-id="bc429-209">Replace *{filter}* with hello condition that you wish tooapply toofilter hello list of roles:</span></span>

   * <span data-ttu-id="bc429-210">Lijst met beschikbare rollen voor toewijzing op Hallo opgegeven bereik en een van de onderliggende bereiken:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="bc429-210">List roles available for assignment at hello specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="bc429-211">Zoeken naar een rol met de exacte weergavenaam: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="bc429-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="bc429-212">Hallo URL gecodeerde vorm van Hallo exacte weergavenaam van de rol hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc429-212">Use hello URL encoded form of hello exact display name of hello role.</span></span> <span data-ttu-id="bc429-213">Bijvoorbeeld:`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="bc429-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="bc429-214">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-214">Response</span></span>
<span data-ttu-id="bc429-215">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="get-information-about-a-role"></a><span data-ttu-id="bc429-216">Informatie ophalen over een rol</span><span class="sxs-lookup"><span data-stu-id="bc429-216">Get information about a Role</span></span>
<span data-ttu-id="bc429-217">Hiermee haalt u informatie over een enkele rol door Hallo rol definitie-id opgegeven.</span><span class="sxs-lookup"><span data-stu-id="bc429-217">Gets information about a single role specified by hello role definition identifier.</span></span> <span data-ttu-id="bc429-218">Zie informatie over één rol met de weergavenaam tooget [lijst van alle rollen](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="bc429-218">tooget information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="bc429-219">tooget informatie over een rol, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/read` bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-219">tooget information about a role, you must have access too`Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="bc429-220">Alle Hallo ingebouwde rollen krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-220">All hello built-in roles are granted access toothis operation.</span></span> <span data-ttu-id="bc429-221">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-222">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-222">Request</span></span>
<span data-ttu-id="bc429-223">Gebruik Hallo **ophalen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-223">Use hello **GET** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="bc429-224">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-224">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-225">Vervang *{bereik}* met Hallo bereik waarvoor toolist Hallo roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="bc429-225">Replace *{scope}* with hello scope for which you wish toolist hello role assignments.</span></span> <span data-ttu-id="bc429-226">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-226">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-227">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-228">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-229">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-230">Vervang *{rol-definitie-id}* met Hallo GUID-id van de roldefinitie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-230">Replace *{role-definition-id}* with hello GUID identifier of hello role definition.</span></span>
3. <span data-ttu-id="bc429-231">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="bc429-232">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-232">Response</span></span>
<span data-ttu-id="bc429-233">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access toothem, and not hello virtual network or storage account they\u2019re connected to.",
        "assignableScopes": [
          "/"
        ],
        "permissions": [
          {
            "actions": [
              "Microsoft.Authorization/*/read",
              "Microsoft.Compute/availabilitySets/*",
              "Microsoft.Compute/locations/*",
              "Microsoft.Compute/virtualMachines/*",
              "Microsoft.Compute/virtualMachineScaleSets/*",
              "Microsoft.Insights/alertRules/*",
              "Microsoft.Network/applicationGateways/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/backendAddressPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatPools/join/action",
              "Microsoft.Network/loadBalancers/inboundNatRules/join/action",
              "Microsoft.Network/loadBalancers/read",
              "Microsoft.Network/locations/*",
              "Microsoft.Network/networkInterfaces/*",
              "Microsoft.Network/networkSecurityGroups/join/action",
              "Microsoft.Network/networkSecurityGroups/read",
              "Microsoft.Network/publicIPAddresses/join/action",
              "Microsoft.Network/publicIPAddresses/read",
              "Microsoft.Network/virtualNetworks/read",
              "Microsoft.Network/virtualNetworks/subnets/join/action",
              "Microsoft.Resources/deployments/*",
              "Microsoft.Resources/subscriptions/resourceGroups/read",
              "Microsoft.Storage/storageAccounts/listKeys/action",
              "Microsoft.Storage/storageAccounts/read",
              "Microsoft.Support/*"
            ],
            "notActions": []
          }
        ],
        "createdOn": "2015-06-02T00:18:27.3542698Z",
        "updatedOn": "2015-12-08T03:16:55.6170255Z",
        "createdBy": null,
        "updatedBy": null
      },
      "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
      "type": "Microsoft.Authorization/roleDefinitions",
      "name": "9980e02c-c2be-4d73-94e8-173b1dc7cf3c"
    }
  ],
  "nextLink": null
}

```

## <a name="create-a-custom-role"></a><span data-ttu-id="bc429-234">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="bc429-234">Create a Custom Role</span></span>
<span data-ttu-id="bc429-235">Maak een aangepaste beveiligingsrol.</span><span class="sxs-lookup"><span data-stu-id="bc429-235">Create a custom role.</span></span>

<span data-ttu-id="bc429-236">een aangepaste beveiligingsrol toocreate, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/write` bewerking op alle Hallo `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="bc429-236">toocreate a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="bc429-237">Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-237">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="bc429-238">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-239">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-239">Request</span></span>
<span data-ttu-id="bc429-240">Gebruik Hallo **plaatsen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-240">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="bc429-241">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-241">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-242">Vervang *{bereik}* Hello eerste *AssignableScope* van Hallo aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-242">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="bc429-243">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus.</span><span class="sxs-lookup"><span data-stu-id="bc429-243">hello following examples show how toospecify hello scope for different levels.</span></span>

   * <span data-ttu-id="bc429-244">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-245">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-246">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-247">Vervang *{rol-definitie-id}* met een nieuwe GUID die Hallo GUID-id van nieuwe aangepaste rol hello wordt.</span><span class="sxs-lookup"><span data-stu-id="bc429-247">Replace *{role-definition-id}* with a new GUID, which becomes hello GUID identifier of hello new custom role.</span></span>
3. <span data-ttu-id="bc429-248">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="bc429-249">Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="bc429-249">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="bc429-250">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="bc429-250">Element Name</span></span> | <span data-ttu-id="bc429-251">Vereist</span><span class="sxs-lookup"><span data-stu-id="bc429-251">Required</span></span> | <span data-ttu-id="bc429-252">Type</span><span class="sxs-lookup"><span data-stu-id="bc429-252">Type</span></span> | <span data-ttu-id="bc429-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc429-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bc429-254">naam</span><span class="sxs-lookup"><span data-stu-id="bc429-254">name</span></span> |<span data-ttu-id="bc429-255">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-255">Yes</span></span> |<span data-ttu-id="bc429-256">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-256">String</span></span> |<span data-ttu-id="bc429-257">GUID-id van de aangepaste rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-257">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="bc429-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="bc429-258">properties.roleName</span></span> |<span data-ttu-id="bc429-259">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-259">Yes</span></span> |<span data-ttu-id="bc429-260">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-260">String</span></span> |<span data-ttu-id="bc429-261">Weergavenaam van de aangepaste rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-261">Display name of hello custom role.</span></span> <span data-ttu-id="bc429-262">Maximale grootte 128 tekens.</span><span class="sxs-lookup"><span data-stu-id="bc429-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="bc429-263">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="bc429-263">properties.description</span></span> |<span data-ttu-id="bc429-264">Nee</span><span class="sxs-lookup"><span data-stu-id="bc429-264">No</span></span> |<span data-ttu-id="bc429-265">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-265">String</span></span> |<span data-ttu-id="bc429-266">Beschrijving van aangepaste Hallo-rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-266">Description of hello custom role.</span></span> <span data-ttu-id="bc429-267">Maximale grootte 1024 tekens.</span><span class="sxs-lookup"><span data-stu-id="bc429-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="bc429-268">Properties.type</span><span class="sxs-lookup"><span data-stu-id="bc429-268">properties.type</span></span> |<span data-ttu-id="bc429-269">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-269">Yes</span></span> |<span data-ttu-id="bc429-270">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-270">String</span></span> |<span data-ttu-id="bc429-271">Stel te 'CustomRole'.</span><span class="sxs-lookup"><span data-stu-id="bc429-271">Set too"CustomRole."</span></span> |
| <span data-ttu-id="bc429-272">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="bc429-272">properties.permissions.actions</span></span> |<span data-ttu-id="bc429-273">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-273">Yes</span></span> |<span data-ttu-id="bc429-274">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-274">String[]</span></span> |<span data-ttu-id="bc429-275">Een matrix van actie tekenreeksen geven Hallo operations verleend door Hallo aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-275">An array of action strings specifying hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="bc429-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="bc429-276">properties.permissions.notActions</span></span> |<span data-ttu-id="bc429-277">Nee</span><span class="sxs-lookup"><span data-stu-id="bc429-277">No</span></span> |<span data-ttu-id="bc429-278">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-278">String[]</span></span> |<span data-ttu-id="bc429-279">Een matrix met actie tekenreeksen Hallo operations tooexclude van Hallo-bewerkingen die zijn verleend door de aangepaste rol Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="bc429-279">An array of action strings specifying hello operations tooexclude from hello operations granted by hello custom role.</span></span> |
| <span data-ttu-id="bc429-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="bc429-280">properties.assignableScopes</span></span> |<span data-ttu-id="bc429-281">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-281">Yes</span></span> |<span data-ttu-id="bc429-282">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-282">String[]</span></span> |<span data-ttu-id="bc429-283">Een matrix van bereiken in welke Hallo aangepaste rol kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bc429-283">An array of scopes in which hello custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="bc429-284">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-284">Response</span></span>
<span data-ttu-id="bc429-285">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="bc429-285">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="update-a-custom-role"></a><span data-ttu-id="bc429-286">Bijwerken van een aangepaste rol</span><span class="sxs-lookup"><span data-stu-id="bc429-286">Update a Custom Role</span></span>
<span data-ttu-id="bc429-287">Een aangepaste rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bc429-287">Modify a custom role.</span></span>

<span data-ttu-id="bc429-288">een aangepaste beveiligingsrol toomodify, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/write` bewerking op alle Hallo `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="bc429-288">toomodify a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/write` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="bc429-289">Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-289">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="bc429-290">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-291">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-291">Request</span></span>
<span data-ttu-id="bc429-292">Gebruik Hallo **plaatsen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-292">Use hello **PUT** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="bc429-293">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-293">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-294">Vervang *{bereik}* Hello eerste *AssignableScope* van Hallo aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-294">Replace *{scope}* with hello first *AssignableScope* of hello custom role.</span></span> <span data-ttu-id="bc429-295">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-295">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-296">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-297">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-298">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-299">Vervang *{rol-definitie-id}* met Hallo GUID-id van de aangepaste rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-299">Replace *{role-definition-id}* with hello GUID identifier of hello custom role.</span></span>
3. <span data-ttu-id="bc429-300">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="bc429-301">Voor de aanvraagtekst hello, bieden Hallo waarden in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="bc429-301">For hello request body, provide hello values in hello following format:</span></span>

```
{
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "properties": {
    "roleName": "Virtual Machine Operator",
    "description": "Lets you monitor virtual machines and restart them.",
    "type": "CustomRole",
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ]
  }
}

```

| <span data-ttu-id="bc429-302">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="bc429-302">Element Name</span></span> | <span data-ttu-id="bc429-303">Vereist</span><span class="sxs-lookup"><span data-stu-id="bc429-303">Required</span></span> | <span data-ttu-id="bc429-304">Type</span><span class="sxs-lookup"><span data-stu-id="bc429-304">Type</span></span> | <span data-ttu-id="bc429-305">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc429-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="bc429-306">naam</span><span class="sxs-lookup"><span data-stu-id="bc429-306">name</span></span> |<span data-ttu-id="bc429-307">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-307">Yes</span></span> |<span data-ttu-id="bc429-308">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-308">String</span></span> |<span data-ttu-id="bc429-309">GUID-id van de aangepaste rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-309">GUID identifier of hello custom role.</span></span> |
| <span data-ttu-id="bc429-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="bc429-310">properties.roleName</span></span> |<span data-ttu-id="bc429-311">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-311">Yes</span></span> |<span data-ttu-id="bc429-312">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-312">String</span></span> |<span data-ttu-id="bc429-313">Weergavenaam van Hallo bijgewerkt aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-313">Display name of hello updated custom role.</span></span> |
| <span data-ttu-id="bc429-314">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="bc429-314">properties.description</span></span> |<span data-ttu-id="bc429-315">Nee</span><span class="sxs-lookup"><span data-stu-id="bc429-315">No</span></span> |<span data-ttu-id="bc429-316">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-316">String</span></span> |<span data-ttu-id="bc429-317">Beschrijving van Hallo bijgewerkt aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="bc429-317">Description of hello updated custom role.</span></span> |
| <span data-ttu-id="bc429-318">Properties.type</span><span class="sxs-lookup"><span data-stu-id="bc429-318">properties.type</span></span> |<span data-ttu-id="bc429-319">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-319">Yes</span></span> |<span data-ttu-id="bc429-320">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="bc429-320">String</span></span> |<span data-ttu-id="bc429-321">Stel te 'CustomRole'.</span><span class="sxs-lookup"><span data-stu-id="bc429-321">Set too"CustomRole."</span></span> |
| <span data-ttu-id="bc429-322">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="bc429-322">properties.permissions.actions</span></span> |<span data-ttu-id="bc429-323">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-323">Yes</span></span> |<span data-ttu-id="bc429-324">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-324">String[]</span></span> |<span data-ttu-id="bc429-325">Een matrix met actie tekenreeksen geven Hallo operations toowhich Hallo bijgewerkt aangepaste rol verleent toegang.</span><span class="sxs-lookup"><span data-stu-id="bc429-325">An array of action strings specifying hello operations toowhich hello updated custom role grants access.</span></span> |
| <span data-ttu-id="bc429-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="bc429-326">properties.permissions.notActions</span></span> |<span data-ttu-id="bc429-327">Nee</span><span class="sxs-lookup"><span data-stu-id="bc429-327">No</span></span> |<span data-ttu-id="bc429-328">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-328">String[]</span></span> |<span data-ttu-id="bc429-329">Een matrix van actie tekenreeksen geven Hallo operations tooexclude van welke Hallo aangepaste rol verleent bijgewerkt Hallo-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bc429-329">An array of action strings specifying hello operations tooexclude from hello operations which hello updated custom role grants.</span></span> |
| <span data-ttu-id="bc429-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="bc429-330">properties.assignableScopes</span></span> |<span data-ttu-id="bc429-331">Ja</span><span class="sxs-lookup"><span data-stu-id="bc429-331">Yes</span></span> |<span data-ttu-id="bc429-332">String]</span><span class="sxs-lookup"><span data-stu-id="bc429-332">String[]</span></span> |<span data-ttu-id="bc429-333">Een matrix van bereiken in welke Hallo bijgewerkte aangepaste rol kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bc429-333">An array of scopes in which hello updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="bc429-334">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-334">Response</span></span>
<span data-ttu-id="bc429-335">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="bc429-335">Status code: 201</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-18T00:10:51.4662695Z",
    "updatedOn": "2015-12-18T00:10:51.4662695Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "7c8c8ccd-9838-4e42-b38c-60f0bbe9a9d7"
}

```

## <a name="delete-a-custom-role"></a><span data-ttu-id="bc429-336">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="bc429-336">Delete a Custom Role</span></span>
<span data-ttu-id="bc429-337">Een aangepaste rol verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc429-337">Delete a custom role.</span></span>

<span data-ttu-id="bc429-338">een aangepaste beveiligingsrol toodelete, u moet de toegang te hebben`Microsoft.Authorization/roleDefinitions/delete` bewerking op alle Hallo `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="bc429-338">toodelete a custom role, you must have access too`Microsoft.Authorization/roleDefinitions/delete` operation on all hello `AssignableScopes`.</span></span> <span data-ttu-id="bc429-339">Hallo ingebouwde rollen, alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang toothis bewerking.</span><span class="sxs-lookup"><span data-stu-id="bc429-339">Of hello built-in roles, only *Owner* and *User Access Administrator* are granted access toothis operation.</span></span> <span data-ttu-id="bc429-340">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="bc429-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="bc429-341">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="bc429-341">Request</span></span>
<span data-ttu-id="bc429-342">Gebruik Hallo **verwijderen** methode Hello URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="bc429-342">Use hello **DELETE** method with hello following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="bc429-343">Zorg binnen Hallo URI, Hallo vervangingen toocustomize na uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="bc429-343">Within hello URI, make hello following substitutions toocustomize your request:</span></span>

1. <span data-ttu-id="bc429-344">Vervang *{bereik}* met Hallo-bereik dat u wenst dat toodelete Hallo roldefinitie.</span><span class="sxs-lookup"><span data-stu-id="bc429-344">Replace *{scope}* with hello scope at which you wish toodelete hello role definition.</span></span> <span data-ttu-id="bc429-345">Hallo volgen voorbeelden laten zien hoe toospecify Hallo bereik voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="bc429-345">hello following examples show how toospecify hello scope for different levels:</span></span>

   * <span data-ttu-id="bc429-346">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="bc429-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="bc429-347">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="bc429-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="bc429-348">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="bc429-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="bc429-349">Vervang *{rol-definitie-id}* met Hallo GUID roldefinitie-id van de aangepaste rol Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc429-349">Replace *{role-definition-id}* with hello GUID role definition id of hello custom role.</span></span>
3. <span data-ttu-id="bc429-350">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="bc429-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="bc429-351">Antwoord</span><span class="sxs-lookup"><span data-stu-id="bc429-351">Response</span></span>
<span data-ttu-id="bc429-352">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="bc429-352">Status code: 200</span></span>

```
{
  "properties": {
    "roleName": "Virtual Machine Operator",
    "type": "CustomRole",
    "description": "Lets you monitor virtual machines and restart them.",
    "assignableScopes": [
      "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e"
    ],
    "permissions": [
      {
        "actions": [
          "Microsoft.Authorization/*/read",
          "Microsoft.Compute/*/read",
          "Microsoft.Insights/alertRules/*",
          "Microsoft.Network/*/read",
          "Microsoft.Resources/subscriptions/resourceGroups/read",
          "Microsoft.Storage/*/read",
          "Microsoft.Support/*",
          "Microsoft.Compute/virtualMachines/start/action",
          "Microsoft.Compute/virtualMachines/restart/action"
        ],
        "notActions": []
      }
    ],
    "createdOn": "2015-12-16T00:07:02.9236555Z",
    "updatedOn": "2015-12-16T00:07:02.9236555Z",
    "createdBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e",
    "updatedBy": "877f0ab8-9c5f-420b-bf88-a1c6c7e2643e"
  },
  "id": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/providers/Microsoft.Authorization/roleDefinitions/0bd62a70-e1b8-4e0b-a7c2-75cab365c95b",
  "type": "Microsoft.Authorization/roleDefinitions",
  "name": "0bd62a70-e1b8-4e0b-a7c2-75cab365c95b"
}

```

## <a name="next-steps"></a><span data-ttu-id="bc429-353">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc429-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
