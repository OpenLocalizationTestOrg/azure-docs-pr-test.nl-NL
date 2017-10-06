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
# <a name="elevate-access-as-a-tenant-admin-with-role-based-access-control"></a>Toegangsrechten uitbreiden als een tenantbeheerder met toegangsbeheer op basis van rollen

Toegangsbeheer op basis van rollen kunt tenantbeheerders tijdelijke uitbreidingen in toegang krijgen, zodat ze hoger dan normaal machtigen kunnen. Een tenantbeheerder bevoegdheden zichzelf toohello toegang beheerderrol wanneer deze nodig is. Die rol biedt Hallo beheerder machtigingen toogrant tenant zichzelf of andere functies op Hallo bereik '/'.

Deze functie is belangrijk omdat hiermee tenant Hallo beheerder toosee die alle abonnementen die zijn opgenomen in een organisatie Hallo. Ook kunt automation-apps (zoals facturering en controle) tooaccess alle Hallo-abonnementen en bieden een nauwkeurige weergave van de status van de organisatie Hallo voor facturerings- of asset management Hallo.  

## <a name="how-toouse-elevateaccess-toogive-tenant-access"></a>Hoe toouse elevateAccess toogive tenant-toegang

Hallo basisproces werkt met Hallo stappen te volgen:

1. REST, aanroepen *elevateAccess*, hebt u de rol beheerder voor gebruikerstoegang op Hallo ' / ' bereik.

    ```
    POST https://management.azure.com/providers/Microsoft.Authorization/elevateAccess?api-version=2016-07-01
    ```

2. Maak een [roltoewijzing](/rest/api/authorization/roleassignments) tooassign elke rol op een bereik. Hallo volgende voorbeeld ziet u Hallo-eigenschappen voor het toewijzen van de rol lezer op Hallo ' / ' bereik:

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

3. Tijdens een gebruiker toegang beheerder, kunt u ook verwijderen roltoewijzingen op ' / ' bereik.

4. De gebruiker toegang tot de beheerdersmachtigingen intrekken totdat ze weer nodig zijn.


## <a name="how-tooundo-hello-elevateaccess-action"></a>Hoe tooundo elevateAccess actie Hallo

Als u aanroept *elevateAccess* u een roltoewijzing maken voor uzelf, zodat toorevoke die bevoegdheden beschikt u de moet toodelete, toewijzing Hallo.

1.  Roep [GET roleDefinitions](/rest/api/authorization/roledefinitions#RoleDefinitions_Get) waar roleName = naam van de Hallo beheerder voor gebruikerstoegang toodetermine GUID van Hallo beheerder voor gebruikerstoegang rol. Hallo antwoord ziet er als volgt:

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

    Hallo GUID van Hallo opslaan *naam* parameter in dit geval **18d7d88d-d35e-4fb5-a5c3-7773c20a72d9**.

2. Roep [GET roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_Get) waar principalId = uw eigen ObjectId. Hier ziet u alle toewijzingen in Hallo-tenant. Hallo een zoekt waarbij Hallo scope is '/' hello RoleDefinitionId eindigt met Hallo rol naam GUID die u in stap 1 hebt gevonden. Hallo roltoewijzing moet er als volgt uitzien:

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

    Hallo GUID weer van Hallo opslaan *naam* parameter in dit geval **e7dd75bc-06f6-4e71-9014-ee96a929d099**.

3. Tenslotte roept [verwijderen roleAssignments](/rest/api/authorization/roleassignments#RoleAssignments_DeleteById) waar roleAssignmentId = Hallo naam GUID die u in stap 2 hebt vastgesteld.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [toegangsbeheer op basis van rollen met REST beheren](role-based-access-control-manage-access-rest.md)

- [Beheren van toegangstoewijzingen](role-based-access-control-manage-assignments.md) in hello Azure-portal
