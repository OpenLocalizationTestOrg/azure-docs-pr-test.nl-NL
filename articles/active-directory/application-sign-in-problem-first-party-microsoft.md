---
title: aaaProblems aanmelden tooa Microsoft-toepassing | Microsoft Docs
description: Algemene problemen geconfronteerd tijdens het aanmelden toofirst derden Microsoft Applications using Azure AD (zoals Office 365)
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
ms.openlocfilehash: 35849ca8dbaa909d17b6d0da572f5c11041a8559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="problems-signing-in-tooa-microsoft-application"></a>Problemen met aanmelden tooa Microsoft-toepassing

Microsoft Applications (zoals Office 365 Exchange, SharePoint, Yammer, enzovoort) worden toegewezen en beheerd iets anders dan 3e SaaS-toepassingen van derden of andere toepassingen die u integreert met Azure AD voor eenmalige aanmelding op.

Er zijn drie manieren die een gebruiker toegang tot tooa Microsoft gepubliceerde toepassing krijgt.

-   Voor toepassingen in Hallo Office 365 of andere betaald suites gebruikers krijgen toegang via **licentie toewijzing** ofwel rechtstreeks tootheir-gebruikersaccount, of door een groep met onze toewijzing op basis van een groep licentie mogelijkheid.

-   Voor toepassingen die Microsoft of een derde partij vrijelijk voor iedereen toouse publiceert gebruikers mogelijk toegang worden verleend via **toestemming van de gebruiker**. This0 betekent dat ze zich in de toepassing toohello met hun Azure AD werk of School-account en toohave toegang toosome beperkte set van gegevens op hun account toestaan.

-   Voor toepassingen die Microsoft of een 3rd Party vrijelijk voor iedereen toouse publiceert gebruikers kunnen ook toegang worden verleend via **beheerder toestemming**. Dit betekent dat een beheerder heeft vastgesteld Hallo toepassing kan worden gebruikt door iedereen in de organisatie hello, zodat ze zich in de toepassing toohello met een globale beheerdersaccount en tooeveryone in Hallo organisatie toegang verlenen.

tootroubleshoot uw probleem, beginnen met Hallo [algemene probleemgebieden met toegang tot toepassingen tooconsider](#general-problem-areas-with-application-access-to-consider) en leest u Hallo [Walkthrough: stappen tootroubleshoot Microsoft Application toegang](#walkthrough-steps-to-troubleshoot-microsoft-application-access) tooget in Hallo details.

## <a name="general-problem-areas-with-application-access-tooconsider"></a>Algemene probleemgebieden met toegang tot toepassingen tooconsider

Hieronder volgt een lijst van Hallo algemene probleemgebieden die u inzoomen kunt in als u al weet waar toostart, maar we raden u Hallo scenario tooget gaan snel lezen: [Walkthrough: stappen tootroubleshoot Microsoft Application toegang](#walkthrough-steps-to-troubleshoot-microsoft-application-access).

-   [Problemen met Hallo gebruikersaccount](#problems-with-the-users-account)

-   [Problemen met groepen](#problems-with-groups)

-   [Problemen met het beleid voor voorwaardelijke toegang](#problems-with-conditional-access-policies)

-   [Problemen met toestemming van de toepassing](#problems-with-application-consent)

## <a name="steps-tootroubleshoot-microsoft-application-access"></a>Stappen tootroubleshoot Microsoft Application toegang

Hieronder worden enkele veelvoorkomende problemen met mensen uitgevoerd in wanneer gebruikers zich niet tooa Microsoft-toepassing aanmelden.

-   Algemene problemen toocheck eerst

  * Zorg ervoor dat het Hallo-gebruiker zich aanmeldt toohello **Corrigeer URL** en niet de URL van een lokale toepassing.

  * Zorg ervoor dat het account van de gebruiker Hallo **niet is vergrendeld.**

  * Zorg ervoor dat Hallo **gebruikersaccount bestaat** in Azure Active Directory. [Controleer of er een gebruikersaccount in Azure Active Directory bestaat](#problems-with-the-users-account)

  * Zorg ervoor dat het account van de gebruiker Hallo **ingeschakeld** voor aanmeldingen. [Controleer de status van de account van een gebruiker](#problems-with-the-users-account)

  * Zorg ervoor dat Hallo-gebruiker **wachtwoord niet is verlopen of is vergeten.** [Opnieuw instellen van het wachtwoord van een gebruiker](#reset-a-users-password) of [selfservice voor wachtwoordherstel inschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-getting-started)

   * Zorg ervoor dat **multi-Factor Authentication** gebruikerstoegang niet blokkeert. [Controleer de status van een gebruiker multi-factor authentication-server](#check-a-users-multi-factor-authentication-status) of [contactgegevens van de verificatie van de gebruiker controleren](#check-a-users-authentication-contact-info)

   * Zorg ervoor dat een **beleid voor voorwaardelijke toegang** of **Identity Protection** beleid voor de gebruikerstoegang niet blokkeert. [Controleren van een specifieke voorwaardelijk toegangsbeleid](#problems-with-conditional-access-policies) of [beleid voor voorwaardelijke toegang van een specifieke toepassing controleren](#check-a-specific-applications-conditional-access-policy) of [beleid voor specifieke voorwaardelijke toegang uitschakelen](#disable-a-specific-conditional-access-policy)

   * Zorg ervoor dat een gebruiker **verificatie contactgegevens** is toodate tooallow multi-factor Authentication of voorwaardelijk beleid toobe afgedwongen. [Controleer de status van een gebruiker multi-factor authentication-server](#check-a-users-multi-factor-authentication-status) of [contactgegevens van de verificatie van de gebruiker controleren](#check-a-users-authentication-contact-info)

-   Voor **Microsoft** **toepassingen waarvoor een licentie** (zoals Office365) worden hier zijn enkele specifieke problemen toocheck zodra u algemene problemen Hallo hierboven hebt uitgesloten:

   * Zorg ervoor dat de gebruiker Hallo of heeft een **licentie is toegewezen.** [Controleer de toegewezen licenties van een gebruiker](#check-a-users-assigned-licenses) of [controleren van de groep toegewezen licenties](#check-a-groups-assigned-licenses)

   * Als het Hallo-licentie is **toegewezen tooa** **statische groep**, zorg ervoor dat Hallo **gebruiker lid is** van die groep. [Controleer de groepslidmaatschappen van een gebruiker](#check-a-users-group-memberships)

   * Als het Hallo-licentie is **toegewezen tooa** **dynamische groep**, zorg ervoor dat Hallo **dynamische groepsregel correct is ingesteld**. [Controleer de criteria voor lidmaatschap van een dynamische groep](#check-a-dynamic-groups-membership-criteria)

   * Als het Hallo-licentie is **toegewezen tooa** **dynamische groep**, ervoor zorgen dat dynamische groep Hallo heeft **verwerkt** lidmaatschap en die Hallo **gebruiker is een lid** (dit kan enige tijd duren). [Controleer de groepslidmaatschappen van een gebruiker](#check-a-users-group-memberships)

   *  Nadat u ervoor te zorgen Hallo-licentie is toegewezen, zorg ervoor dat Hallo-licentie is **niet verlopen**.

   *  Zorg ervoor dat het Hallo-licentie is **voor de toepassing hello** ze toegang hebben tot.

-   Voor **Microsoft** **toepassingen waarvoor een licentie niet**, hier zijn enkele andere dingen toocheck:

   * Als de toepassing hello aanvraagt **op gebruikersniveau machtigingen** (bijvoorbeeld ' toegang tot deze gebruiker Postvak'), zorg ervoor dat deze gebruiker Hallo toohello toepassing heeft aangemeld en heeft uitgevoerd een **op gebruikersniveau toestemming bewerking**  toolet Hallo toepassing toegang tot haar gegevens.

   * Als de toepassing hello aanvraagt **administratormachtigingen** (bijvoorbeeld ' toegang tot postvakken van alle gebruikers'), zorg ervoor dat een globale beheerder is uitgevoerd. een **bewerking op beheerdersniveau toestemming andere gebruikers van alle gebruikers** in Hallo-organisatie.

## <a name="problems-with-hello-users-account"></a>Problemen met Hallo gebruikersaccount

Toegang tot de toepassing kan vanwege een probleem met een gebruiker die is toegewezen toohello toepassing tooa worden geblokkeerd. Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met gebruikers en hun Accountinstellingen:

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

  * **Opmerking**: als een gebruiker zich in een **afgedwongen** staat, kunt u ze te instellen**uitgeschakelde** tijdelijk toolet deze terug te zetten bij hun account. Wanneer ze terug in bent, kunt u wijzigen hun status te**ingeschakeld** opnieuw toorequire ze hun contactgegevens tijdens de volgende Meld u aan de toore registratie. U kunt ook u kunt stappen Hallo in Hallo [controleren van de contactgegevens van de verificatie van een gebruiker](#check-a-users-authentication-contact-info) tooverify of instellen van deze gegevens voor deze.

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

## <a name="problems-with-groups"></a>Problemen met groepen

Toegang tot toepassingen kan worden geblokkeerd vanwege tooa probleem met een groep die is toegewezen toohello toepassing. Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met groepen en groepslidmaatschappen:

-   [Controleer het lidmaatschap van een groep](#check-a-groups-membership)

-   [Controleer de criteria voor lidmaatschap van een dynamische groep](#check-a-dynamic-groups-membership-criteria)

-   [Controleer de toegewezen licenties van een groep](#check-a-groups-assigned-licenses)

-   [Opnieuw verwerken van een groep licenties](#reprocess-a-groups-licenses)

-   [Een licentie toewijzen aan een groep](#assign-a-group-a-license)

### <a name="check-a-groups-membership"></a>Controleer het lidmaatschap van een groep

toocheck een groepslidmaatschap, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **leden** tooreview Hallo lijst met gebruikers toothis groep toegewezen.

### <a name="check-a-dynamic-groups-membership-criteria"></a>Controleer de criteria voor lidmaatschap van een dynamische groep 

toocheck criteria voor het lidmaatschap van een dynamische groep Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **dynamisch lidmaatschapsregels.**

8.  Bekijk Hallo **eenvoudige** of **geavanceerde** regel gedefinieerd voor de groep en zorg ervoor dat die u wilt dat een lid van deze groep toobe Hallo-gebruiker aan deze criteria voldoet.

### <a name="check-a-groups-assigned-licenses"></a>Controleer de toegewezen licenties van een groep

toocheck een groep van toegewezen licenties, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.

### <a name="reprocess-a-groups-licenses"></a>Opnieuw verwerken van een groep licenties

tooreprocess een groep van toegewezen licenties, Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.

8.  Klik op Hallo **opnieuw verwerken** knop tooensure die leden van de licenties die zijn toegewezen toothis beveiligingsgroep Hallo actueel zijn. Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.

   >[!NOTE]
   >toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen. [Een gebruiker een licentie toewijzen](#problems-with-application-consent).
   >
   >

### <a name="assign-a-group-a-license"></a>Een licentie toewijzen aan een groep

een licentiegroep tooa tooassign Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **alle groepen**.

6.  **Search** voor u geïnteresseerd in het bent Hallo-groep en **klikt u op Hallo rij** tooselect.

7.  Klik op **licenties** toosee welke licenties Hallo groep momenteel is toegewezen.

8.  Klik op Hallo **toewijzen** knop.

9.  Selecteer **een of meer producten** uit de lijst met beschikbare producten Hallo.

10. **Optionele** klikt u op Hallo **toewijzingsopties** item toogranularly producten toewijzen. Klik op **Ok** wanneer dit is voltooid.

11. Klik op Hallo **toewijzen** knop tooassign deze groep toothis-licenties. Dit kan lang duren, afhankelijk van Hallo omvang en complexiteit van Hallo-groep.

   >[!NOTE]
   >toodo dit snellere en overweeg tijdelijk een licentie toohello gebruiker rechtstreeks toewijzen. [Een gebruiker een licentie toewijzen](#problems-with-application-consent).
   > 
   >

## <a name="problems-with-conditional-access-policies"></a>Problemen met het beleid voor voorwaardelijke toegang

### <a name="check-a-specific-conditional-access-policy"></a>Beleid voor voorwaardelijke toegang specifieke controleren

toocheck of om een voorwaardelijk toegangsbeleid te valideren:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.

5.  Klik op Hallo **voorwaardelijke toegang** navigatie-item.

6.  Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.

7.  Controleer of er zijn geen specifieke voorwaarden, toewijzingen of andere instellingen die gebruikerstoegang mogelijk blokkeert.

   >[!NOTE]
   >U kunt desgewenst tootemporarily uitschakelen op dit beleid tooensure deze geen invloed op aanmelding mediaprofielen toodo deze, Hallo set **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop .
   >
   >

### <a name="check-a-specific-applications-conditional-access-policy"></a>Beleid voor voorwaardelijke toegang van een specifieke toepassing controleren

toocheck of valideren van één toepassing momenteel geconfigureerde voorwaardelijk toegangsbeleid:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.

5.  Klik op **alle toepassingen**.

6.  Zoeken voor het Hallo-toepassing u geïnteresseerd bent in of Hallo gebruiker probeert toosign in tooby toepassing weergegeven naam of een toepassing-id.

     >[!NOTE]
     >Als het Hallo-toepassing die u zoekt niet wordt weergegeven, klikt u op Hallo **Filter** knop en het Hallo-bereik van Hallo lijst te vergroten**alle toepassingen**. Als u wilt dat toosee meer kolommen, klikt u op Hallo **kolommen** knop tooadd aanvullende informatie voor uw toepassingen.
     >
     >

7.  Klik op Hallo **voorwaardelijke toegang** navigatie-item.

8.  Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.

9.  Controleer of er zijn geen specifieke voorwaarden, toewijzingen of andere instellingen die gebruikerstoegang mogelijk blokkeert.

     >[!NOTE]
     >U kunt desgewenst tootemporarily uitschakelen op dit beleid tooensure deze geen invloed op aanmelding mediaprofielen toodo deze, Hallo set **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop .
     >
     >

### <a name="disable-a-specific-conditional-access-policy"></a>Beleid voor specifieke voorwaardelijke toegang uitschakelen

toocheck of om een voorwaardelijk toegangsbeleid te valideren:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** in het navigatiemenu Hallo.

5.  Klik op Hallo **voorwaardelijke toegang** navigatie-item.

6.  Klik op Hallo beleid dat u geïnteresseerd bent in het te bekijken.

7.  Hallo-beleid uitschakelen door Hallo instelling **beleid inschakelen** te schakelen**Nee** en klik op Hallo **opslaan** knop.

## <a name="problems-with-application-consent"></a>Problemen met toestemming van de toepassing

Toegang tot toepassingen kan worden geblokkeerd omdat Hallo juiste machtigingen toestemming bewerking nog niet heeft plaatsgevonden. Hieronder volgen enkele manieren waarop u deze kunt oplossen en oplossen van problemen met de toepassing toestemming:

-   [Een bewerking op gebruikersniveau toestemming uitvoeren](#perform-a-user-level-consent-operation)

-   [De bewerking beheerdersniveau toestemming voor elke toepassing uitvoeren](#perform-administrator-level-consent-operation-for-any-application)

-   [Beheerdersniveau toestemming uitvoeren voor een toepassing voor één tenant](#perform-administrator-level-consent-for-a-single-tenant-application)

-   [Beheerdersniveau toestemming voor een multitenant-toepassing uitvoeren](#perform-administrator-level-consent-for-a-multi-tenant-application)

### <a name="perform-a-user-level-consent-operation"></a>Een bewerking op gebruikersniveau toestemming uitvoeren

-   Voor een Open ID Connect-toepassing die machtigingen aanvragen, voert navigeren van de toepassing toohello scherm aanmelden een toepassing van de gebruiker toestemming niveau toohello voor Hallo aangemelde gebruiker.

-   Als u toodo dit programmatisch wenst, Zie [afzonderlijke gebruikers toestemming wordt gevraagd](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#requesting-individual-user-consent).

### <a name="perform-administrator-level-consent-operation-for-any-application"></a>De bewerking beheerdersniveau toestemming voor elke toepassing uitvoeren

-   Voor **alleen toepassingen die zijn ontwikkeld met Hallo V1 toepassingsmodel**, kunt u deze beheerder niveau toestemming toooccur forceren door toe te voegen '**? prompt = admin\_toestemming**' toohello einde van een aanmelding van de toepassing in een URL.

-   Voor **alle toepassingen die zijn ontwikkeld met Hallo V2 toepassingsmodel**, kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **Hallo machtigingen aanvragen bij een map beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-single-tenant-application"></a>Beheerdersniveau toestemming uitvoeren voor een toepassing voor één tenant

-   Voor **toepassingen voor één tenant** die aanvragen machtigingen (zoals die u ontwikkelt of in uw organisatie eigenaar), kunt u uitvoeren een **beheerniveau toestemming** bewerking namens alle gebruikers met aanmelden als globale beheerder en te klikken op Hallo **machtigingen verlenen** knop bovenaan Hallo Hallo **toepassingsregister -&gt; alle toepassingen -&gt; Selecteer een App - &gt; Required Permissions** blade.

-   Voor **alle toepassingen die zijn ontwikkeld met Hallo V1 of V2-toepassingsmodel**, kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **hello om machtigingen vragen bij een Directory-beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

### <a name="perform-administrator-level-consent-for-a-multi-tenant-application"></a>Beheerdersniveau toestemming voor een multitenant-toepassing uitvoeren

-   Voor **multitenant-toepassingen** dat machtigingen voor aanvragen (zoals een toepassing van een derde partij, of Microsoft, ontwikkelt), kunt u uitvoeren een **beheerniveau toestemming** bewerking. Meld u aan als een globale beheerder en te klikken op Hallo **machtigingen verlenen** knop onder Hallo **bedrijfstoepassingen -&gt; alle toepassingen -&gt; Selecteer een App -&gt; Machtigingen** blade (beschikbaar snel).

-   Ook kunt u deze toooccur beheerdersniveau toestemming afdwingen door de instructies Hallo onder Hallo **Hallo machtigingen aanvragen bij een directory-beheerder** sectie van [gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint).

## <a name="next-steps"></a>Volgende stappen
[Gebruik van het Hallo-beheerder toestemming eindpunt](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes#using-the-admin-consent-endpoint)

