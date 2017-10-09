---
title: aaaDisable gebruikersaanmeldingen een enterprise-App in Azure Active Directory | Microsoft Docs
description: Hoe toodisable een zakelijke toepassing die geen gebruikers zich tooit in Azure Active Directory aanmelden kunnen
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: a27562f9-18dc-42e8-9fee-5419566f8fd7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 4c560b59359d433b0852a7606cc2cc0204866234
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="disable-user-sign-ins-for-an-enterprise-app-in-azure-active-directory"></a>Gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen
Het is gemakkelijk toodisable een zakelijke toepassing zodat geen gebruikers zich tooit in Azure Active Directory (Azure AD aanmelden kunnen). U moet Hallo gemachtigd toomanage Hallo enterprise app, en moet u hoofdbeheerder voor Hallo-directory.

## <a name="how-do-i-disable-user-sign-ins"></a>Hoe schakel ik gebruikersaanmelding
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.
3. Op Hallo **Azure Active Directory** -  ***directoryname*** blade (dat wil zeggen hello Azure AD blade voor Hallo-directory die u beheert), selecteer **bedrijfstoepassingen**.

    ![Openen zakelijke apps](./media/active-directory-coreapps-disable-app-azure-portal/open-enterprise-apps.png)
4. Op Hallo **bedrijfstoepassingen** blade Selecteer **alle toepassingen**. U ziet een lijst met Hallo-apps die u kunt beheren.
5. Op Hallo **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.
6. Op Hallo ***appname*** blade (dat wil zeggen, Hallo blade met de naam van de geselecteerde app Hallo in Hallo titel Hallo), selecteer **eigenschappen**.

    ![Opdracht voor alle toepassingen selecteren Hallo](./media/active-directory-coreapps-disable-app-azure-portal/select-app.png)
7. Op Hallo ***appname*** - **eigenschappen** blade Selecteer **Nee** voor **ingeschakeld voor gebruikers toosign in?**.
8. Selecteer Hallo **opslaan** opdracht.

## <a name="next-steps"></a>Volgende stappen
* [Mijn groepen bekijken](active-directory-groups-view-azure-portal.md)
* [Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)
* [De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Hallo-naam of het logo van een enterprise-app wijzigen](active-directory-coreapps-change-app-logo-user-azure-portal.md)
