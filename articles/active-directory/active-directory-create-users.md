---
title: aaaAdd nieuwe gebruikers tooAzure Active Directory | Microsoft Docs
description: Legt uit hoe nieuwe gebruikers tooadd gebruikersgegevens in Azure Active Directory of wijzigen.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a>Nieuwe gebruikers toevoegen of met Microsoft-accounts tooAzure Active Directory
Toevoegen van gebruikers toopopulate uw directory. Dit artikel wordt uitgelegd hoe tooadd nieuwe gebruikers in uw organisatie en hoe tooadd gebruikers die Microsoft-account. Zie [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md) (Engelstalig) voor meer informatie over het toevoegen van gebruikers van andere directory's in Azure Active Directory of over het toevoegen van gebruikers van partnerbedrijven. Toegevoegde gebruikers hebben geen beheerdersrechten standaard, maar u kunt functies toothem toewijzen op elk gewenst moment.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Voor hoe tooadd een gebruiker in hello Azure AD-beheercentrum, Zie [toevoegen van nieuwe gebruikers tooAzure Active Directory](active-directory-users-create-azure-portal.md).

## <a name="add-a-user"></a>Een gebruiker toevoegen
1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) met een account met globale beheerdersrechten voor Hallo-directory.
2. Selecteer **Active Directory**, en selecteer vervolgens Hallo-naam van de organisatiedirectory.
3. Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens in de opdrachtbalk Hallo **gebruiker toevoegen**.
4. Op Hallo **Vertel ons meer over deze gebruiker** pagina onder **Type gebruiker**, selecteer:

   * **Nieuwe gebruiker in uw organisatie**: hiermee voegt u een nieuw gebruikersaccount toe aan uw directory.
   * **Gebruiker met een bestaand Microsoft-account** – voegt u een bestaande Microsoft consumer account tooyour map (bijvoorbeeld een Outlook-account)
5. Afhankelijk van de waarde van **Type gebruiker** voert u een gebruikersnaam in (voor de nieuwe gebruiker) of een e-mailadres (voor een gebruiker met een Microsoft-account).
6. Op gebruiker Hallo **profiel** pagina, Geef een naam en achternaam, een gebruiksvriendelijke naam en een gebruikersrol uit Hallo **rollen** lijst. Zie [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md) (Engelstalig) voor meer informatie over gebruikers- en beheerdersrollen. Opgeven of te**multi-factor Authentication inschakelen** voor Hallo-gebruiker.
7. Op Hallo **tijdelijk wachtwoord** pagina **maken**.

> [!IMPORTANT]
> Als uw organisatie meer dan één domein gebruikt, moet u weten over Hallo problemen te volgen wanneer u een gebruikersaccount toevoegen:
>
> * tooadd gebruikersaccounts met dezelfde UPN (User Principal Name) in meerdere domeinen, Hallo **eerste** toevoegen, bijvoorbeeld geoffgrisso@contoso.onmicrosoft.com, **gevolgd door** geoffgrisso@contoso.com.
> * Voeg geoffgrisso@contoso.com **niet** vóór geoffgrisso@contoso.onmicrosoft.com toe. Deze volgorde is belangrijk en omslachtige tooundo kan zijn.
>
>

## <a name="change-user-information"></a>Gebruikersgegevens wijzigen
U kunt elk gebruikerskenmerk, met uitzondering van Hallo object-ID.

1. Open uw directory.
2. Selecteer Hallo **gebruikers** tabblad en selecteer vervolgens Hallo weergavenaam van de gebruiker die u wilt dat toochange Hallo.
3. Voer de wijzigingen uit en klik vervolgens op **Opslaan**.

Als het Hallo-gebruiker die u wilt wijzigen, is gesynchroniseerd met uw on-premises Active Directory-service, kunt u gebruikersgegevens Hallo met deze procedure niet wijzigen. toochange hello gebruiker, uw lokale Active Directory-beheerhulpprogramma's gebruiken.

## <a name="guest-user-management-and-limitations"></a>Beheer van gastgebruikers en beperkingen
Gastaccounts zijn accounts van gebruikers uit andere directory's die uitgenodigde tooyour directory tooaccess SharePoint-documenten, toepassingen of andere Azure-resources zijn. Een gastaccount in uw directory heeft de onderliggende UserType-kenmerk ingesteld te 'gast'. Gewone gebruikers (met name de leden van uw directory) hebben Hallo UserType-kenmerk "Lid."

Gasten hebben een beperkte set rechten in Hallo-directory. Deze rechten beperken Hallo mogelijkheid voor gasten toodiscover informatie over andere gebruikers in de directory Hallo. Gastgebruikers kunnen echter wel communiceren met het Hallo-gebruikers en groepen die zijn gekoppeld aan Hallo resources waarmee die ze werken op. Gastgebruikers hebben de volgende mogelijkheden:

* Zie andere gebruikers en groepen die zijn gekoppeld aan een Azure-abonnement toowhich waaraan ze zijn toegewezen
* Zie Hallo leden van groepen toowhich die ze horen
* Opzoeken van andere gebruikers in de directory hello, als ze Hallo volledige e-mailadres van Hallo gebruiker kennen
* Zie een beperkt aantal kenmerken van Hallo gebruikers die ze--de naam van de beperkte toodisplay, e-mailadres, UPN (user Principal name) en een foto van miniatuurformaat opzoeken
* Een lijst met geverifieerde domeinen in de map Hallo ophalen
* Toestemming tooapplications, zodat ze Hallo dezelfde toegang hebben als leden in uw directory hebben

## <a name="set-guest-user-access-policies"></a>Toegangsbeleid instellen voor gasten
Hallo **configureren** tabblad van een directory bevat opties toocontrol toegang van gastgebruikers. Deze opties kunnen alleen worden gewijzigd in de klassieke Azure-portal door een hoofdbeheerder van de directory. Op dit moment is er geen PowerShell- of API-methode beschikbaar.

Hallo tooopen **configureren** tabblad hello Azure classic portal, selecteer **Active Directory**, en selecteer vervolgens de naam Hallo van Hallo-directory.

![Het tabblad Configureren in Azure Active Directory][1]

U kunt vervolgens Hallo opties toocontrol toegang van gastgebruikers bewerken.

![Opties voor het beheren van toegang voor gastgebruikers][2]

## <a name="whats-next"></a>Volgend onderwerp
* [Gebruikers vanuit andere mappen of partnerbedrijven toevoegen in Azure Active Directory](active-directory-create-users-external.md)
* [Administering Azure AD](active-directory-administer.md) (Azure AD beheren)
* [Wachtwoorden beheren in Azure AD](active-directory-manage-passwords.md)
* [Groepen beheren in Azure Active Directory](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
