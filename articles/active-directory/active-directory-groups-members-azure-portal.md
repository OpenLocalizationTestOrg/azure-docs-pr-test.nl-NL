---
title: aaaManage hello leden voor een groep in Azure Active Directory | Microsoft Docs
description: Hoe tooadd of gebruikers en apparaten verwijderen uit een groep in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d399a97d-fd2a-4b2d-b73d-0975db83f41b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4cb16ee63828003da251423a04736f7174dd4896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-group-membership-for-users-in-your-azure-active-directory-tenant"></a>Groepslidmaatschap voor gebruikers in uw Azure Active Directory-tenant beheren
Dit artikel wordt uitgelegd hoe toomanage Hallo leden voor een groep in Azure Active Directory (Azure AD).

## <a name="how-do-i-find-hello-members-and-manage-them"></a>Hoe ik Hallo leden zoeken en deze beheren?
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-groups-members-azure-portal/search-user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.

   ![Openen Hallo groepen blade](./media/active-directory-groups-members-azure-portal/view-groups-blade.png)
4. Op Hallo **gebruikers en groepen - alle groepen** blade, selecteert u een groep.
5. Op Hallo **groep - *groupname***  blade Selecteer **leden**.

   ![Openen Hallo leden blade](./media/active-directory-groups-members-azure-portal/view-group-members.png)
6. tooadd leden toohello groep op Hallo **groep - leden** blade Selecteer **leden toevoegen**.

   ![De opdracht leden toevoegen](./media/active-directory-groups-members-azure-portal/add-group-members-command.png)
7. Op Hallo **leden** blade, selecteert u een of meer gebruikers of apparaten tooadd toohello groep en selecteer Hallo **Selecteer** knop Hallo Hallo blade tooadd onder aan deze groep toohello. Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat. Er is geen jokertekens worden in dit vak geaccepteerd.
8. tooremove leden uit de groep hello, op Hallo **groep - leden** blade, selecteert u een lid.
9. Op Hallo ***membername*** blade, selecteer Hallo **verwijderen** opdracht in en Bevestig uw keuze op Hallo-prompt.

   ![Verwijder leden opdracht](./media/active-directory-groups-members-azure-portal/remove-group-members-command.png)
10. Wanneer u klaar bent met het wijzigen van leden voor Hallo groep, selecteert u **opslaan**.

## <a name="additional-information"></a>Aanvullende informatie
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Een nieuwe groep maken en leden toe te voegen](active-directory-groups-create-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Lidmaatschap van een groep beheren](active-directory-groups-membership-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
