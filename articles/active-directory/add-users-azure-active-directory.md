---
title: aaaAdd nieuwe gebruikers tooAzure Active Directory | Microsoft Docs
description: Legt uit hoe tooadd nieuwe gebruikers in Azure Active Directory.
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Snelstartgids: Nieuwe gebruikers tooAzure Active Directory toevoegen
Dit artikel wordt uitgelegd hoe nieuwe gebruikers in uw organisatie in Azure Active Directory (Azure AD) Hallo tooadd één tegelijk met hello Azure-portal of door het synchroniseren van uw on-premises Windows Server AD-gebruiker account gegevens. 

## <a name="add-cloud-based-users"></a>Cloud-gebaseerde gebruikers toevoegen
1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **Azure Active Directory** en vervolgens **gebruikers en groepen**.
3. Op Hallo **gebruikers en groepen** blade Selecteer **alle gebruikers**, en selecteer vervolgens **nieuwe gebruiker**.
   ![Hallo Add-opdracht selecteren](./media/add-users-azure-active-directory/add-user.png)
4. Voer details voor de gebruiker hello, zoals **naam** en **gebruikersnaam**. Hallo domeingedeelte van gebruikersnaam Hallo moet zijn Hallo initiële standaard domain name '[domeinnaam].onmicrosoft.com' of een geverifieerde niet-gefedereerde [aangepaste domeinnaam](add-custom-domain.md) zoals 'contoso.com'.
5. Kopiëren of anderszins Opmerking Hallo gegenereerd gebruikerswachtwoord zodat u deze informatie toohello gebruiker verstrekt kunt nadat dit proces voltooid is.
6. U kunt desgewenst openen en Hallo gegevens invult in Hallo **profiel** blade, Hallo **groepen** blade of Hallo **functie Directory** blade voor Hallo gebruiker. Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen.
7. Op Hallo **gebruiker** blade Selecteer **maken**.
8. Hallo gegenereerd wachtwoord toohello nieuwe gebruiker veilig distribueren zodat hello gebruiker kunt aanmelden.

> [!TIP]
> U kunt ook gegevens van gebruikersaccounts uit de lokale Windows Server AD synchroniseren. Microsoft identiteitsoplossingen span on-premises en cloud-gebaseerde mogelijkheden tooall netwerkbronnen, ongeacht de locatie van de identiteit van een enkele gebruiker voor verificatie en autorisatie maken. We noemen deze hybride identiteit. [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) gebruikte toointegrate uw on-premises adreslijsten met Azure Active Directory voor hybride identiteit scenario's kan worden. Hiermee kunt u een algemene identiteit voor uw gebruikers voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide. 

## <a name="delete-users-from-azure-ad"></a>Gebruikers verwijderen van Azure AD
1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **gebruikers en groepen**.
3. Op Hallo **gebruikers en groepen** blade, selecteer Hallo gebruiker toodelete uit Hallo-lijst. 
4. Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **overzicht**, en selecteer vervolgens in de opdrachtbalk Hallo **verwijderen**.
   ![Hallo Add-opdracht selecteren](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>Meer informatie 
* [Een externe gebruiker toevoegen](active-directory-users-create-external-azure-portal.md)

* [Een gebruikersrol tooa toewijzen in uw Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Volgende stappen
In deze snelstartgids hebt u geleerd hoe tooadd nieuwe gebruikers tooAzure AD Premium. 

U kunt Hallo volgende koppeling toocreate een nieuwe gebruiker in Azure AD uit hello Azure-portal gebruiken.

> [!div class="nextstepaction"]
> [Toevoegen van gebruikers tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
