---
title: aaaProblem toohello toegang Configuratiescherm website aanmelden | Microsoft Docs
description: Richtlijnen tootroubleshoot problemen die optreden kunnen tijdens een poging toosign in toouse Hallo Toegangsvenster
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
ms.reviwer: japere
ms.openlocfilehash: 1037f7c5fbaa9425760ad5739b383c716d5fc3a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-signing-in-toohello-access-panel-website"></a>Probleem bij aanmelden toohello toegang Configuratiescherm website

Hallo Toegangspaneel is een portal op Internet zodat een gebruiker met een werk- of school-account in Azure Active Directory (Azure AD) tooview en start cloud-gebaseerde toepassingen of hello Azure AD-beheerder heeft deze toegang verleend tot. Een gebruiker met Azure AD-edities kunt ook gebruiken voor groepsbeheer met Self-service en beheermogelijkheden van de app via Hallo Toegangsvenster. Hallo Toegangspaneel is gescheiden van hello Azure-portal en vereist geen gebruikers toohave een Azure-abonnement.

In het deelvenster toegang toohello kunnen gebruikers zich aanmelden als ze een account voor werk of school in Azure AD hebben.

-   Gebruikers kunnen worden geverifieerd door Azure AD rechtstreeks.

-   Gebruikers kunnen worden geverifieerd met behulp van Active Directory Federation Services (AD FS).

-   Gebruikers kunnen worden geverifieerd door Windows Server Active Directory.

Als een gebruiker een abonnement voor Azure of Office 365 heeft en de hello Azure-portal of een Office 365-toepassing gebruikt, moet ze kunnen toouse Hallo Toegangsvenster naadloos opnieuw zonder toosign in. Gebruikers die niet worden geverifieerd worden na vragen aan gebruiker toosign in met behulp van Hallo gebruikersnaam en wachtwoord voor hun account in Azure AD. Als de organisatie Hallo heeft federation geconfigureerd, is te typen Hallo gebruikersnaam voldoende.

## <a name="general-issues-toocheck-first"></a>Algemene problemen toocheck eerst 

-   Zorg ervoor dat het Hallo-gebruiker zich aanmeldt toohello **Corrigeer URL**: <https://myapps.microsoft.com>

-   Zorg ervoor dat de browser van de gebruiker Hallo Hallo URL tooits is toegevoegd **vertrouwde sites**

-   Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen.

-   Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**

-   Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.**

-   Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert.

-   Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen.

-   Zorg ervoor dat tooalso probeer wissen van cookies in uw browser opnieuw te proberen toosign in.

## <a name="meeting-browser-requirements-for-hello-access-panel"></a>Vergadering Browservereisten voor Hallo Toegangsvenster

Hallo Toegangsvenster vereist een browser die JavaScript ondersteunt en CSS is ingeschakeld. toouse op basis van wachtwoorden eenmalige aanmelding (SSO) in Hallo paneel voor Apptoegang, Hallo Toegangsvenster extensie moet zijn geïnstalleerd in de browser van Hallo gebruiker. Deze extensie wordt automatisch gedownload wanneer een gebruiker selecteert een toepassing die is geconfigureerd voor eenmalige aanmelding op basis van wachtwoorden.

Voor eenmalige aanmelding op basis van wachtwoorden kunnen browsers Hallo van de eindgebruiker zijn:

-   Internet Explorer 8, 9, 10, 11--op Windows 7 of hoger

-   Rand verjaardagseditie van Windows 10 of hoger 

-   Chrome--Op Windows 7 of hoger, en op Mac OS X of hoger

-   Firefox 26,0 of later--op Windows XP SP2 of hoger, en op Mac OS X 10,6 of hoger


## <a name="problems-with-hello-users-account"></a>Problemen met Hallo gebruikersaccount

Toegang tot toohello die toegangspaneel vanwege een probleem met Hallo gebruikersaccount tooa kunnen worden geblokkeerd. Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met gebruikers en hun Accountinstellingen:

-   [Controleer of er een gebruikersaccount in Azure Active Directory bestaat](#check-if-a-user-account-exists-in-azure-active-directory)

-   [Controleer de status van de account van een gebruiker](#check-a-users-account-status)

-   [Een gebruiker-wachtwoord opnieuw instellen](#reset-a-users-password)

-   [Selfservice voor wachtwoordherstel inschakelen](#enable-self-service-password-reset)

-   [Controleer de status van een gebruiker multi-factor authentication-server](#check-a-users-multi-factor-authentication-status)

-   [Controleer de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info)

-   [Controleer de groepslidmaatschappen van een gebruiker](#check-a-users-group-memberships)

-   [Controleer de toegewezen licenties van een gebruiker](#check-a-users-assigned-licenses)

-   [Een gebruiker een licentie toewijzen](#assign-a-user-a-license)

### <a name="check-if-a-user-account-exists-in-azure-active-directory"></a>Controleer of er een gebruikersaccount in Azure Active Directory bestaat

toocheck als aanwezig is, is van een gebruikersaccount Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Controleer de eigenschappen Hallo van Hallo gebruiker object toobe zeker van te zijn dat ze zo uitzien als u verwacht en er worden geen gegevens ontbreekt.

### <a name="check-a-users-account-status"></a>Controleer de status van de account van een gebruiker

toocheck een gebruiker van account status, volgt u onderstaande Hallo stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **profiel**.

8.  Onder **instellingen** ervoor te zorgen dat **blok aanmelden** te is ingesteld,**Nee**.

### <a name="reset-a-users-password"></a>Een gebruiker-wachtwoord opnieuw instellen

tooreset het gebruikerswachtwoord Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op Hallo **wachtwoord opnieuw instellen** knop bovenaan Hallo Hallo gebruiker blade.

8.  Klik op Hallo **wachtwoord opnieuw instellen** knop op Hallo **wachtwoord opnieuw instellen** blade die wordt weergegeven.

9.  Kopiëren Hallo **tijdelijk wachtwoord** of **een nieuw wachtwoord invoeren** voor Hallo-gebruiker.

10. Deze nieuwe gebruiker met wachtwoord toohello communiceren, kunnen ze vereist toochange dit wachtwoord tijdens de volgende aanmelden tooAzure Active Directory.

### <a name="enable-self-service-password-reset"></a>Selfservice voor wachtwoordherstel inschakelen

tooenable zelf uw wachtwoord opnieuw instellen, Hallo implementatie volgende stappen:

-   [Tooreset gebruikers hun wachtwoorden met Azure Active Directory inschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-their-azure-ad-passwords)

-   [Inschakelen van gebruikers tooreset of hun on-premises Active Directory wachtwoorden wijzigen](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started#enable-users-to-reset-or-change-their-ad-passwords)

### <a name="check-a-users-multi-factor-authentication-status"></a>Controleer de status van een gebruiker multi-factor authentication-server

toocheck een gebruiker de multi-factor authentication status, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  Klik op Hallo **multi-Factor Authentication** knop Hallo boven aan het Hallo-blade.

7.  Eenmaal Hallo **multi-factor Authentication-beheerportal** laadt, zorg ervoor dat u op Hallo **gebruikers** tabblad.

8.  Hallo-gebruiker in de lijst met gebruikers Hallo vinden door te zoeken, filteren of sorteren.

9.  Selecteer Hallo gebruiker uit Hallo lijst met gebruikers en **inschakelen**, **uitschakelen**, of **afdwingen** multi-factor authentication-server naar wens.

   >[!NOTE]
   >Als een gebruiker zich in een **afgedwongen** staat, kunt u ze te instellen**uitgeschakelde** tijdelijk toolet deze terug te zetten bij hun account. Wanneer ze terug in bent, kunt u wijzigen hun status te**ingeschakeld** opnieuw toorequire ze hun contactgegevens tijdens de volgende Meld u aan de toore registratie. U kunt ook u kunt stappen Hallo in Hallo [controleren van de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info) tooverify of instellen van deze gegevens voor deze.
   >
   >

### <a name="check-a-users-authentication-contact-info"></a>Controleer de contactgegevens van de verificatie van een gebruiker

verificatie van een gebruiker contactgegevens gebruikt voor multi-factor authentication, voorwaardelijke toegang, Identity Protection en het wachtwoord opnieuw instellen, toocheck Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **profiel**.

8.  Schuif naar beneden te**verificatie contactgegevens**.

9.  **Bekijk** Hallo gegevens geregistreerd voor Hallo gebruiker en de update zo nodig.

### <a name="check-a-users-group-memberships"></a>Controleer de groepslidmaatschappen van een gebruiker

toocheck een gebruiker van groepslidmaatschappen, volgt u onderstaande Hallo stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **groepen** toosee die Hallo gebruiker groepen lid van is.

### <a name="check-a-users-assigned-licenses"></a>Controleer de toegewezen licenties van een gebruiker

toocheck een gebruiker de toegewezen licenties, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.

### <a name="assign-a-user-a-license"></a>Een gebruiker een licentie toewijzen 

een gebruiker van de tooa licentie tooassign Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle gebruikers**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-gebruiker en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo gebruiker momenteel is toegewezen.

8.  Klik op Hallo **toewijzen** knop.

9.  Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.

10. **Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen. Klik op **Ok** wanneer dit is voltooid.

11. Klik op Hallo **toewijzen** knop tooassign deze licenties toothis-gebruiker.

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a>Als u deze stappen voor probleemoplossing Hallo probleem niet verhelpen

Open een ondersteuningsticket Hello volgende informatie, indien beschikbaar:

-   Correlatie fout-ID

-   UPN (e-mailadres van de gebruiker)

-   Tenant-id

-   Browsertype

-   Tijdzone en de tijd/tijdsbestek tijdens fout optreedt

-   Fiddler traceringen

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)
