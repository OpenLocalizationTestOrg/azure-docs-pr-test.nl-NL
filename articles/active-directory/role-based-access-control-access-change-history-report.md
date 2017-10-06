---
title: aaaAccess rapportage - Azure RBAC | Microsoft Docs
description: Genereer een rapport dat een lijst met alle wijzigingen in de tooyour voor toegang tot Azure-abonnementen met op rollen gebaseerde toegangsbeheer via Hallo afgelopen 90 dagen.
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
ms.assetid: 2bc68595-145e-4de3-8b71-3a21890d13d9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/17/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ad85d3d8e66ce167032638a35e4afffb46d3892
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-access-report-for-role-based-access-control"></a>Een access-rapport maken voor toegangsbeheer op basis van rollen
Elk gewenst moment iemand verleent of trekt u toegang binnen uw abonnementen worden Hallo wijzigingen geregistreerd in Azure gebeurtenissen. U kunt maken toegang wijzigen geschiedenis rapporten toosee alle wijzigingen voor Hallo afgelopen 90 dagen.

## <a name="create-a-report-with-azure-powershell"></a>Een rapport maken met Azure PowerShell
toocreate een toegang wijzigen geschiedenisrapport in PowerShell gebruik Hallo [Get-AzureRMAuthorizationChangeLog](/powershell/module/azurerm.resources/get-azurermauthorizationchangelog) opdracht.

Wanneer u deze opdracht aanroept, kunt u opgeven welke eigenschap van de gewenste weergegeven, met inbegrip van de volgende Hallo Hallo-toewijzingen:

| Eigenschap | Beschrijving |
| --- | --- |
| **Actie** |Hiermee wordt aangegeven of toegang is toegekend of ingetrokken |
| **Aanroeper** |Hallo-eigenaar die verantwoordelijk is voor Hallo toegang wijzigen |
| **PrincipalId** | de unieke id van het Hallo-gebruiker, groep of toepassing die is toegewezen rol Hallo Hallo |
| **Primaire naam** |Hallo-naam van het Hallo-gebruiker, groep of toepassing |
| **PrincipalType** |Hiermee wordt aangegeven of Hallo-toewijzing voor een gebruiker, groep of toepassing is |
| **RoleDefinitionId** |Hallo GUID van het Hallo-rol die is toegekend of ingetrokken |
| **Rolnaam** |Hallo-rol die is toegekend of ingetrokken |
| **Bereik** | Hallo unieke id van Hallo abonnement, resourcegroep of resource die Hallo toewijzing is van toepassing te| 
| **ScopeName** |Hallo-naam van het Hallo-abonnement, resourcegroep of resource |
| **ScopeType** |Hiermee wordt aangegeven of Hallo-toewijzing is op het Hallo-abonnement, resourcegroep of resource bereik |
| **Tijdstempel** |Hallo-datum en tijd waarop de toegang is gewijzigd |

Deze opdracht worden alle toegang wijzigingen in het abonnement voor Hallo Hallo afgelopen zeven dagen:

```
Get-AzureRMAuthorizationChangeLog -StartTime ([DateTime]::Now - [TimeSpan]::FromDays(7)) | FT Caller,Action,RoleName,PrincipalType,PrincipalName,ScopeType,ScopeName
```

![PowerShell Get-AzureRMAuthorizationChangeLog - schermafbeelding](./media/role-based-access-control-configure/access-change-history.png)

## <a name="create-a-report-with-azure-cli"></a>Een rapport maken met Azure CLI
een geschiedenisrapport voor gewijzigde van toegang in hello Azure-opdrachtregelinterface (CLI) toocreate gebruiken Hallo `azure role assignment changelog list` opdracht.

## <a name="export-tooa-spreadsheet"></a>Werkblad tooa exporteren
toosave rapport Hallo of Hallo gegevens bewerken, export Hallo toegang verandert in een CSV-bestand. U kunt vervolgens Hallo rapport weergeven in een werkblad voor controle.

![Changelog weergegeven als werkblad - schermafbeelding](./media/role-based-access-control-configure/change-history-spreadsheet.png)

## <a name="next-steps"></a>Volgende stappen
* Werken met [aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md)
* Meer informatie over hoe toomanage [Azure RBAC met powershell](role-based-access-control-manage-access-powershell.md)

