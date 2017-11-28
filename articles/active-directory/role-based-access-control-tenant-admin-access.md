---
title: aaaTenant admin toegangsrechten - Azure AD uitbreiden | Microsoft Docs
description: Dit onderwerp beschrijft Hallo ingebouwde rollen voor op rollen gebaseerde toegangsbeheer (RBAC).
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
ms.openlocfilehash: 7996f2af3277dc40e2a1766cc4a7862a2399cdef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a><span data-ttu-id="de45a-103">Toegangsrechten uitbreiden als een tenantbeheerder met toegangsbeheer op basis van rollen</span><span class="sxs-lookup"><span data-stu-id="de45a-103">Elevate access as a tenant admin with Role-Based Access Control</span></span>

<span data-ttu-id="de45a-104">Toegangsbeheer op basis van rollen kunt tenantbeheerders tijdelijke uitbreidingen in toegang krijgen, zodat ze hoger dan normaal machtigen kunnen.</span><span class="sxs-lookup"><span data-stu-id="de45a-104">Role-based Access Control helps tenant administrators get temporary elevations in access so that they can grant higher permissions than normal.</span></span> <span data-ttu-id="de45a-105">Een tenantbeheerder bevoegdheden zichzelf toohello toegang beheerderrol wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="de45a-105">A tenant admin can elevate herself toohello User Access Administrator role when needed.</span></span> <span data-ttu-id="de45a-106">Die rol biedt Hallo beheerder machtigingen toogrant tenant zichzelf of andere functies op Hallo bereik '/'.</span><span class="sxs-lookup"><span data-stu-id="de45a-106">That role gives hello tenant admin permissions toogrant herself or others roles at hello "/" scope.</span></span>

<span data-ttu-id="de45a-107">Deze functie is belangrijk omdat hiermee tenant Hallo beheerder toosee die alle abonnementen die zijn opgenomen in een organisatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="de45a-107">This feature is important because it allows hello tenant admin toosee all hello subscriptions that exist in an organization.</span></span> <span data-ttu-id="de45a-108">Ook kunt automation-apps (zoals facturering en controle) tooaccess alle Hallo-abonnementen en bieden een nauwkeurige weergave van de status van de organisatie Hallo voor facturerings- of asset management Hallo.</span><span class="sxs-lookup"><span data-stu-id="de45a-108">It also allows for automation apps (like invoicing and auditing) tooaccess all hello subscriptions and provide an accurate view of hello state of hello organization for billing or asset management.</span></span>  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a><span data-ttu-id="de45a-109">Hoe toouse elevateAccess toogive tenant-toegang</span><span class="sxs-lookup"><span data-stu-id="de45a-109">How toouse elevateAccess toogive tenant access</span></span>

<span data-ttu-id="de45a-110">Hallo basisproces werkt met Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="de45a-110">hello basic process works with hello following steps:</span></span>

1. <span data-ttu-id="de45a-111">REST, aanroepen *elevateAccess*, hebt u de rol beheerder voor gebruikerstoegang op Hallo ' / ' bereik.</span><span class="sxs-lookup"><span data-stu-id="de45a-111">Using REST, call *elevateAccess*, which grants you hello User Access Administrator role at "/" scope.</span></span>

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. <span data-ttu-id="de45a-112">Maak een [roltoewijzing](/rest/api/authorization/roleassignments) tooassign elke rol op een bereik.</span><span class="sxs-lookup"><span data-stu-id="de45a-112">Create a [role assignment](/rest/api/authorization/roleassignments) tooassign any role at any scope.</span></span> <span data-ttu-id="de45a-113">Hallo volgende voorbeeld ziet u Hallo-eigenschappen voor het toewijzen van de rol lezer op Hallo ' / ' bereik:</span><span class="sxs-lookup"><span data-stu-id="de45a-113">hello following example shows hello properties for assigning hello Reader role at "/" scope:</span></span>

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

3. <span data-ttu-id="de45a-114">Tijdens een gebruiker toegang beheerder, kunt u ook verwijderen roltoewijzingen op ' / ' bereik.</span><span class="sxs-lookup"><span data-stu-id="de45a-114">While a User Access Admin, you can also delete role assignments at "/" scope.</span></span>

4. <span data-ttu-id="de45a-115">De gebruiker toegang tot de beheerdersmachtigingen intrekken totdat ze weer nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="de45a-115">Revoke your User Access Admin privileges until they're needed again.</span></span>


## <a name="how-tooundo-hello-elevateaccess-action"></a><span data-ttu-id="de45a-116">Hoe tooundo elevateAccess actie Hallo</span><span class="sxs-lookup"><span data-stu-id="de45a-116">How tooundo hello elevateAccess action</span></span>

<span data-ttu-id="de45a-117">Als u aanroept *elevateAccess* u een roltoewijzing maken voor uzelf, zodat toorevoke die bevoegdheden beschikt u de moet toodelete, toewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="de45a-117">When you call *elevateAccess* you create a role assignment for yourself, so toorevoke those privileges you need toodelete hello assignment.</span></span>

1.  <span data-ttu-id="de45a-118">Roep [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) waar roleName = naam van de Hallo beheerder voor gebruikerstoegang toodetermine GUID van Hallo beheerder voor gebruikerstoegang rol.</span><span class="sxs-lookup"><span data-stu-id="de45a-118">Call [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) where roleName = User Access Administrator toodetermine hello name GUID of hello User Access Administrator role.</span></span> <span data-ttu-id="de45a-119">Hallo antwoord ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="de45a-119">hello response should look like this:</span></span>

    ```
    {"value":[{"properties":{
    "roleName":"User Access Administrator",
    "type":"BuiltInRole",
    "description":"Lets you manage user access tooAzure resources.",
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

    <span data-ttu-id="de45a-120">Hallo GUID van Hallo opslaan *naam* parameter in dit geval **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span><span class="sxs-lookup"><span data-stu-id="de45a-120">Save hello GUID from hello *name* parameter, in this case **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.</span></span>

2. <span data-ttu-id="de45a-121">Roep [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) waar principalId = uw eigen ObjectId.</span><span class="sxs-lookup"><span data-stu-id="de45a-121">Call [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) where principalId = your own ObjectId.</span></span> <span data-ttu-id="de45a-122">Hier ziet u alle toewijzingen in Hallo-tenant.</span><span class="sxs-lookup"><span data-stu-id="de45a-122">This lists all your assignments in hello tenant.</span></span> <span data-ttu-id="de45a-123">Hallo een zoekt waarbij Hallo scope is '/' hello RoleDefinitionId eindigt met Hallo rol naam GUID die u in stap 1 hebt gevonden.</span><span class="sxs-lookup"><span data-stu-id="de45a-123">Look for hello one where hello scope is "/" and hello RoleDefinitionId ends with hello role name GUID you found in step 1.</span></span> <span data-ttu-id="de45a-124">Hallo roltoewijzing moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="de45a-124">hello role assignment should look like this:</span></span>

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

    <span data-ttu-id="de45a-125">Hallo GUID weer van Hallo opslaan *naam* parameter in dit geval **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span><span class="sxs-lookup"><span data-stu-id="de45a-125">Again, save hello GUID from hello *name* parameter, in this case **e7dd75bc-06f6-4e71-9014-ee96a929d099**.</span></span>

3. <span data-ttu-id="de45a-126">Tenslotte roept [verwijderen roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) waar roleAssignmentId = Hallo naam GUID die u in stap 2 hebt vastgesteld.</span><span class="sxs-lookup"><span data-stu-id="de45a-126">Finally, call [DELETE roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) where roleAssignmentId = hello name GUID you found in step 2.</span></span>

## <a name="next-steps"></a><span data-ttu-id="de45a-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de45a-127">Next steps</span></span>

- <span data-ttu-id="de45a-128">Meer informatie over [toegangsbeheer op basis van rollen met REST beheren](role-based-access-control-manage-access-rest.md)</span><span class="sxs-lookup"><span data-stu-id="de45a-128">Learn more about [managing Role-Based Access Control with REST](role-based-access-control-manage-access-rest.md)</span></span>

- <span data-ttu-id="de45a-129">[Beheren van toegangstoewijzingen](role-based-access-control-manage-assignments.md) in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="de45a-129">[Manage access assignments](role-based-access-control-manage-assignments.md) in hello Azure portal</span></span>
