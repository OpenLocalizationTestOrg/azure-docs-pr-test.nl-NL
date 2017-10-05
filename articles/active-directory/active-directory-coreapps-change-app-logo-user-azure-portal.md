---
title: Wijzig de naam of het logo van een enterprise-app in Azure Active Directory | Microsoft Docs
description: Het wijzigen van de naam of het logo voor een aangepaste enterprise-app in Azure Active Directory
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d01303ce-e6cb-4f3b-a4d6-ec29dfd68146
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: curtand
ms.openlocfilehash: 3e44e876dcbac704a9809ae5b3957bf94be21c48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-name-or-logo-of-an-enterprise-app-in-azure-active-directory"></a>De naam of het logo van een enterprise-app in Azure Active Directory wijzigen
Het is gemakkelijk om te wijzigen van de naam of het logo voor een aangepaste toepassing in Azure Active Directory (Azure AD). U moet de juiste machtigingen voor u deze wijzigingen hebben en u moet de maker van de aangepaste app.

## <a name="how-do-i-change-an-enterprise-apps-name-or-logo"></a>Hoe wijzig ik de naam of het logo een enterprise-app?
1. Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **meer services**, voer **Azure Active Directory** in het tekstvak in en selecteer vervolgens **Enter**.
3. Op de **Azure Active Directory - *directoryname***  blade (dat wil zeggen, de Azure AD blade voor de map die u beheert), selecteer **bedrijfstoepassingen**.

    ![Openen zakelijke apps](./media/active-directory-coreapps-change-app-logo-azure-portal/open-enterprise-apps.png)
4. Op de **bedrijfstoepassingen** blade Selecteer **alle toepassingen**. Hier ziet u een lijst met de apps die u kunt beheren.
5. Op de **bedrijfstoepassingen - alle toepassingen** blade, selecteert u een app.
6. Op de ***appname*** blade (dat wil zeggen, de blade met de naam van de geselecteerde app in de titel), selecteer **eigenschappen**.

    ![De opdracht Eigenschappen selecteren](./media/active-directory-coreapps-change-app-logo-azure-portal/select-app.png)
7. Op de ***appname*** **-eigenschappen** blade, blader naar een bestand om te gebruiken als een nieuwe logo of bewerken van de app-naam of beide.

    ![Het wijzigen van de app-logo of nameproperties-opdracht](./media/active-directory-coreapps-change-app-logo-azure-portal/change-logo.png)
8. Selecteer de **opslaan** opdracht.

## <a name="next-steps"></a>Volgende stappen
* [Zie al mijn groepen](active-directory-groups-view-azure-portal.md)
* [Een gebruiker of groep toewijzen aan een enterprise-app](active-directory-coreapps-assign-user-azure-portal.md)
* [De toewijzing van een gebruiker of groep verwijderen uit een enterprise-app](active-directory-coreapps-remove-assignment-azure-portal.md)
* [Uitschakelen van de gebruikersaanmeldingen voor een enterprise-app](active-directory-coreapps-disable-app-azure-portal.md)
