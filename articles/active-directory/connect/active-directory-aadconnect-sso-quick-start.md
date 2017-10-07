---
title: 'Azure AD Connect: Naadloze eenmalige aanmelding - snel aan de slag | Microsoft Docs'
description: Dit artikel wordt beschreven hoe tooget gestart met Azure Active Directory naadloze eenmalige aanmelding.
services: active-directory
keywords: Wat is Azure AD Connect, installeer Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Azure Active Directory naadloze eenmalige aanmelding: snel starten

## <a name="how-toodeploy-seamless-sso"></a>Hoe toodeploy naadloze eenmalige aanmelding

Azure Active Directory naadloze eenmalige aanmelding (Azure AD naadloze SSO) gebruikers wanneer ze zijn in het bedrijfsnetwerk van hun bedrijfscomputers verbonden tooyour automatisch afgemeld. Dit biedt uw gebruikers eenvoudig toegang tooyour cloud-gebaseerde toepassingen zonder extra on-premises onderdelen.

>[!IMPORTANT]
>Hallo naadloze SSO-functie is momenteel in preview.

Wanneer u toofollow toodeploy naadloze eenmalige aanmelding, moet deze stappen:

## <a name="step-1-check-prerequisites"></a>Stap 1: Controle van vereisten

Zorg ervoor dat Hallo volgende vereisten wordt voldaan:

1. Instellen van uw Azure AD Connect-server: als u [Pass through-verificatie](active-directory-aadconnect-pass-through-authentication.md) als uw contactmethode aanmelden is geen verdere actie vereist. Als u [synchronisatie van wachtwoordhash](active-directory-aadconnectsync-implement-password-synchronization.md) als uw contactmethode aanmelden en als er een firewall tussen Azure AD Connect en Azure AD, zorg ervoor dat:
- U gebruikt versies 1.1.484.0 of hoger van Azure AD Connect.
- Azure AD Connect kan communiceren met `*.msappproxy.net` URL's en meer dan poort 443. Deze vereiste geldt alleen wanneer u Hallo-functie, niet voor de werkelijke gebruikersaanmeldingen inschakelt.
- Azure AD Connect kunt aanbrengen direct IP-verbindingen toohello [Azure datacentrum IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653). Deze vereiste geldt opnieuw, alleen wanneer u Hallo functie inschakelt.
2. U moet domeinbeheerder-referenties voor elk AD-forest dat u tooAzure AD synchroniseren (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat tooenable naadloze eenmalige aanmelding.

## <a name="step-2-enable-hello-feature"></a>Stap 2: Hallo-functie inschakelen

Naadloze eenmalige aanmelding kan worden ingeschakeld met [Azure AD Connect](active-directory-aadconnect.md).

Als u een nieuwe installatie van Azure AD Connect uitvoert, kiest u Hallo [aangepaste installatiepad](active-directory-aadconnect-get-started-custom.md). Controleer op Hallo ' gebruiker ' aanmeldingspagina, Hallo 'Inschakelen voor eenmalige aanmelding' optie.

![Azure AD Connect - gebruiker aanmelden](./media/active-directory-aadconnect-sso/sso8.png)

Als u al een installatie van Azure AD Connect, kiest u 'Gebruiker aanmelden pagina wijzigen' op Azure AD Connect en klik op 'Volgende'. Controleer vervolgens Hallo 'Inschakelen voor eenmalige aanmelding' optie.

![Azure AD Connect - wijziging gebruiker aanmelden](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Hallo wizard vervolgen, totdat u toohello 'Inschakelen voor eenmalige aanmelding' pagina. Referenties van de domeinbeheerder voor elk AD-forest dat u tooAzure AD gesynchroniseerd (met behulp van Azure AD Connect) en gebruikers voor wie u wilt dat tooenable naadloze eenmalige aanmelding. 

Naadloze eenmalige aanmelding is na voltooiing van de wizard hello wordt ingeschakeld op uw tenant.

>[!NOTE]
> Hallo domeinbeheerder-referenties niet zijn opgeslagen in Azure AD Connect of in Azure AD, maar alleen gebruikte tooenable Hallo functie zijn.

Volg deze instructies tooverify naadloze eenmalige aanmelding correct ingeschakeld:

1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met Hallo hoofdbeheerder referenties voor uw tenant.
2. Selecteer **Azure Active Directory** op de linkernavigatiebalk Hallo.
3. Selecteer **Azure AD Connect**.
4. Controleer of deze Hallo **naadloze eenmalige aanmelding** functie wordt weergegeven als **ingeschakeld**.

![Azure-portal - blade van Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Stap 3: Implementeer Hallo-functie

tooroll hello functie tooyour gebruikers, moet u tooadd twee Azure AD-URL's (https://autologon.microsoftazuread-sso.com en https://aadg.windows.net.nsatc.net) toousers de Intranet-beveiligingszone-instellingen via Groepsbeleid in Active Directory.

>[!NOTE]
> Hallo alleen werk voor Internet Explorer en Google Chrome instructies te volgen in Windows (indien deze reeks URL's van vertrouwde site met Internet Explorer deelt). Lees de volgende sectie Hallo voor instructies tooset Mozilla Firefox en Google Chrome op Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Waarom moet u gebruikers toomodify Intranet-beveiligingszone-instellingen?

Standaard berekend Hallo browser automatisch Hallo in de juiste zone (Internet of een Intranet) van een URL. Http://contoso/ is bijvoorbeeld toegewezen toohello intranetzone terwijl http://intranet.contoso.com/ toegewezen toohello internetzone (omdat het Hallo-URL bevat een periode). Browsers verzenden geen Kerberos-tickets tooa cloudeindpunt - zoals Hallo twee Azure AD-URL's -, tenzij de URL van de browser toohello intranetzone is expliciet zijn toegevoegd.

### <a name="detailed-steps"></a>Gedetailleerde stappen

1. Open het Hallo Group Policy Management-hulpprogramma.
2. Hallo Groepsbeleid die toegepaste toosome of alle gebruikers bewerken. In dit voorbeeld gebruiken we Hallo **standaarddomeinbeleid**.
3. Navigeer te**Configuration\Administrative Templates\Windows Explorer\Onderdeel Internet Control Panel\Security op de gebruikerspagina** en selecteer **tooZone lijst van zonetoewijzingen Site**.
![Eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso6.png)  
4. Hallo-beleid inschakelen en Voer Hallo waarden (Azure AD URL's waarin de Kerberos-tickets worden doorgestuurd) te volgen en gegevens (*1* intranetzone geeft) in het dialoogvenster Hallo.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Als u toodisallow sommige gebruikers met een naadloze eenmalige aanmelding - bijvoorbeeld, wilt als deze gebruikers op gedeelde kiosken aanmelden zich - stelt Hallo voorafgaand aan waarden te*4*. Deze actie hello Azure AD-URL's toohello beperkte Zone worden toegevoegd en alle Hallo tijd voor naadloze eenmalige aanmelding mislukt.

5. Klik op **OK** en **OK** opnieuw.

![Eenmalige aanmelding](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Browser-overwegingen

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox niet automatisch Kerberos-verificatie. Elke gebruiker heeft toomanually hello Azure AD-URL's tootheir Firefox instellingen met behulp van de volgende stappen uit Hallo toevoegen:
1. Firefox uitvoeren en voer `about:config` in de adresbalk Hallo. Meldingen die u ziet worden genegeerd.
2. Zoeken naar Hallo **network.negotiate-auth.trusted-URI's** voorkeur. Deze voorkeur geeft een lijst met vertrouwde sites van Firefox voor Kerberos-verificatie.
3. Met de rechtermuisknop en selecteer 'Wijzigen'.
4. Voer "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" in het Hallo-veld.
5. Klik op 'OK' en Hallo browser openen.

#### <a name="safari-on-mac-os"></a>Safari op Mac OS

Zorg ervoor dat Hallo-machine met Mac OS gekoppelde tooAD. Zie de instructies voor het toodo die [hier](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome op Mac OS

Raadpleeg te voor Google Chrome op Mac OS en andere niet-Windows-platforms,[in dit artikel](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) voor meer informatie over hoe toowhitelist hello Azure AD-URL's voor geïntegreerde verificatie.

Het gebruik van Active Directory-groepsbeleid van derden is extensies tooroll hello Azure AD-URL's tooFirefox en Google Chrome op Mac-gebruikers buiten het bereik van dit artikel.

#### <a name="known-limitations"></a>Bekende beperkingen

Naadloze eenmalige aanmelding werkt niet in de privémodus Browse Firefox en rand browsers. Deze ook werkt niet op Internet Explorer als Hallo browser wordt uitgevoerd in de modus voor uitgebreide beveiliging.

>[!IMPORTANT]
>We onlangs teruggedraaid ondersteuning voor rand tooinvestigate klanten gemelde problemen.

## <a name="step-4-test-hello-feature"></a>Stap 4: Hallo functie testen

tootest Hallo-functie voor een specifieke gebruiker controleren of _alle_ Hallo volgende voorwaarden wordt voldaan:
  - Hallo-gebruiker zich aanmeldt op een zakelijke apparaat.
  - Hallo-apparaat is eerder samengevoegde tooyour Active Directory (AD)-domein.
  - Hallo-apparaat heeft een directe verbinding tooyour domeincontroller (DC), op Hallo bekabelde of draadloze bedrijfsnetwerk of via een externe verbinding, zoals een VPN-verbinding.
  - U hebt [uitgerold Hallo functie](##step-3-roll-out-the-feature) toothis-gebruiker met behulp van Groepsbeleid.

tootest hello scenario waarbij Hallo gebruiker alleen Hallo gebruikersnaam, maar niet Hallo wachtwoord invoert:
- Meld u aan bij *https://myapps.microsoft.com/* in een nieuwe persoonlijke browsersessie.

tootest hello scenario waarbij Hallo gebruiker geen tooenter Hallo gebruikersnaam of het Hallo-wachtwoord: 
- Meld u aan bij *https://myapps.microsoft.com/contoso.onmicrosoft.com* in een nieuwe persoonlijke browsersessie. Vervang '*contoso*"met de naam van uw tenant.
- Of meld u aan bij *https://myapps.microsoft.com/contoso.com* in een nieuwe persoonlijke browsersessie. Vervang '*contoso.com*' met een geverifieerd domein (niet een federatieve domein) in uw tenant.

## <a name="step-5-roll-over-keys"></a>Stap 5: Sleutels rollover

Azure AD Connect maakt in stap 2 computeraccounts (voor Azure AD) in alle Hallo AD-forests waarop naadloze eenmalige aanmelding is ingeschakeld. Meer informatie over meer in detail [hier](active-directory-aadconnect-sso-how-it-works.md). Het wordt aanbevolen dat u vaak Hallo Kerberos-sleutels voor ontsleuteling van deze computeraccounts overschakelen voor betere beveiliging.

>[!IMPORTANT]
>U hoeft niet toodo deze stap _onmiddellijk_ nadat u Hallo-functie hebt ingeschakeld. Hallo Kerberos ontsleutelingssleutels bevatten overschakelen met ten minste elke 30 dagen.

## <a name="next-steps"></a>Volgende stappen

- [**Technische diepgaand** ](active-directory-aadconnect-sso-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-sso-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-sso.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
