---
title: een groep voor gebruikers in Azure Active Directory aaaCreate | Microsoft Docs
description: Hoe toocreate een groep in Azure Active Directory en leden toohello groep toevoegen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cc5f232a-1e77-45c2-b28b-1fcb4621725c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc583a7f02ce50e7f3b2c8f97a9c032a3e2dc33a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-group-and-add-members-in-azure-active-directory"></a>Een groep maken en leden toevoegen in Azure Active Directory
> [!div class="op_single_selector"]
> * [Azure Portal](active-directory-groups-create-azure-portal.md)
> * [Klassieke Azure Portal](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Dit artikel wordt uitgelegd hoe toocreate en een nieuwe groep in Azure Active Directory te vullen. Een groep tooperform beheertaken, zoals het toewijzen van licenties of machtigingen tooa aantal gebruikers of apparaten tegelijkertijd gebruiken.

## <a name="how-do-i-create-a-group"></a>Hoe maak ik een groep?
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

   ![Gebruikersbeheer openen](./media/active-directory-groups-create-azure-portal/search-user-management.png)
3. Op Hallo **gebruikers en groepen** blade Selecteer **alle groepen**.

   ![Openen Hallo groepen blade](./media/active-directory-groups-create-azure-portal/view-groups-blade.png)
4. Op Hallo **gebruikers en groepen - alle groepen** blade, selecteer Hallo **toevoegen** opdracht.

   ![Hallo Add-opdracht selecteren](./media/active-directory-groups-create-azure-portal/add-group-command.png)
5. Op Hallo **groep** blade een naam en beschrijving voor Hallo groep toevoegen.
6. tooselect tooadd toohello groep leden, selecteer **toegewezen** in Hallo **lidmaatschapstype** vak en selecteer vervolgens **leden**. Zie voor meer informatie over hoe toomanage lidmaatschap van een groep dynamisch Hallo [met behulp van kenmerken toocreate van geavanceerde regels voor lidmaatschap](active-directory-groups-dynamic-membership-azure-portal.md).

   ![Tooadd leden selecteren](./media/active-directory-groups-create-azure-portal/select-members.png)
7. Op Hallo **leden** blade, selecteert u een of meer gebruikers of apparaten tooadd toohello groep en selecteer Hallo **Selecteer** knop Hallo Hallo blade tooadd onder aan deze groep toohello. Hallo **gebruiker** vak filters Hallo weergeven op basis van overeenkomst van uw vermelding tooany een deel van naam van een gebruiker of apparaat. Er is geen jokertekens worden in dit vak geaccepteerd.
8. Wanneer u klaar bent met het toevoegen van leden toohello groep, selecteert u **maken** op Hallo **groep** blade.    

   ![Bevestiging van de groep maken](./media/active-directory-groups-create-azure-portal/create-group-confirmation.png)


## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure Active Directory.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Leden van een groep beheren](active-directory-groups-members-azure-portal.md)
* [Lidmaatschap van een groep beheren](active-directory-groups-membership-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)
