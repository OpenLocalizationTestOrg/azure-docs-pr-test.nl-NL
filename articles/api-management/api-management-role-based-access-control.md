---
title: aaaHow tooUse toegangsbeheer op basis van rollen in Azure API Management | Microsoft Docs
description: Meer informatie over hoe toouse Hallo ingebouwde rollen en aangepaste rollen maken in Azure API Management
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: apimpm
ms.openlocfilehash: c51da2ff6886ebcaf796022e3a759c67f36670a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-role-based-access-control-in-azure-api-management"></a>Hoe tooUse rollen gebaseerde toegang beheren in Azure API Management
Azure API Management afhankelijk is gebaseerd toegangsbeheer (RBAC) tooenable Geavanceerd toegangsbeheer voor API Management-services en entiteiten (bijvoorbeeld API's, beleid). In dit artikel biedt een overzicht van de ingebouwde en aangepaste rollen Hallo in API Management. Als u meer informatie over toegangsbeheer in hello Azure-portal wilt, Zie [aan de slag met toegangsbeheer in hello Azure-portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)

## <a name="built-in-roles"></a>Ingebouwde rollen
API Management biedt 3 ingebouwde rollen momenteel en 2 meer functies in Hallo nabije toekomst wordt toegevoegd. Deze rollen kunnen worden toegewezen aan verschillende bereiken, met inbegrip van abonnement, resourcegroep en een afzonderlijk exemplaar van API Management. Bijvoorbeeld, als Hallo 'Azure API Management-Service Reader'-rol is toegewezen tooan-gebruiker op het niveau van de resourcegroep hello, heeft vervolgens hello gebruiker leestoegang tooall exemplaren van API Management in de resourcegroep Hallo. 

Hallo volgende tabel bevat korte beschrijvingen van Hallo ingebouwde rollen. U kunt deze hello Azure Portal of andere hulpprogramma's zoals Azure rollen toewijzen [PowerShell](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-powershell), Azure [opdrachtregelinterface](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-azure-cli), en [REST-API](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-manage-access-rest). Voor meer informatie over het tooassign ingebouwde rollen, Zie [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/).

| Rol          | Leestoegang<sup>[1]</sup> | Schrijftoegang<sup>[2]</sup> | Service maken, verwijderen, VPN- en aangepaste domeinconfiguratie schalen | Toegang tot toolegacy Publsiher Portal | Beschrijving
| ------------- | ---- | ---- | ---- | ---- | ---- | ---- |
| Azure API Management-Service Inzender | ✓ | ✓ | ✓ | ✓ | SUPER-gebruiker. Heeft volledige CRUD toegang tooAPI Management-services en entiteiten (bijvoorbeeld API's, beleid). Heeft toegang tot toohello verouderde publicatieportal. |
| Azure API Management-Service lezer | ✓ | | || Heeft alleen-lezentoegang tooAPI Management-services en entiteiten. |
| Azure API Management-Service-Operator | ✓ | | ✓ | | API Management-services, maar geen entiteiten beheren.|
| Azure API Management Service-Editor<sup>*</sup> | ✓ | ✓ | |  | API Management-entiteiten, maar niet services beheren.|
| Azure API Management-Inhoudsbeheerder<sup>*</sup> | ✓ | | | ✓ | Developer-portal beheren. Alleen-lezentoegang tooservices en entiteiten.|

<sup>[1] leestoegang tooAPI Management-services en entiteiten (bijvoorbeeld API's, beleid)</sup>

<sup>[2]-schrijftoegang tooAPI Management-services en entiteiten met uitzondering van de volgende opeartions: 1)-exemplaar maken, verwijderen en schalen van 2) VPN-configuratie 3) aangepast domein naam instellen</sup>

<sup>\*rol van de Service Editor Hallo zijn beschikbaar nadat we alle admin UI van Hallo bestaande uitgever portal toohello Azure-portal migreren. Hallo Inhoudsbeheerder-functie is beschikbaar nadat de publicatieportal hello, is geherstructureerd tooonly functionaliteiten gerelateerde toomanaging Hallo-portal voor ontwikkelaars bevatten.</sup>  


## <a name="custom-roles"></a>Aangepaste rollen
Als geen van de ingebouwde rollen Hallo aan uw specifieke behoeften, aangepaste rollen kunnen worden gemaakt tooprovide meer gedetailleerd toegangsbeheer voor API Management-entiteiten. U kunt bijvoorbeeld een aangepaste rol die alleen-lezentoegang tooan API Management-service heeft, maar alleen specifieke schrijftoegang tooone-API maken. toolearn meer informatie over aangepaste rollen Zie [aangepaste rollen in Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles). 

Wanneer u een aangepaste rol maakt, is het eenvoudiger toostart met een van de ingebouwde rollen Hallo. Hallo kenmerken tooadd Hallo acties, NotActions of AssignableScopes bewerken en vervolgens Hallo wijzigingen opslaan als een nieuwe rol. Hallo volgende voorbeeld begint met de rol van de 'Azure API Management Service lezer' Hallo en maakt u een aangepaste beveiligingsrol 'Rekenmachine-API-Editor' genoemd. Hallo aangepaste rol kan worden toegewezen alleen tooa die specifieke API daarom alleen wordt toegang toothat API. 

```
$role = Get-AzureRmRoleDefinition "API Management Service Reader Role"
$role.Id = $null
$role.Name = 'Calculator API Contributor'
$role.Description = 'Has read access tooContoso APIM instance and write access toohello Calculator API.'
$role.Actions.Add('Microsoft.ApiManagement/service/apis/write')
$role.AssignableScopes.Clear()
$role.AssignableScopes.Add('/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>')
New-AzureRmRoleDefinition -Role $role
New-AzureRmRoleAssignment -ObjectId <object ID of hello user account> -RoleDefinitionName 'Calculator API Contributor' -Scope '/subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.ApiManagement/service/<service name>/apis/<api ID>'
```

## <a name="watch-a-video-overview"></a>Bekijk een Video-overzicht

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Role-Based-Access-Control-in-API-Management/player]
> 
> 

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over toegangsbeheer op basis van rollen in Azure
  * [Aan de slag met toegangsbeheer in hello Azure-portal](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](https://azure.microsoft.com/en-us/documentation/articles/role-based-access-control-what-is/)
  * [Aangepaste rollen in Azure RBAC](https://docs.microsoft.com/en-us/azure/active-directory/role-based-access-control-custom-roles)
