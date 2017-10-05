---
title: Tenantbeheerder toegangsrechten - Azure AD uitbreiden | Microsoft Docs
description: Dit onderwerp beschrijft de ingebouwde rollen voor op rollen gebaseerde toegangsbeheer (RBAC).
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: rqureshi
ms.assetid: b547c5a5-2da2-4372-9938-481cb962d2d6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andredm
ms.openlocfilehash: bf64a92b359a6f68d84fa5ee17eda64ed6371990
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="ed3b5-103">Toegangsrechten uitbreiden als een tenantbeheerder met toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="ed3b5-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="ed3b5-104">Toegangsbeheer op basis van rollen kunt tenantbeheerders tijdelijke uitbreidingen in toegang krijgen, zodat ze hoger dan normaal machtigen kunnen.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="ed3b5-105">Een tenantbeheerder kan zichzelf uitbreiden naar de rol beheerder voor gebruikerstoegang wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-105">A tenant admin can elevate herself to the User Access Administrator role when needed.</span></span> <span data-ttu-id="ed3b5-106">Die rol, krijgt de tenant beheerdersmachtigingen te verlenen aan zichzelf of andere functies op het bereik '/'.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-106">That role gives the tenant admin permissions to grant herself or others roles at the "/" scope.</span></span>

<span data-ttu-id="ed3b5-107">Deze functie is belangrijk omdat hiermee de tenantbeheerder om te zien van de abonnementen die zijn opgenomen in een organisatie.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-107">This feature is important because it allows the tenant admin to see all the subscriptions that exist in an organization.</span></span> <span data-ttu-id="ed3b5-108">Kunt u ook voor automation-apps (zoals facturering en controle) voor toegang tot alle abonnementen en bieden een nauwkeurige weergave van de status van de organisatie voor facturerings- of asset management.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-108">It also allows for automation apps (like invoicing and auditing) to access all the subscriptions and provide an accurate view of the state of the organization for billing or asset management.</span></span>  

## <a name="how-to-use-elevateaccess-to-give-tenant-access"></a><span data-ttu-id="ed3b5-109">Het gebruik van elevateAccess tenant toegang te verlenen</span><span class="sxs-lookup"><span data-stu-id="ed3b5-109">How to use elevateAccess to give tenant access</span></span>

<span data-ttu-id="ed3b5-110">Het basisproces werkt met de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="ed3b5-110">The basic process works with the following steps:</span></span>

1. <span data-ttu-id="ed3b5-111">REST, aanroepen *elevateAccess*, waarmee u de rol van beheerder voor gebruikerstoegang op verleent ' / ' bereik.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-111">Using REST, call *elevateAccess*, which grants you the User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="ed3b5-112">Maak een [roltoewijzing](/rest/api/authorization/roleassignments) aan elke rol op een bereik toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-112">Create a [role assignment](/rest/api/authorization/roleassignments) to assign any role at any scope.</span></span> <span data-ttu-id="ed3b5-113">Het volgende voorbeeld ziet u de eigenschappen voor het toewijzen van de rol lezer op ' / ' bereik:</span><span class="sxs-lookup"><span data-stu-id="ed3b5-113">The following example shows the properties for assigning the Reader role at "/" scope:</span></span>

    ```
    { "properties":{
    "roleDefinitionId": "providers/Microsoft.Authorization/roleDefinitions/acdd72a7338548efbd42f606fba81ae7",
    "principalId": "cbc5e050-d7cd-4310-813b-4870be8ef5bb",
    "scope": "/"
    },
    "id": "providers/Microsoft.Authorization/roleAssignments/64736CA0-56D7-4A94-A551-973C2FE7888B",
    "type": "Microsoft.Authorization/roleAssignments",
    "name": "64736CA0-56D7-4A94-A551-973C2FE7888B"
    }
    ```

3. <span data-ttu-id="ed3b5-114">Tijdens een gebruiker toegang beheerder, kunt u ook verwijderen roltoewijzingen op ' / ' bereik.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="ed3b5-115">De gebruiker toegang tot de beheerdersmachtigingen intrekken totdat ze weer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-to-undo-the-elevateaccess-action"></a><span data-ttu-id="ed3b5-116">De actie elevateAccess ongedaan maken</span><span class="sxs-lookup"><span data-stu-id="ed3b5-116">How to undo the elevateAccess action</span></span>

<span data-ttu-id="ed3b5-117">Als u aanroept *elevateAccess* u een roltoewijzing maken voor uzelf, zodat deze bevoegdheden intrekken moet u de toewijzing verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-117">When you call *elevateAccess* you create a role assignment for yourself, so to revoke those privileges you need to delete the assignment.</span></span>

1.  <span data-ttu-id="ed3b5-118">Roep [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) waar roleName = beheerder voor gebruikerstoegang om te bepalen van de naam van de GUID van de rol beheerder voor gebruikerstoegang.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator to determine the name GUID of the User Access Administrator role.</span></span> <span data-ttu-id="ed3b5-119">Het antwoord ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="ed3b5-119">The response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access to Azure resources.",
    "assignableScopes":["/"],
    "permissions":[{"actions":["*/read","Microsoft.Authorization/*","Microsoft.Support/*"],"notActions":[]}],
    "createdOn":"0001-01-01T08:00:00.0000000Z",
    "updatedOn":"2016-05-31T23:14:04.6964687Z",
    "createdBy":null,
    "updatedBy":null},
    "id":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "type":"Microsoft.Authorization/roleDefinitions",
    "name":"18d7d88d-d35e-4fb5-a5c3-7773c20a72d9"}],
    "nextLink":null}
    ```

    <span data-ttu-id="ed3b5-120">Sla de GUID van de *naam* parameter in dit geval **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-120">Save the GUID from the *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="ed3b5-121">Roep [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) waar principalId = uw eigen ObjectId.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="ed3b5-122">Hier ziet u alle toewijzingen in de tenant.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-122">This lists all your assignments in the tenant.</span></span> <span data-ttu-id="ed3b5-123">Zoek naar de waar de scope is '/' en de RoleDefinitionId eindigt met de naam van de rol GUID die u in stap 1 hebt gevonden.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-123">Look for the one where the scope is "/" and the RoleDefinitionId ends with the role name GUID you found in step 1.</span></span> <span data-ttu-id="ed3b5-124">De roltoewijzing moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="ed3b5-124">The role assignment should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleDefinitionId":"/providers/Microsoft.Authorization/roleDefinitions/18d7d88d-d35e-4fb5-a5c3-7773c20a72d9",
    "principalId":"{objectID}",
    "scope":"/",
    "createdOn":"2016-08-17T19:21:16.3422480Z",
    "updatedOn":"2016-08-17T19:21:16.3422480Z",
    "createdBy":"93ce6722-3638-4222-b582-78b75c5c6d65",
    "updatedBy":"93ce6722-3638-4222-b582-78b75c5c6d65"},
    "id":"/providers/Microsoft.Authorization/roleAssignments/e7dd75bc-06f6-4e71-9014-ee96a929d099",
    "type":"Microsoft.Authorization/roleAssignments",
    "name":"e7dd75bc-06f6-4e71-9014-ee96a929d099"}],
    "nextLink":null}
    ```

    <span data-ttu-id="ed3b5-125">Opnieuw in en sla de GUID van de *naam* parameter in dit geval **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-125">Again, save the GUID from the *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="ed3b5-126">Tenslotte roept [verwijderen roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) waar roleAssignmentId = de naam van de GUID die u in stap 2 hebt vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="ed3b5-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = the name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed3b5-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed3b5-127">Next steps</span></span>

- <span data-ttu-id="ed3b5-128">Meer informatie over [toegangsbeheer op basis van rollen met REST beheren](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="ed3b5-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="ed3b5-129">[Beheren van toegangstoewijzingen](role-based-access-control-manage-assignments.md) in de Azure portal</span><span class="sxs-lookup"><span data-stu-id="ed3b5-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in the Azure portal</span></span>
