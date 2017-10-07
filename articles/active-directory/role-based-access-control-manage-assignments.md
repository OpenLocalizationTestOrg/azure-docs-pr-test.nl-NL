---
title: toewijzingen aaaView Azure-resource-access | Microsoft Docs
description: Weergeven en beheren van alle toewijzingen van Hallo toegangsbeheer op basis van rollen voor elke gebruiker of groep in hello Azure-portal
services: active-directory
documentationcenter: 
author: andredm7
manager: femila
editor: jeffsta
ms.assetid: e6f9e657-8ee3-4eec-a21c-78fe1b52a005
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/04/2017
ms.author: andredm
ms.openlocfilehash: ec96c9d4b9e2cb4925949b8bac78767bd564c8ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-access-assignments-for-users-and-groups-in-hello-azure-portal"></a>Toegang tot toewijzingen weergeven voor gebruikers en groepen in hello Azure-portal
> [!div class="op_single_selector"]
> * [Toegang beheren per gebruiker of groep](role-based-access-control-manage-assignments.md)
> * [Toegang beheren per resource](role-based-access-control-configure.md)

Met op rollen gebaseerde toegangsbeheer (RBAC) in hello Azure Active Directory (Azure AD), kunt u access tooyour Azure beheren resources. 

Toegang met RBAC toegewezen is fijnmazig omdat er zijn twee manieren kunt u Hallo machtigingen beperken:

* **Bereik:** RBAC-roltoewijzingen zijn binnen het bereik tooa specifiek abonnement, resourcegroep of resource. Een gebruiker toegang tooa één resource krijgt geen toegang tot alle andere resources in Hallo hetzelfde abonnement.
* **Rol:** binnen het bereik van de Hallo van Hallo toewijzing, de toegang wordt teruggebracht nog verder door een rol toewijst. Rollen kunnen worden op hoog niveau, zoals eigenaar of specifieke, zoals de lezer van de virtuele machine.

Rollen kunnen alleen binnen het Hallo-abonnement, resourcegroep of resource die Hallo bereik voor de toewijzing van Hallo worden toegewezen. Maar u kunt alle Hallo toegangstoewijzingen voor een bepaalde gebruiker of groep bekijken op één plaats. U kunt up too2000 roltoewijzingen in elk abonnement hebben. 

Meer informatie over het te verkrijgen[rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](role-based-access-control-configure.md).

## <a name="view-access-assignments"></a>De toewijzingen toegang weergeven
toolook up Hallo toegangstoewijzingen voor een enkele gebruiker of groep te starten in Azure Active Directory in Hallo [Azure-portal](http://portal.azure.com).

1. Selecteer **Azure Active Directory**. Als deze optie niet zichtbaar in de navigatie-lijst is, selecteert u **meer Services** en schuif omlaag toofind **Azure Active Directory**.
2. Selecteer **gebruikers en groepen**, en selecteer vervolgens **alle gebruikers** of **alle groepen**. In dit voorbeeld richten we op afzonderlijke gebruikers.
    ![Beheren van gebruikers en groepen in Azure Active Directory - schermafbeelding](./media/role-based-access-control-manage-assignments/rbac_users_groups.png)
3. Hallo gebruiker zoeken op naam of gebruikersnaam.
4. Selecteer **Azure-resources** op Hallo gebruiker blade. Alle Hallo toegangstoewijzingen voor die gebruiker weergegeven.

### <a name="read-permissions-tooview-assignments"></a>Leesmachtigingen tooview toewijzingen
Deze pagina bevat alleen Hallo toegangstoewijzingen u tooread machtiging hebt. Bijvoorbeeld: u hebt leestoegang toosubscription A en ga toohello Azure-resources blade toocheck toewijzingen van een gebruiker. U kunt zien haar toegangstoewijzingen voor een abonnement, maar niet zien dat zij ook toegangstoewijzingen op abonnement B. heeft

## <a name="delete-access-assignments"></a>Toegangstoewijzingen verwijderen
U kunt via deze blade toegangstoewijzingen die rechtstreeks zijn toegewezen tooa gebruiker of groep verwijderen. Als Hallo toegang toewijzing is overgenomen van een bovenliggende groep, kunt u toogo toohello resource of -abonnement nodig hebt en er Hallo-toewijzing te beheren.

1. Selecteer Hallo een gewenste toodelete in Hallo lijst van alle Hallo toegangstoewijzingen voor een gebruiker of groep.
2. Selecteer **verwijderen** en vervolgens **Ja** tooconfirm.
    ![Verwijder toegang toewijzing - schermafbeelding](./media/role-based-access-control-manage-assignments/delete_assignment.png)

## <a name="next-steps"></a>Volgende stappen

* Aan de slag met toegangsbeheer op basis van rollen te[rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](role-based-access-control-configure.md)
* Zie Hallo [ingebouwde RBAC-rollen](role-based-access-built-in-roles.md)

