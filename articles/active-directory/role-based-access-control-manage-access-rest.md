---
title: Op rollen gebaseerde toegangsbeheer met de REST - Azure AD | Microsoft Docs
description: Op rollen gebaseerde toegangsbeheer met de REST-API beheren
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
ms.openlocfilehash: a5c19fd87ce1ae3e199bf1dfc8cf82f5653baac2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-role-based-access-control-with-the-rest-api"></a><span data-ttu-id="8e8d3-103">Op rollen gebaseerde toegangsbeheer met de REST-API beheren</span><span class="sxs-lookup"><span data-stu-id="8e8d3-103">Manage Role-Based Access Control with the REST API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8e8d3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8e8d3-104">PowerShell</span></span>](role-based-access-control-manage-access-powershell.md)
> * [<span data-ttu-id="8e8d3-105">Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="8e8d3-105">Azure CLI</span></span>](role-based-access-control-manage-access-azure-cli.md)
> * [<span data-ttu-id="8e8d3-106">REST API</span><span class="sxs-lookup"><span data-stu-id="8e8d3-106">REST API</span></span>](role-based-access-control-manage-access-rest.md)

<span data-ttu-id="8e8d3-107">Op rollen gebaseerde toegangsbeheer (RBAC) in de Azure portal en Azure Resource Manager-API kunt u toegang tot uw abonnement en bronnen op een heel nauwkeurig beheren.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-107">Role-Based Access Control (RBAC) in the Azure portal and Azure Resource Manager API helps you manage access to your subscription and resources at a fine-grained level.</span></span> <span data-ttu-id="8e8d3-108">Met deze functie kunt u toegang tot Active Directory-gebruikers, groepen of service-principals verlenen door sommige rollen toewijzen aan deze bij een bepaald bereik.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-108">With this feature, you can grant access for Active Directory users, groups, or service principals by assigning some roles to them at a particular scope.</span></span>

## <a name="list-all-role-assignments"></a><span data-ttu-id="8e8d3-109">Lijst van alle roltoewijzingen</span><span class="sxs-lookup"><span data-stu-id="8e8d3-109">List all role assignments</span></span>
<span data-ttu-id="8e8d3-110">Geeft een lijst van alle roltoewijzingen aan het opgegeven bereik en subscopes.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-110">Lists all the role assignments at the specified scope and subscopes.</span></span>

<span data-ttu-id="8e8d3-111">Aan de lijst roltoewijzingen, u moet toegang hebben tot `Microsoft.Authorization/roleAssignments/read` bewerking in het bereik.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-111">To list role assignments, you must have access to `Microsoft.Authorization/roleAssignments/read` operation at the scope.</span></span> <span data-ttu-id="8e8d3-112">De ingebouwde rollen krijgen toegangsrechten voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-112">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-113">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-113">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-114">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-114">Request</span></span>
<span data-ttu-id="8e8d3-115">Gebruik de **ophalen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-115">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments?api-version={api-version}&$filter={filter}

<span data-ttu-id="8e8d3-116">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-116">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-117">Vervang *{bereik}* met het bereik waarvoor u wilt de roltoewijzingen lijst.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-117">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="8e8d3-118">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-118">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-119">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-119">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-120">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-120">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-121">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-121">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-122">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-122">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="8e8d3-123">Vervang *{filter}* met de voorwaarde die u wilt toepassen om de rol toewijzingslijst te filteren:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-123">Replace *{filter}* with the condition that you wish to apply to filter the role assignment list:</span></span>

   * <span data-ttu-id="8e8d3-124">Roltoewijzingen voor alleen het opgegeven bereik niet met inbegrip van de roltoewijzingen op subscopes lijst:`atScope()`</span><span class="sxs-lookup"><span data-stu-id="8e8d3-124">List role assignments for only the specified scope, not including the role assignments at subscopes: `atScope()`</span></span>    
   * <span data-ttu-id="8e8d3-125">Roltoewijzingen lijst voor een specifieke gebruiker, groep of toepassing:`principalId%20eq%20'{objectId of user, group, or service principal}'`</span><span class="sxs-lookup"><span data-stu-id="8e8d3-125">List role assignments for a specific user, group, or application: `principalId%20eq%20'{objectId of user, group, or service principal}'`</span></span>  
   * <span data-ttu-id="8e8d3-126">Lijst van roltoewijzingen voor een specifieke gebruiker, inclusief overgenomen van groepen |`assignedTo('{objectId of user}')`</span><span class="sxs-lookup"><span data-stu-id="8e8d3-126">List role assignments for a specific user, including ones inherited from groups | `assignedTo('{objectId of user}')`</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-127">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-127">Response</span></span>
<span data-ttu-id="8e8d3-128">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-128">Status code: 200</span></span>

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

## <a name="get-information-about-a-role-assignment"></a><span data-ttu-id="8e8d3-129">Informatie ophalen over een roltoewijzing</span><span class="sxs-lookup"><span data-stu-id="8e8d3-129">Get information about a role assignment</span></span>
<span data-ttu-id="8e8d3-130">Hiermee haalt u informatie over één roltoewijzing opgegeven door de id van de toewijzing van rollen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-130">Gets information about a single role assignment specified by the role assignment identifier.</span></span>

<span data-ttu-id="8e8d3-131">Als u informatie over een roltoewijzing, u moet toegang hebben tot `Microsoft.Authorization/roleAssignments/read` bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-131">To get information about a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/read` operation.</span></span> <span data-ttu-id="8e8d3-132">De ingebouwde rollen krijgen toegangsrechten voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-132">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-133">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-133">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-134">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-134">Request</span></span>
<span data-ttu-id="8e8d3-135">Gebruik de **ophalen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-135">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8e8d3-136">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-136">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-137">Vervang *{bereik}* met het bereik waarvoor u wilt de roltoewijzingen lijst.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-137">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="8e8d3-138">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-138">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-139">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-139">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-140">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-140">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-141">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-141">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-142">Vervang *{toewijzing-rol-id}* met de id van de GUID van de roltoewijzing.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-142">Replace *{role-assignment-id}* with the GUID identifier of the role assignment.</span></span>
3. <span data-ttu-id="8e8d3-143">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-143">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-144">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-144">Response</span></span>
<span data-ttu-id="8e8d3-145">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-145">Status code: 200</span></span>

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

## <a name="create-a-role-assignment"></a><span data-ttu-id="8e8d3-146">Een roltoewijzing maken</span><span class="sxs-lookup"><span data-stu-id="8e8d3-146">Create a Role Assignment</span></span>
<span data-ttu-id="8e8d3-147">Een roltoewijzing bij het opgegeven bereik voor de opgegeven principal verlenen van de opgegeven rol maken.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-147">Create a role assignment at the specified scope for the specified principal granting the specified role.</span></span>

<span data-ttu-id="8e8d3-148">Voor het maken van een roltoewijzing, u moet toegang hebben tot `Microsoft.Authorization/roleAssignments/write` bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-148">To create a role assignment, you must have access to `Microsoft.Authorization/roleAssignments/write` operation.</span></span> <span data-ttu-id="8e8d3-149">Van de ingebouwde rollen alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang tot deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-149">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-150">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-150">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-151">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-151">Request</span></span>
<span data-ttu-id="8e8d3-152">Gebruik de **plaatsen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-152">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8e8d3-153">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-153">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-154">Vervang *{bereik}* met het bereik waarmee u wilt maken van de roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-154">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="8e8d3-155">Wanneer u een roltoewijzing op een bovenliggend bereik maakt, nemen alle onderliggende bereiken de dezelfde toewijzing van rollen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-155">When you create a role assignment at a parent scope, all child scopes inherit the same role assignment.</span></span> <span data-ttu-id="8e8d3-156">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-156">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-157">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-157">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-158">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-158">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>   
   * <span data-ttu-id="8e8d3-159">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-159">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-160">Vervang *{toewijzing-rol-id}* met een nieuwe GUID die de GUID-id van de nieuwe roltoewijzing wordt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-160">Replace *{role-assignment-id}* with a new GUID, which becomes the GUID identifier of the new role assignment.</span></span>
3. <span data-ttu-id="8e8d3-161">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-161">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8e8d3-162">Geef de waarden in de volgende notatie voor de hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-162">For the request body, provide the values in the following format:</span></span>

```
{
  "properties": {
    "roleDefinitionId": "/subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/Network/providers/Microsoft.Network/virtualNetworks/EASTUS-VNET-01/subnets/Devices-Engineering-ProjectRND/providers/Microsoft.Authorization/roleDefinitions/9980e02c-c2be-4d73-94e8-173b1dc7cf3c",
    "principalId": "5ac84765-1c8c-4994-94b2-629461bd191b"
  }
}

```

| <span data-ttu-id="8e8d3-163">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="8e8d3-163">Element Name</span></span> | <span data-ttu-id="8e8d3-164">Vereist</span><span class="sxs-lookup"><span data-stu-id="8e8d3-164">Required</span></span> | <span data-ttu-id="8e8d3-165">Type</span><span class="sxs-lookup"><span data-stu-id="8e8d3-165">Type</span></span> | <span data-ttu-id="8e8d3-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e8d3-166">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e8d3-167">roleDefinitionId</span><span class="sxs-lookup"><span data-stu-id="8e8d3-167">roleDefinitionId</span></span> |<span data-ttu-id="8e8d3-168">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-168">Yes</span></span> |<span data-ttu-id="8e8d3-169">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-169">String</span></span> |<span data-ttu-id="8e8d3-170">De id van de rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-170">The identifier of the role.</span></span> <span data-ttu-id="8e8d3-171">De indeling van de id is:`{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span><span class="sxs-lookup"><span data-stu-id="8e8d3-171">The format of the identifier is: `{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id-guid}`</span></span> |
| <span data-ttu-id="8e8d3-172">principalId</span><span class="sxs-lookup"><span data-stu-id="8e8d3-172">principalId</span></span> |<span data-ttu-id="8e8d3-173">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-173">Yes</span></span> |<span data-ttu-id="8e8d3-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-174">String</span></span> |<span data-ttu-id="8e8d3-175">object-id van de Azure AD-principal waaraan de rol is toegewezen (gebruiker, groep of service-principal).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-175">objectId of the Azure AD principal (user, group, or service principal) to which the role is assigned.</span></span> |

### <a name="response"></a><span data-ttu-id="8e8d3-176">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-176">Response</span></span>
<span data-ttu-id="8e8d3-177">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="8e8d3-177">Status code: 201</span></span>

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

## <a name="delete-a-role-assignment"></a><span data-ttu-id="8e8d3-178">Een roltoewijzing verwijderen</span><span class="sxs-lookup"><span data-stu-id="8e8d3-178">Delete a Role Assignment</span></span>
<span data-ttu-id="8e8d3-179">Een roltoewijzing bij het opgegeven bereik verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-179">Delete a role assignment at the specified scope.</span></span>

<span data-ttu-id="8e8d3-180">Als u wilt een roltoewijzing hebt verwijderd, u moet toegang hebben tot de `Microsoft.Authorization/roleAssignments/delete` bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-180">To delete a role assignment, you must have access to the `Microsoft.Authorization/roleAssignments/delete` operation.</span></span> <span data-ttu-id="8e8d3-181">Van de ingebouwde rollen alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang tot deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-181">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-182">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-182">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-183">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-183">Request</span></span>
<span data-ttu-id="8e8d3-184">Gebruik de **verwijderen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-184">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleAssignments/{role-assignment-id}?api-version={api-version}

<span data-ttu-id="8e8d3-185">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-185">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-186">Vervang *{bereik}* met het bereik waarmee u wilt maken van de roltoewijzingen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-186">Replace *{scope}* with the scope at which you wish to create the role assignments.</span></span> <span data-ttu-id="8e8d3-187">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-187">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-188">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-188">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-189">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-189">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-190">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-190">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-191">Vervang *{toewijzing-rol-id}* met de roltoewijzings-id GUID.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-191">Replace *{role-assignment-id}* with the role assignment id GUID.</span></span>
3. <span data-ttu-id="8e8d3-192">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-192">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-193">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-193">Response</span></span>
<span data-ttu-id="8e8d3-194">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-194">Status code: 200</span></span>

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

## <a name="list-all-roles"></a><span data-ttu-id="8e8d3-195">Lijst van alle rollen</span><span class="sxs-lookup"><span data-stu-id="8e8d3-195">List all Roles</span></span>
<span data-ttu-id="8e8d3-196">Geeft een lijst van alle functies die beschikbaar voor toewijzing op het opgegeven bereik zijn.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-196">Lists all the roles that are available for assignment at the specified scope.</span></span>

<span data-ttu-id="8e8d3-197">Lijst met rollen, u moet toegang hebben tot `Microsoft.Authorization/roleDefinitions/read` bewerking in het bereik.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-197">To list roles, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation at the scope.</span></span> <span data-ttu-id="8e8d3-198">De ingebouwde rollen krijgen toegangsrechten voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-198">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-199">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-199">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-200">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-200">Request</span></span>
<span data-ttu-id="8e8d3-201">Gebruik de **ophalen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-201">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions?api-version={api-version}&$filter={filter}

<span data-ttu-id="8e8d3-202">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-202">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-203">Vervang *{bereik}* met het bereik waarvoor u wilt weergeven van de rollen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-203">Replace *{scope}* with the scope for which you wish to list the roles.</span></span> <span data-ttu-id="8e8d3-204">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-204">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-205">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-205">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-206">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-206">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-207">Resource /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-208">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-208">Replace *{api-version}* with 2015-07-01.</span></span>
3. <span data-ttu-id="8e8d3-209">Vervang *{filter}* met de voorwaarde die u wilt toepassen om te filteren op de lijst met rollen:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-209">Replace *{filter}* with the condition that you wish to apply to filter the list of roles:</span></span>

   * <span data-ttu-id="8e8d3-210">Lijst met beschikbare rollen voor toewijzing bij het opgegeven bereik en een van de onderliggende scopes van:`atScopeAndBelow()`</span><span class="sxs-lookup"><span data-stu-id="8e8d3-210">List roles available for assignment at the specified scope and any of its child scopes: `atScopeAndBelow()`</span></span>
   * <span data-ttu-id="8e8d3-211">Zoeken naar een rol met de exacte weergavenaam: `roleName%20eq%20'{role-display-name}'`.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-211">Search for a role using exact display name: `roleName%20eq%20'{role-display-name}'`.</span></span> <span data-ttu-id="8e8d3-212">Gebruik het URL-gecodeerd-formulier van de exacte weergavenaam van de rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-212">Use the URL encoded form of the exact display name of the role.</span></span> <span data-ttu-id="8e8d3-213">Bijvoorbeeld:`$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span><span class="sxs-lookup"><span data-stu-id="8e8d3-213">For instance, `$filter=roleName%20eq%20'Virtual%20Machine%20Contributor'` |</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-214">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-214">Response</span></span>
<span data-ttu-id="8e8d3-215">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-215">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="get-information-about-a-role"></a><span data-ttu-id="8e8d3-216">Informatie ophalen over een rol</span><span class="sxs-lookup"><span data-stu-id="8e8d3-216">Get information about a Role</span></span>
<span data-ttu-id="8e8d3-217">Hiermee haalt u informatie over een enkele rol die is opgegeven door de rol definitie-id.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-217">Gets information about a single role specified by the role definition identifier.</span></span> <span data-ttu-id="8e8d3-218">Zie voor informatie over de weergegeven naam met één functie, [lijst van alle rollen](role-based-access-control-manage-access-rest.md#list-all-roles).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-218">To get information about a single role using its display name, see [List all roles](role-based-access-control-manage-access-rest.md#list-all-roles).</span></span>

<span data-ttu-id="8e8d3-219">Als u informatie over een rol, u moet toegang hebben tot `Microsoft.Authorization/roleDefinitions/read` bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-219">To get information about a role, you must have access to `Microsoft.Authorization/roleDefinitions/read` operation.</span></span> <span data-ttu-id="8e8d3-220">De ingebouwde rollen krijgen toegangsrechten voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-220">All the built-in roles are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-221">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-221">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-222">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-222">Request</span></span>
<span data-ttu-id="8e8d3-223">Gebruik de **ophalen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-223">Use the **GET** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8e8d3-224">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-224">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-225">Vervang *{bereik}* met het bereik waarvoor u wilt de roltoewijzingen lijst.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-225">Replace *{scope}* with the scope for which you wish to list the role assignments.</span></span> <span data-ttu-id="8e8d3-226">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-226">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-227">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-227">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-228">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-228">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-229">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-229">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-230">Vervang *{rol-definitie-id}* met de id van de GUID van de functiedefinitie.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-230">Replace *{role-definition-id}* with the GUID identifier of the role definition.</span></span>
3. <span data-ttu-id="8e8d3-231">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-231">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-232">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-232">Response</span></span>
<span data-ttu-id="8e8d3-233">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-233">Status code: 200</span></span>

```
{
  "value": [
    {
      "properties": {
        "roleName": "Virtual Machine Contributor",
        "type": "BuiltInRole",
        "description": "Lets you manage virtual machines, but not access to them, and not the virtual network or storage account they\u2019re connected to.",
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

## <a name="create-a-custom-role"></a><span data-ttu-id="8e8d3-234">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="8e8d3-234">Create a Custom Role</span></span>
<span data-ttu-id="8e8d3-235">Maak een aangepaste beveiligingsrol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-235">Create a custom role.</span></span>

<span data-ttu-id="8e8d3-236">Voor het maken van een aangepaste rol die u moet toegang hebben tot `Microsoft.Authorization/roleDefinitions/write` bewerking op alle de `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-236">To create a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="8e8d3-237">Van de ingebouwde rollen alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang tot deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-237">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-238">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-238">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-239">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-239">Request</span></span>
<span data-ttu-id="8e8d3-240">Gebruik de **plaatsen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-240">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8e8d3-241">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-241">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-242">Vervang *{bereik}* met het eerste *AssignableScope* van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-242">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="8e8d3-243">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-243">The following examples show how to specify the scope for different levels.</span></span>

   * <span data-ttu-id="8e8d3-244">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-244">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-245">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-245">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-246">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-246">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-247">Vervang *{rol-definitie-id}* met een nieuwe GUID die de GUID-id van de nieuwe aangepaste rol wordt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-247">Replace *{role-definition-id}* with a new GUID, which becomes the GUID identifier of the new custom role.</span></span>
3. <span data-ttu-id="8e8d3-248">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-248">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8e8d3-249">Geef de waarden in de volgende notatie voor de hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-249">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="8e8d3-250">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="8e8d3-250">Element Name</span></span> | <span data-ttu-id="8e8d3-251">Vereist</span><span class="sxs-lookup"><span data-stu-id="8e8d3-251">Required</span></span> | <span data-ttu-id="8e8d3-252">Type</span><span class="sxs-lookup"><span data-stu-id="8e8d3-252">Type</span></span> | <span data-ttu-id="8e8d3-253">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e8d3-253">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e8d3-254">naam</span><span class="sxs-lookup"><span data-stu-id="8e8d3-254">name</span></span> |<span data-ttu-id="8e8d3-255">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-255">Yes</span></span> |<span data-ttu-id="8e8d3-256">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-256">String</span></span> |<span data-ttu-id="8e8d3-257">GUID-id van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-257">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="8e8d3-258">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="8e8d3-258">properties.roleName</span></span> |<span data-ttu-id="8e8d3-259">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-259">Yes</span></span> |<span data-ttu-id="8e8d3-260">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-260">String</span></span> |<span data-ttu-id="8e8d3-261">Weergavenaam van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-261">Display name of the custom role.</span></span> <span data-ttu-id="8e8d3-262">Maximale grootte 128 tekens.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-262">Maximum size 128 characters.</span></span> |
| <span data-ttu-id="8e8d3-263">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="8e8d3-263">properties.description</span></span> |<span data-ttu-id="8e8d3-264">Nee</span><span class="sxs-lookup"><span data-stu-id="8e8d3-264">No</span></span> |<span data-ttu-id="8e8d3-265">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-265">String</span></span> |<span data-ttu-id="8e8d3-266">Beschrijving van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-266">Description of the custom role.</span></span> <span data-ttu-id="8e8d3-267">Maximale grootte 1024 tekens.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-267">Maximum size 1024 characters.</span></span> |
| <span data-ttu-id="8e8d3-268">Properties.type</span><span class="sxs-lookup"><span data-stu-id="8e8d3-268">properties.type</span></span> |<span data-ttu-id="8e8d3-269">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-269">Yes</span></span> |<span data-ttu-id="8e8d3-270">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-270">String</span></span> |<span data-ttu-id="8e8d3-271">Ingesteld op 'CustomRole'.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-271">Set to "CustomRole."</span></span> |
| <span data-ttu-id="8e8d3-272">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="8e8d3-272">properties.permissions.actions</span></span> |<span data-ttu-id="8e8d3-273">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-273">Yes</span></span> |<span data-ttu-id="8e8d3-274">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-274">String[]</span></span> |<span data-ttu-id="8e8d3-275">Een matrix van tekenreeksen voor actie geven de bewerkingen die zijn verleend door de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-275">An array of action strings specifying the operations granted by the custom role.</span></span> |
| <span data-ttu-id="8e8d3-276">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="8e8d3-276">properties.permissions.notActions</span></span> |<span data-ttu-id="8e8d3-277">Nee</span><span class="sxs-lookup"><span data-stu-id="8e8d3-277">No</span></span> |<span data-ttu-id="8e8d3-278">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-278">String[]</span></span> |<span data-ttu-id="8e8d3-279">Een matrix van tekenreeksen voor actie geven de bewerkingen moeten worden uitgesloten van de bewerkingen die zijn verleend door de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-279">An array of action strings specifying the operations to exclude from the operations granted by the custom role.</span></span> |
| <span data-ttu-id="8e8d3-280">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="8e8d3-280">properties.assignableScopes</span></span> |<span data-ttu-id="8e8d3-281">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-281">Yes</span></span> |<span data-ttu-id="8e8d3-282">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-282">String[]</span></span> |<span data-ttu-id="8e8d3-283">Een matrix van bereiken waarin de aangepaste rol kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-283">An array of scopes in which the custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="8e8d3-284">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-284">Response</span></span>
<span data-ttu-id="8e8d3-285">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="8e8d3-285">Status code: 201</span></span>

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

## <a name="update-a-custom-role"></a><span data-ttu-id="8e8d3-286">Bijwerken van een aangepaste rol</span><span class="sxs-lookup"><span data-stu-id="8e8d3-286">Update a Custom Role</span></span>
<span data-ttu-id="8e8d3-287">Een aangepaste rol wijzigen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-287">Modify a custom role.</span></span>

<span data-ttu-id="8e8d3-288">Voor het wijzigen van een aangepaste rol die u moet toegang hebben tot `Microsoft.Authorization/roleDefinitions/write` bewerking op alle de `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-288">To modify a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/write` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="8e8d3-289">Van de ingebouwde rollen alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang tot deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-289">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-290">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-290">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-291">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-291">Request</span></span>
<span data-ttu-id="8e8d3-292">Gebruik de **plaatsen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-292">Use the **PUT** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8e8d3-293">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-293">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-294">Vervang *{bereik}* met het eerste *AssignableScope* van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-294">Replace *{scope}* with the first *AssignableScope* of the custom role.</span></span> <span data-ttu-id="8e8d3-295">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-295">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-296">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-296">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-297">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-297">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-298">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-298">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-299">Vervang *{rol-definitie-id}* met de GUID-id van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-299">Replace *{role-definition-id}* with the GUID identifier of the custom role.</span></span>
3. <span data-ttu-id="8e8d3-300">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-300">Replace *{api-version}* with 2015-07-01.</span></span>

<span data-ttu-id="8e8d3-301">Geef de waarden in de volgende notatie voor de hoofdtekst van de aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-301">For the request body, provide the values in the following format:</span></span>

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

| <span data-ttu-id="8e8d3-302">Elementnaam</span><span class="sxs-lookup"><span data-stu-id="8e8d3-302">Element Name</span></span> | <span data-ttu-id="8e8d3-303">Vereist</span><span class="sxs-lookup"><span data-stu-id="8e8d3-303">Required</span></span> | <span data-ttu-id="8e8d3-304">Type</span><span class="sxs-lookup"><span data-stu-id="8e8d3-304">Type</span></span> | <span data-ttu-id="8e8d3-305">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8e8d3-305">Description</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8e8d3-306">naam</span><span class="sxs-lookup"><span data-stu-id="8e8d3-306">name</span></span> |<span data-ttu-id="8e8d3-307">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-307">Yes</span></span> |<span data-ttu-id="8e8d3-308">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-308">String</span></span> |<span data-ttu-id="8e8d3-309">GUID-id van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-309">GUID identifier of the custom role.</span></span> |
| <span data-ttu-id="8e8d3-310">properties.roleName</span><span class="sxs-lookup"><span data-stu-id="8e8d3-310">properties.roleName</span></span> |<span data-ttu-id="8e8d3-311">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-311">Yes</span></span> |<span data-ttu-id="8e8d3-312">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-312">String</span></span> |<span data-ttu-id="8e8d3-313">Weergavenaam van de aangepaste rol die is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-313">Display name of the updated custom role.</span></span> |
| <span data-ttu-id="8e8d3-314">Properties.Description</span><span class="sxs-lookup"><span data-stu-id="8e8d3-314">properties.description</span></span> |<span data-ttu-id="8e8d3-315">Nee</span><span class="sxs-lookup"><span data-stu-id="8e8d3-315">No</span></span> |<span data-ttu-id="8e8d3-316">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-316">String</span></span> |<span data-ttu-id="8e8d3-317">Beschrijving van de aangepaste rol die is bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-317">Description of the updated custom role.</span></span> |
| <span data-ttu-id="8e8d3-318">Properties.type</span><span class="sxs-lookup"><span data-stu-id="8e8d3-318">properties.type</span></span> |<span data-ttu-id="8e8d3-319">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-319">Yes</span></span> |<span data-ttu-id="8e8d3-320">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8e8d3-320">String</span></span> |<span data-ttu-id="8e8d3-321">Ingesteld op 'CustomRole'.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-321">Set to "CustomRole."</span></span> |
| <span data-ttu-id="8e8d3-322">Properties.permissions.Actions</span><span class="sxs-lookup"><span data-stu-id="8e8d3-322">properties.permissions.actions</span></span> |<span data-ttu-id="8e8d3-323">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-323">Yes</span></span> |<span data-ttu-id="8e8d3-324">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-324">String[]</span></span> |<span data-ttu-id="8e8d3-325">Een matrix van tekenreeksen voor actie geven de bewerkingen waarvoor de bijgewerkte aangepaste rol die toegang verleent.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-325">An array of action strings specifying the operations to which the updated custom role grants access.</span></span> |
| <span data-ttu-id="8e8d3-326">properties.permissions.notActions</span><span class="sxs-lookup"><span data-stu-id="8e8d3-326">properties.permissions.notActions</span></span> |<span data-ttu-id="8e8d3-327">Nee</span><span class="sxs-lookup"><span data-stu-id="8e8d3-327">No</span></span> |<span data-ttu-id="8e8d3-328">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-328">String[]</span></span> |<span data-ttu-id="8e8d3-329">Een matrix van tekenreeksen voor actie geven de bewerkingen moeten worden uitgesloten van de bewerkingen die de bijgewerkte aangepaste rol toekent.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-329">An array of action strings specifying the operations to exclude from the operations which the updated custom role grants.</span></span> |
| <span data-ttu-id="8e8d3-330">properties.assignableScopes</span><span class="sxs-lookup"><span data-stu-id="8e8d3-330">properties.assignableScopes</span></span> |<span data-ttu-id="8e8d3-331">Ja</span><span class="sxs-lookup"><span data-stu-id="8e8d3-331">Yes</span></span> |<span data-ttu-id="8e8d3-332">String]</span><span class="sxs-lookup"><span data-stu-id="8e8d3-332">String[]</span></span> |<span data-ttu-id="8e8d3-333">Een matrix van bereiken waarin de bijgewerkte aangepaste rol kan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-333">An array of scopes in which the updated custom role can be used.</span></span> |

### <a name="response"></a><span data-ttu-id="8e8d3-334">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-334">Response</span></span>
<span data-ttu-id="8e8d3-335">Statuscode: 201</span><span class="sxs-lookup"><span data-stu-id="8e8d3-335">Status code: 201</span></span>

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

## <a name="delete-a-custom-role"></a><span data-ttu-id="8e8d3-336">Een aangepaste rol verwijderen</span><span class="sxs-lookup"><span data-stu-id="8e8d3-336">Delete a Custom Role</span></span>
<span data-ttu-id="8e8d3-337">Een aangepaste rol verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-337">Delete a custom role.</span></span>

<span data-ttu-id="8e8d3-338">Voor het verwijderen van een aangepaste rol die u moet toegang hebben tot `Microsoft.Authorization/roleDefinitions/delete` bewerking op alle de `AssignableScopes`.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-338">To delete a custom role, you must have access to `Microsoft.Authorization/roleDefinitions/delete` operation on all the `AssignableScopes`.</span></span> <span data-ttu-id="8e8d3-339">Van de ingebouwde rollen alleen *eigenaar* en *beheerder voor gebruikerstoegang* krijgen toegang tot deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-339">Of the built-in roles, only *Owner* and *User Access Administrator* are granted access to this operation.</span></span> <span data-ttu-id="8e8d3-340">Zie voor meer informatie over roltoewijzingen en het beheer van toegang voor Azure-resources [rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="8e8d3-340">For more information about role assignments and managing access for Azure resources, see [Azure Role-Based Access Control](role-based-access-control-configure.md).</span></span>

### <a name="request"></a><span data-ttu-id="8e8d3-341">Aanvraag</span><span class="sxs-lookup"><span data-stu-id="8e8d3-341">Request</span></span>
<span data-ttu-id="8e8d3-342">Gebruik de **verwijderen** methode met de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-342">Use the **DELETE** method with the following URI:</span></span>

    https://management.azure.com/{scope}/providers/Microsoft.Authorization/roleDefinitions/{role-definition-id}?api-version={api-version}

<span data-ttu-id="8e8d3-343">Binnen de URI moet u de volgende vervangingen voor het aanpassen van uw aanvraag:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-343">Within the URI, make the following substitutions to customize your request:</span></span>

1. <span data-ttu-id="8e8d3-344">Vervang *{bereik}* met het bereik waarmee u wilt verwijderen van de functiedefinitie.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-344">Replace *{scope}* with the scope at which you wish to delete the role definition.</span></span> <span data-ttu-id="8e8d3-345">De volgende voorbeelden laten zien hoe het bereik opgeven voor verschillende niveaus:</span><span class="sxs-lookup"><span data-stu-id="8e8d3-345">The following examples show how to specify the scope for different levels:</span></span>

   * <span data-ttu-id="8e8d3-346">Abonnement: /subscriptions/ {abonnement-id}</span><span class="sxs-lookup"><span data-stu-id="8e8d3-346">Subscription: /subscriptions/{subscription-id}</span></span>  
   * <span data-ttu-id="8e8d3-347">Resourcegroep: /subscriptions/ {abonnement-id} / resourceGroups/myresourcegroup1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-347">Resource Group: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1</span></span>  
   * <span data-ttu-id="8e8d3-348">Bron: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span><span class="sxs-lookup"><span data-stu-id="8e8d3-348">Resource: /subscriptions/{subscription-id}/resourceGroups/myresourcegroup1/providers/Microsoft.Web/sites/mysite1</span></span>  
2. <span data-ttu-id="8e8d3-349">Vervang *{rol-definitie-id}* met de GUID roldefinitie-id van de aangepaste rol.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-349">Replace *{role-definition-id}* with the GUID role definition id of the custom role.</span></span>
3. <span data-ttu-id="8e8d3-350">Vervang *{api-versie}* met 2015-07-01.</span><span class="sxs-lookup"><span data-stu-id="8e8d3-350">Replace *{api-version}* with 2015-07-01.</span></span>

### <a name="response"></a><span data-ttu-id="8e8d3-351">Antwoord</span><span class="sxs-lookup"><span data-stu-id="8e8d3-351">Response</span></span>
<span data-ttu-id="8e8d3-352">Statuscode: 200</span><span class="sxs-lookup"><span data-stu-id="8e8d3-352">Status code: 200</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8e8d3-353">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e8d3-353">Next steps</span></span>

[!INCLUDE [role-based-access-control-toc.md](../../includes/role-based-access-control-toc.md)]
