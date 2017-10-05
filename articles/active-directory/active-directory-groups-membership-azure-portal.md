---
title: De groepen die uw groep bij Azure Active Directory behoort beheren | Microsoft Docs
description: Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier volgt deze lidmaatschappen beheren.
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
ms.openlocfilehash: 08e04a6590176c4084ca47b4bd6cbb22500eca2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-to-which-groups-a-group-belongs-in-your-azure-active-directory-tenant"></a>Beheren welke groepen door een groep behoort in uw Azure Active Directory-tenant
Groepen kunnen andere Azure Active Directory-groepen bevatten. Hier volgt deze lidmaatschappen beheren.

## <a name="how-do-i-find-the-groups-my-group-is-a-member-of"></a>Hoe kan ik mijn groep deel uit van maakt groepen vinden?
1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-groups-membership-azure-portal/search-user-management.png)
3. Op de **gebruikers en groepen** blade Selecteer **alle groepen**.

   ![De blade groepen openen](./media/active-directory-groups-membership-azure-portal/view-groups-blade.png)
4. Op de **gebruikers en groepen - alle groepen** blade, selecteert u een groep.
5. Op de **groep - *groupname***  blade Selecteer **groepslidmaatschappen**.

   ![Openen van de groep lidmaatschappen-blade](./media/active-directory-groups-membership-azure-portal/group-membership-blade.png)
6. Uw groep toevoegen als lid van een andere groep, op de **Group - groepslidmaatschappen** blade, selecteer de **toevoegen** opdracht.
7. Selecteer een groep in de **groep selecteren** blade en selecteer vervolgens de **Selecteer** knop aan de onderkant van de blade. U kunt uw groep toevoegen aan slechts één groep tegelijk. De **gebruiker** vak gefilterd op basis van overeenkomst van uw invoer voor een deel van de naam van een gebruiker of het apparaat weergegeven. Er is geen jokertekens worden in dit vak geaccepteerd.

   ![Geen groepslidmaatschap toevoegen](./media/active-directory-groups-membership-azure-portal/add-group-membership.png)
8. Verwijderen van uw groep als lid van een andere groep voor de **Group - groepslidmaatschappen** blade, selecteert u een groep.
9. Op de ***groupname*** blade, selecteer de **verwijderen** opdracht in en Bevestig uw keuze bij de opdrachtprompt.

   ![lidmaatschap opdracht verwijderen](./media/active-directory-groups-membership-azure-portal/remove-group-membership.png)
10. Wanneer u klaar bent met het wijzigen van groepslidmaatschappen voor uw groep, selecteert u **opslaan**.

## <a name="additional-information"></a>Aanvullende informatie
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Een nieuwe groep maken en leden toe te voegen](active-directory-groups-create-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Leden van een groep beheren](active-directory-groups-members-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
