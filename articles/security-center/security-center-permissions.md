---
title: aaaPermissions in Azure Security Center | Microsoft Docs
description: In dit artikel wordt uitgelegd hoe Azure Security Center gebruikt voor toegang op basis van rollen besturingselement tooassign machtigingen toousers en identificeert Hallo toegestane acties voor elke rol.
services: security-center
cloud: na
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
ms.assetid: 
ms.service: security-center
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: terrylan
ms.openlocfilehash: 03e16132dc3d951ef8ad9e86b9970b9e4d15c76b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="permissions-in-azure-security-center"></a>Machtigingen in Azure Security Center

Maakt gebruik van Azure Security Center [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md), waarmee u [ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md) die kunnen worden toegewezen toousers, groepen en services in Azure.

Security Center beoordeelt Hallo-configuratie van uw resources tooidentify beveiligingsproblemen en beveiligingsproblemen. In Security Center, ziet u alleen informatie gerelateerd tooa resource wanneer u Hallo rol van eigenaar, bijdrager of lezer Hallo abonnement of resourcegroep beheergroep die deel uitmaakt van een resource te worden toegewezen.

In aanvulling toothese rollen zijn er twee specifieke Security Center-rollen:

* **Beveiliging lezer**: een gebruiker die deel uitmaakt van de rol toothis heeft rechten tooSecurity Center weer te geven. Hallo-gebruiker kunt bekijken aanbevelingen, waarschuwingen, een beveiligingsbeleid en beveiliging, maar geen wijzigingen aanbrengen.
* **Beveiligingsbeheerder**: een gebruiker die deel uitmaakt van de rol toothis Hallo dezelfde als Hallo beveiliging lezer rechten heeft en kan ook bijwerken Hallo-beveiligingsbeleid en negeren van waarschuwingen en aanbevelingen.

> [!NOTE]
> Hallo beveiligingsrollen, beveiliging lezer en Beveiligingsbeheerder, hebben toegang alleen in Security Center. Hallo beveiligingsrollen hebt geen toegang tooother servicegebieden van Azure zoals opslag, Web & mobiele of Internet der dingen.
>
>

## <a name="roles-and-allowed-actions"></a>Functies en de toegestane acties

Hallo volgende tabel geeft de rollen en toegestane acties in Security Center. Een X geeft aan dat het Hallo-actie is toegestaan voor die rol.

| Rol | Beveiligingsbeleid bewerken | Aanbevelingen voor beveiliging voor een resource toepassen | Negeren van waarschuwingen en aanbevelingen | Waarschuwingen weergeven en aanbevelingen |
|:--- |:---:|:---:|:---:|:---:|
| De eigenaar van abonnement | X | X | X | X |
| Abonnement Inzender | X | X | X | X |
| De eigenaar van de resourcegroep | -- | X | -- | X |
| Resourcegroep Inzender | -- | X | -- | X |
| Lezer | -- | -- | -- | X |
| Beveiligingsbeheerder | X | -- | X | X |
| Beveiliging lezer | -- | -- | -- | X |

> [!NOTE]
> Het is raadzaam dat u Hallo toewijst minimaal rol die nodig zijn voor gebruikers toocomplete hun taken. Bijvoorbeeld toewijzen Hallo lezer rol toousers die alleen tooview informatie over de beveiligingsstatus Hallo van een resource nodig hebt, maar geen actie uitvoert, zoals het toepassen van aanbevelingen of het bewerken van beleid.
>
>

## <a name="next-steps"></a>Volgende stappen
Dit artikel uitgelegd hoe Security Center RBAC tooassign machtigingen toousers gebruikt en geïdentificeerd Hallo toegestane acties voor elke rol. Nu u bekend met de roltoewijzingen Hallo nodig toomonitor Hallo beveiligingsstatus van uw abonnement bent, beveiligingsbeleid, bewerken en toepassen van aanbevelingen, informatie over hoe:

- [Instellen van beveiligingsbeleid in Security Center](security-center-policies.md)
- [Aanbevelingen voor beveiliging in Security Center beheren](security-center-recommendations.md)
- [Hallo beveiligingsstatus van uw Azure-resources bewaken](security-center-monitoring.md)
- [Beheren en hierop reageren toosecurity waarschuwingen in Security Center](security-center-managing-and-responding-alerts.md)
- [Bewaken van beveiligingsoplossingen van partners](security-center-partner-solutions.md)
