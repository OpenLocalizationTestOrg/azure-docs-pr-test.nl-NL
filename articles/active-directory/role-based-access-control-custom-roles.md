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
# <a name="create-custom-roles-for-azure-role-based-access-control"></a>Aangepaste rollen maken voor op rollen gebaseerd toegangsbeheer
Maak een aangepaste rol in gebaseerd toegangsbeheer (RBAC) als geen van de ingebouwde rollen Hallo voldoet aan de behoeften van uw specifieke toegang. Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface](role-based-access-control-manage-access-azure-cli.md) (CLI) en Hallo [REST-API](role-based-access-control-manage-access-rest.md). Net als de ingebouwde rollen kunt u aangepaste rollen toousers, groepen en toepassingen bij het abonnement, resourcegroep en resource bereiken toewijzen. Aangepaste rollen worden opgeslagen in een Azure AD-tenant en kunnen worden gedeeld door abonnementen.

Elke tenant kunt maken van aangepaste rollen too2000. 

Hallo volgende voorbeeld ziet u een aangepaste rol voor het controleren en opnieuw starten van virtuele machines:

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
## <a name="actions"></a>Acties
Hallo **acties** eigenschap van een aangepaste rol geeft hello Azure-bewerkingen toowhich Hallo rol toegang verleent. Er is een verzameling van bewerking tekenreeksen waarmee beveiligbare bewerkingen van de Azure-resourceproviders. Bewerking tekenreeksen volgt Hallo-indeling van `Microsoft.<ProviderName>/<ChildResourceType>/<action>`. Bewerking tekenreeksen met jokertekens (\*) toegang verlenen tooall-bewerkingen die overeenkomen met de Hallo bewerking tekenreeks. Bijvoorbeeld:

* `*/read`verleent toegang tot tooread bewerkingen voor alle resourcetypen van alle Azure-resourceproviders.
* `Microsoft.Compute/*`verleent toegang tot tooall bewerkingen voor alle brontypen in Hallo Microsoft.Compute-resourceprovider.
* `Microsoft.Network/*/read`verleent toegang tot tooread bewerkingen voor alle brontypen in Hallo Microsoft.Network-resourceprovider van Azure.
* `Microsoft.Compute/virtualMachines/*`verleent toegang tot tooall bewerkingen van virtuele machines en de onderliggende resourcetypen.
* `Microsoft.Web/sites/restart/Action`verleent toegang tot toorestart websites.

Gebruik `Get-AzureRmProviderOperation` (in PowerShell) of `azure provider operations show` (in de Azure CLI) toolist bewerkingen van de Azure-resourceproviders. U kunt ook deze opdrachten tooverify of een tekenreeks bewerking geldig is en tooexpand jokertekens bewerking tekenreeksen.

```
Get-AzureRMProviderOperation Microsoft.Compute/virtualMachines/*/action | FT Operation, OperationName

Get-AzureRMProviderOperation Microsoft.Network/*
```

![Schermafbeelding van de PowerShell - Get-AzureRMProviderOperation](./media/role-based-access-control-configure/1-get-azurermprovideroperation-1.png)

```
azure provider operations show "Microsoft.Compute/virtualMachines/*/action" --js on | jq '.[] | .operation'

azure provider operations show "Microsoft.Network/*"
```

![Azure CLI schermafbeelding - azure-bewerkingen weergeven voor provider "Microsoft.Compute/virtualMachines/ \* /Action" ](./media/role-based-access-control-configure/1-azure-provider-operations-show.png)

## <a name="notactions"></a>NotActions
Gebruik Hallo **NotActions** eigenschap als Hallo reeks bewerkingen die u wenst dat tooallow eenvoudiger wordt gedefinieerd door het met uitzondering van beperkte bewerkingen. Hallo wordt toegang verleend door een aangepaste beveiligingsrol berekend door af te trekken Hallo **NotActions** bewerkingen van het Hallo **acties** bewerkingen.

> [!NOTE]
> Als een gebruiker een rol heeft die worden uitgesloten van een bewerking in toegewezen **NotActions**, en een tweede rol die toegang verleent is toegewezen toohello dezelfde bewerking, Hallo gebruiker is toegestaan tooperform die voor deze bewerking. **NotActions** is niet een weigeren regel – is gewoon de toocreate van een handige manier kan een aantal toegestane bewerkingen wanneer specifieke bewerkingen moeten toobe uitgesloten.
>
>

## <a name="assignablescopes"></a>AssignableScopes
Hallo **AssignableScopes** eigenschap van de aangepaste rol Hallo Hiermee geeft u Hallo scopes (abonnementen, resourcegroepen of bronnen) in welke Hallo aangepaste rol beschikbaar voor toewijzing is. U kunt aangepaste rol Hallo beschikbaar voor toewijzing in Hallo-abonnementen of resourcegroepen waarvoor en niet vol gebruiker ervaring voor de rest Hallo van Hallo abonnementen of resourcegroepen.

Voorbeelden van geldige toewijsbare bereiken zijn:

* "/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e', '/ subscriptions/e91d47c4-76f3-4271-a796-21b4ecfe3624' - maakt Hallo rol beschikbaar voor toewijzing in twee abonnementen.
* '/ subscriptions/c276fc76-9cd4-44c9-99a7-4fd71546436e' - maakt Hallo rol beschikbaar voor toewijzing in één abonnement.
* '/ abonnementen/c276fc76-9cd4-44c9-99a7-4fd71546436e/resourceGroups/netwerk' - zorgt ervoor dat Hallo rol beschikbaar voor toewijzing alleen in de resourcegroep Hallo-netwerk.

> [!NOTE]
> Moet u ten minste één abonnement, resourcegroep of resource-ID.
>
>

## <a name="custom-roles-access-control"></a>Aangepaste rollen toegangsbeheer
Hallo **AssignableScopes** ook de eigenschap van de aangepaste rol Hallo bepaalt wie kunt weergeven, wijzigen en verwijderen van rol Hallo.

* Wie kan een aangepaste beveiligingsrol maken?
    Eigenaars (en beheerders van de gebruiker toegang) van de abonnementen, resourcegroepen en resources kunnen aangepaste rollen maken voor gebruik in deze bereiken.
    Hallo gebruiker maken Hallo rol moet kunnen tooperform toobe `Microsoft.Authorization/roleDefinition/write` bewerking op alle Hallo **AssignableScopes** van Hallo-rol.
* Wie kan een aangepaste rol wijzigen?
    Eigenaars (en beheerders van de gebruiker toegang) van de abonnementen, resourcegroepen en resources aangepaste rollen in deze bereiken kunnen wijzigen. Gebruikers moeten toobe kunnen tooperform hello `Microsoft.Authorization/roleDefinition/write` bewerking op alle Hallo **AssignableScopes** van een aangepaste beveiligingsrol.
* Wie kan aangepaste rollen bekijken?
    Alle ingebouwde rollen in Azure RBAC kunnen bekijken van functies die beschikbaar voor toewijzing zijn. Gebruikers Hallo uitvoeren kunnen `Microsoft.Authorization/roleDefinition/read` bewerking op een scope Hallo RBAC functies die beschikbaar voor toewijzing op dat bereik zijn kunt weergeven.

## <a name="see-also"></a>Zie ook
* [Op rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.
* Meer informatie over hoe toomanage met toegang tot:
  * [PowerShell](role-based-access-control-manage-access-powershell.md)
  * [Azure-CLI](role-based-access-control-manage-access-azure-cli.md)
  * [REST API](role-based-access-control-manage-access-rest.md)
* [Ingebouwde rollen](role-based-access-built-in-roles.md): meer informatie over het Hallo-functies die standaard in RBAC.
