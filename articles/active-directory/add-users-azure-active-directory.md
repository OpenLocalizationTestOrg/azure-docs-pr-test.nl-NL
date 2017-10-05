---
title: Nieuwe gebruikers toevoegen aan Azure Active Directory | Microsoft Docs
description: Legt uit hoe u nieuwe gebruikers toevoegen in Azure Active Directory.
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a>Snelstartgids: Nieuwe gebruikers toevoegen aan Azure Active Directory
In dit artikel wordt uitgelegd hoe u nieuwe gebruikers toevoegen in uw organisatie in Azure Active Directory (Azure AD) een op een tijdstip met de Azure portal of door het synchroniseren van uw on-premises Windows Server AD-gegevens voor account van gebruiker. 

## <a name="add-cloud-based-users"></a>Cloud-gebaseerde gebruikers toevoegen
1. Aanmelden bij de [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **Azure Active Directory** en vervolgens **gebruikers en groepen**.
3. Op de **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **nieuwe gebruiker**.
   ![De opdracht Add selecteren](./media/add-users-azure-active-directory/add-user.png)
4. Voer details voor de gebruiker, zoals **naam** en **gebruikersnaam**. Het domeingedeelte van de naam van de gebruikersnaam moet worden de oorspronkelijke standaard domain name '[domeinnaam].onmicrosoft.com' of een geverifieerde niet-gefedereerde [aangepaste domeinnaam](add-custom-domain.md) zoals 'contoso.com'.
5. Kopieer of het wachtwoord van de gebruiker gegenereerde anders opmerking zodat u deze informatie aan de gebruiker verstrekt kunt nadat dit proces voltooid is.
6. U kunt desgewenst openen en vul de informatie in de **profiel** blade de **groepen** blade of de **functie Directory** blade voor de gebruiker. Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.
7. Op de **gebruiker** blade Selecteer **maken**.
8. Het gegenereerde wachtwoord naar de nieuwe gebruiker veilig distribueren zodat de gebruiker zich kan aanmelden.

> [!TIP]
> U kunt ook gegevens van gebruikersaccounts uit de lokale Windows Server AD synchroniseren. Microsoft identiteitsoplossingen span on-premises en cloud-gebaseerde mogelijkheden voor het maken van de identiteit van een enkele gebruiker voor verificatie en autorisatie voor alle netwerkbronnen, ongeacht de locatie. We noemen deze hybride identiteit. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) kan worden gebruikt om uw on-premises adreslijsten integreren met Azure Active Directory voor hybride identiteit scenario's. Hiermee kunt u uw gebruikers een algemene identiteit bieden voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Gebruikers verwijderen van Azure AD
1. Aanmelden bij de [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor de map.
2. Selecteer **gebruikers en groepen**.
3. Op de **gebruikers en groepen** blade, selecteer de gebruiker wilt verwijderen uit de lijst. 
4. Selecteer op de blade voor de geselecteerde gebruiker **overzicht**, en selecteer vervolgens in de opdrachtbalk **verwijderen**.
   ![De opdracht Add selecteren](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Meer informatie 
* [Een externe gebruiker toevoegen](active-directory-users-create-external-azure-portal.md)

* [Een gebruiker toewijzen aan een rol in uw Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe u nieuwe gebruikers toevoegen aan Azure AD Premium. 

De volgende koppeling kunt u een nieuwe gebruiker in Azure AD via de Azure portal maken.

> [!div class="nextstepaction"]
> [Gebruikers toevoegen aan Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 