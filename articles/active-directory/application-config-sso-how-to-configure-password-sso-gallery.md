---
title: aaaHow tooconfigure wachtwoord eenmalige aanmelding voor een galerie van Azure AD-toepassing | Microsoft Docs
description: Hoe tooconfigure voor een toepassing beveiligen op basis van wachtwoorden eenmalige aanmelding als deze al wordt vermeld in hello Azure AD-Toepassingsgalerie
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 7a93bff119b477d946368686fc2d9006ca2722a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor een galerie van Azure AD-toepassing

Wanneer u een toepassing toevoegen van Hallo [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery), u Hallo keuze hebt van hoe u wilt dat uw gebruikers toosign in toothat toepassing. U kunt deze keuze op elk gewenst moment configureren met behulp van Hallo **Single Sign-on** navigatie-item op een zakelijke toepassing in Hallo [Azure Portal](https://portal.azure.com/).

Een van de Hallo methoden voor eenmalige aanmelding beschikbaar tooyou Hallo is [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) optie. Dit is een uitstekende manier tooget gestart snel toepassingen integreren met Azure AD en kunt u:

-   Schakel **eenmalige aanmelding voor uw gebruikers** door veilig opslaan en opnieuw wordt afgespeeld gebruikersnamen en wachtwoorden voor de toepassing hello die u hebt geïntegreerd met Azure AD

-   **Ondersteuning voor toepassingen waarvoor meerdere velden aanmelden** voor toepassingen waarvoor meer dan alleen gebruikersnaam en wachtwoord velden toosign in

-   **Hallo labels aanpassen** Hallo gebruikersnaam en wachtwoord invoervelden uw gebruikers te zien op Hallo [toepassing Toegangsvenster](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) wanneer ze hun referenties invoeren

-   Toestaan dat uw **gebruikers** tooprovide hun eigen gebruikersnamen en wachtwoorden voor bestaande toepassing accounts ze handmatig te op Hallo typen zijn [Toegangsvenster toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction)

-   Toestaan dat een **lid is van een bedrijfsgroep Hallo** toospecify Hallo gebruikersnamen en wachtwoorden tooa gebruiker toegewezen met behulp van Hallo [Self-Service toegang tot de toepassing](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) functie

-   Toestaan dat een **beheerder** toospecify Hallo gebruikersnamen en wachtwoorden tooa gebruiker zijn toegewezen met behulp van de referenties van de Update Hallo functie wanneer [toewijzen van een gebruiker tooan-toepassing](#assign-a-user-to-an-application-directly)

-   Toestaan dat een **beheerder** toospecify Hallo gedeelde gebruikersnaam of het wachtwoord dat wordt gebruikt door een groep personen met behulp van de referenties van de Update Hallo functie wanneer [toewijzen van een groep tooan-toepassing](#assign-an-application-to-a-group-directly)

Hieronder wordt beschreven hoe u kunt inschakelen [op basis van wachtwoorden Single Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) tooan-toepassing die al in Hallo [Azure AD-Toepassingsgalerie](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#get-started-with-the-azure-ad-application-gallery).

## <a name="overview-of-steps-required"></a>Overzicht van stappen vereist
een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application-from-the-azure-ad-gallery)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

-   [Hallo toepassing tooa gebruiker of een groep toewijzen](#assign-the-application-to-a-user-or-a-group)

    -   [De toepassing van een gebruiker tooan rechtstreeks toewijzen](#assign-a-user-to-an-application-directly)

    -   [Een groep van toepassingen tooa rechtstreeks toewijzen](#assign-an-application-to-a-group-directly)

## <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

## <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure selecteren

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  [Gebruikers toewijzen toohello toepassing](#assign-a-user-to-an-application-directly).

10. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="assign-a-user-tooan-application-directly"></a>De toepassing van een gebruiker tooan rechtstreeks toewijzen

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.

## <a name="assign-an-application-tooa-group-directly"></a>Een groep van toepassingen tooa rechtstreeks toewijzen

tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.

Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
