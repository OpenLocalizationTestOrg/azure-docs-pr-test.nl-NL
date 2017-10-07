---
title: aaaManage hello groepen uw groep behoort tooin Azure Active Directory | Microsoft Docs
description: Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier ziet u hoe toomanage deze lidmaatschappen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e785c2d0-7724-47d4-a56e-c58280c08a14
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0a0a1967084de0968e1e802559f9cdfd7ca6ae4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-toowhich-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Toowhich groepen die deel uitmaakt van een groep in uw Azure Active Directory-tenant beheren
Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier ziet u hoe toomanage deze lidmaatschappen.

## <a name="how-do-i-find-hello-groups-my-group-is-a-member-of"></a>Hoe kan ik mijn groep deel uit van maakt Hallo-groepen vinden?
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.

   ![Openen Hallo groepen blade](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Op Hallo **gebruikers en groepen - alle groepen** blade, selecteert u een groep.
5. Op Hallo **groep - *groupname***  blade Selecteer **groepslidmaatschappen**.

   ![Blade met lidmaatschappen Hallo openen](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. tooadd uw groep als lid van een andere groep, op Hallo **Group - groepslidmaatschappen** blade, selecteer Hallo **toevoegen** opdracht.
7. Selecteer een groep in Hallo **groep selecteren** blade en selecteer vervolgens Hallo **Selecteer** knop Hallo Hallo blade onderaan in. U kunt uw tooonly één groep tegelijk toevoegen. Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat. Er is geen jokertekens worden in dit vak geaccepteerd.

   ![Geen groepslidmaatschap toevoegen](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. tooremove uw groep als lid van een andere groep, op Hallo **Group - groepslidmaatschappen** blade, selecteert u een groep.
9. Op Hallo ***groupname*** blade, selecteer Hallo **verwijderen** opdracht in en Bevestig uw keuze op Hallo-prompt.

   ![lidmaatschap opdracht verwijderen](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Wanneer u klaar bent met het wijzigen van groepslidmaatschappen voor uw groep, selecteert u **opslaan**.

## <a name="additional-information"></a>Aanvullende informatie
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Een nieuwe groep maken en leden toe te voegen](active-directory-groups-create-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Leden van een groep beheren](active-directory-groups-members-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
