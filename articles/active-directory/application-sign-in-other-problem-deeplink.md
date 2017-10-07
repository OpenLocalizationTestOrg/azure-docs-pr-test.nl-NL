---
title: aaaProblems tooan toepassing met behulp van een deeplink aanmelden | Microsoft Docs
description: Hoe tootroubleshoot problemen met toegang tot een toepassing van een gebruikmaken van Azure AD-deeplink-URL
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
ms.openlocfilehash: dc82410001ac05895cc0244c3a89ace71bcf01a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problems-signing-in-tooan-application-using-a-deeplink"></a>Problemen met aanmelden met een deeplink tooan-toepassing

Hallo Toegangspaneel is een portal op Internet waarmee een gebruiker met een werk of schoolaccount in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen die hello Azure AD-beheerder heeft deze toegang verleend tot. 

Deze toepassingen zijn geconfigureerd namens de gebruiker Hallo in hello Azure AD-portal. Hallo-toepassing moet correct worden geconfigureerd en toegewezen toohello gebruiker of een groep Hallo-gebruiker lid is van toepassing op Hallo toosee in Hallo Toegangsvenster.

Dieptekoppelingen of toegang voor gebruikers zijn URL's koppelingen die uw gebruikers hun wachtwoord SSO-toepassingen rechtstreeks vanuit hun browser-URL balken van tooaccess kunnen gebruiken. Door te navigeren toothis koppeling, worden gebruikers automatisch aangemeld bij de toepassing hello zonder toogo toohello Toegangspaneel eerst. Dit is Hallo dezelfde koppeling die gebruikers tooaccess deze toepassingen vanuit Office 365 Hallo toepassing starten gebruiken.

## <a name="general-issues-toocheck-first"></a>Algemene problemen toocheck eerst

-   Zorg ervoor dat uw met een **browser** die voldoet aan de minimale vereisten van de Hallo voor Hallo Toegangsvenster.

-   Zorg ervoor dat de browser van Hallo gebruiker is toegevoegd Hallo-URL van Hallo toepassing tooits **vertrouwde websites**.

-   Zorg ervoor dat toocheck Hallo toepassing **geconfigureerd** correct.

-   Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.

-   Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**

-   Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**

-   Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.

-   Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.

## <a name="checking-hello-deeplink"></a>Hallo-deeplink-controle

toocheck hebt u de juiste deeplink hello, Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

7.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

8.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

9.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

10. Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

11. Selecteer gewenste Hallo selectievakje Hallo deeplink voor Hallo-toepassing.

12. Hallo-label vinden **toegangs-URL van gebruiker**. U deeplink moet overeenkomen met deze URL.

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo

tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:

1.  Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.

2.  Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.

3.  Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.

4.  Op basis van uw browser zijn u gerichte toohello downloadkoppeling. **Voeg** Hallo extensie tooyour browser.

5.  Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.

6.  Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.

7.  Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen

U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:

-   [Uitbreiding van chrome toegang Configuratiescherm](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Uitbreiding van het Configuratiescherm Firefox toegang](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-tooconfigure-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor een toepassing van de galerie van Azure AD

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Een toepassing uit de galerie van Azure AD Hallo toevoegen](#add-an-application-from-the-Azure-AD-gallery)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

### <a name="add-an-application-from-hello-azure-ad-gallery"></a>Een toepassing uit de galerie van Azure AD Hallo toevoegen

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  In Hallo **Voer een naam** textbox van Hallo **toevoegen uit de galerie Hallo** sectie, Hallo typenaam van de toepassing hello.

7.  Selecteer het gewenste tooconfigure voor eenmalige aanmelding Hallo-toepassing.

8.  Voordat u de toepassing hello toevoegt, kunt u de naam van Hallo **naam** textbox.

9.  Klik op **toevoegen** knop tooadd Hallo-toepassing.

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  [Gebruikers toewijzen toohello toepassing](#how-to-assign-a-user-to-an-application-directly).

10. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="how-tooconfigure-password-single-sign-on-for-a-non-gallery-application"></a>Hoe tooconfigure wachtwoord eenmalige aanmelding voor de toepassing van een niet-galerie

een toepassing uit de galerie van Azure AD Hallo tooconfigure moet u:

-   [Toevoegen van een toepassing niet-galerie](#add-a-non-gallery-application)

-   [Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren](#configure-the-application-for-password-single-sign-on)

### <a name="add-a-non-gallery-application"></a>Toevoegen van een toepassing niet-galerie

een toepassing hello Azure AD-galerie tooadd Hallo volgende stappen:

1.  Open Hallo [Azure Portal](https://portal.azure.com) en meld u aan als een **hoofdbeheerder** of **Co-beheerder**.

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op Hallo **toevoegen** op Hallo rechterbovenhoek op Hallo knop **bedrijfstoepassingen** blade.

6.  Klik op **Non-galerie-toepassing.**

7.  Vul in Hallo Hallo-naam van uw toepassing **naam** textbox. Selecteer **toevoegen.**

Na een korte periode zijn u configuratie-blade kunnen toosee Hallo toepassing.

### <a name="configure-hello-application-for-password-single-sign-on"></a>Hallo-toepassing voor eenmalige aanmelding wachtwoord configureren

Volg onderstaande stappen voor Hallo tooconfigure eenmalige aanmelding voor een toepassing:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

    1.  Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Voer Hallo **aanmeldings-URL**. Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen. Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar tijdens het Hallo-URL.

10. Gebruikers toohello toepassing toewijzen.

11. Bovendien kunt u ook referenties opgeven namens de gebruiker Hallo door het selecteren van rijen Hallo Hallo-gebruikers en te klikken op **updatereferenties** en Hallo gebruikersnaam en wachtwoord in te voeren namens Hallo gebruikers. Anders worden gebruikers na vragen aan gebruiker tooenter Hallo referenties zelf bij het starten.

## <a name="how-tooassign-a-user-tooan-application-directly"></a>Hoe een gebruiker tooan toepassing rechtstreeks tooassign

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

Hallo Toegangsvenster na een korte periode Hallo-gebruikers die u hebt geselecteerd niet kunnen toolaunch deze toepassingen in.

## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a>Als u deze stappen voor probleemoplossing niet Hallo Hallo probleem oplossen 

Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:

-   Correlatie fout-ID

-   UPN (e-mailadres van de gebruiker)

-   TenantID

-   Browsertype

-   Tijdzone en de tijd/tijdsbestek tijdens fout optreedt

-   Fiddler traceringen

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
