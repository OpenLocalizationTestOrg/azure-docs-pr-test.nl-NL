---
title: de toewijzing van een gebruiker of groep van een enterprise-app in Azure Active Directory aaaRemove | Microsoft Docs
description: Hoe tooremove Hallo toegang krijgen tot de toewijzing van een gebruiker of groep van een enterprise-app in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 7b2d365b-ae92-477f-9702-353cc6acc5ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: c067ecf59b4dedfe8f848357ca8bd545bdc610eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-a-user-or-group-assignment-from-an-enterprise-app-in-azure-active-directory"></a>De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory
Het is gemakkelijk tooremove een gebruiker of een groep toegang tooone van uw zakelijke toepassingen in Azure Active Directory (Azure AD) wordt toegewezen. U moet Hallo gemachtigd toomanage Hallo enterprise app, en moet u hoofdbeheerder voor Hallo-directory.

## <a name="how-do-i-remove-a-user-or-group-assignment"></a>Hoe kan ik een gebruiker of groepstoewijzing verwijderen?
1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak Hallo en selecteer vervolgens **Enter**.
3. Op Hallo **Azure Active Directory - *directoryname***  blade (dat wil zeggen hello Azure AD blade voor Hallo-directory die u beheert), selecteer **bedrijfstoepassingen**.

    ![Openen zakelijke apps](./media/active-directory-coreapps-remove-assignment-user-azure-portal/open-enterprise-apps.png)
4. Op Hallo **bedrijfstoepassingen** blade Selecteer **alle toepassingen**. Hier ziet u een lijst met Hallo-apps die u kunt beheren.
5. Op Hallo **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.
6. Op Hallo ***appname*** blade (dat wil zeggen, Hallo blade met de naam van de geselecteerde app Hallo in Hallo titel Hallo), selecteer **gebruikers en groepen**.

    ![Gebruikers of groepen selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-app-users.png)
7. Op Hallo ***appname*** **-gebruiker & groepstoewijzing** blade een van meer gebruikers of groepen selecteren en selecteer vervolgens Hallo **verwijderen** opdracht. Bevestig uw beslissing Hallo een opdrachtprompt.

    ![De opdracht Remove Hallo selecteren](./media/active-directory-coreapps-remove-assignment-user-azure-portal/remove-users.png)

## <a name="next-steps"></a>Volgende stappen
* [Zie al mijn groepen](active-directory-groups-view-azure-portal.md)
* [Toewijzen van een gebruiker of groep tooan enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)
* [Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app](active-directory-coreapps-disable-app-azure-portal.md)
* [Hallo-naam of het logo van een enterprise-app wijzigen](active-directory-coreapps-change-app-logo-user-azure-portal.md)
