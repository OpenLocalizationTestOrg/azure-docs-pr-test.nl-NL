---
title: Azure AD Pass-through-verificatie - snel aan de slag | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooget de slag met Azure Active Directory (Azure AD) Pass through-verificatie.
services: active-directory
keywords: Azure AD Connect Pass through-verificatie, install Active Directory onderdelen vereist voor Azure AD, SSO, Single Sign-on
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: billmath
ms.openlocfilehash: d6d0f85fe144cf36cc94676f6592d37988b20647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-quick-start"></a>Azure Active Directory Pass-through-verificatie: Snel starten

## <a name="how-toodeploy-azure-ad-pass-through-authentication"></a>Hoe toodeploy Azure AD Pass-through-verificatie

Azure Active Directory (Azure AD)-Pass through-verificatie kunnen uw gebruikers toosign op tooboth on-premises en cloudtoepassingen met dezelfde wachtwoorden Hallo. Deze zich gebruikers aanmeldt door het valideren van hun wachtwoorden rechtstreeks op uw lokale Active Directory.

>[!IMPORTANT]
>Azure AD Pass-through-verificatie is momenteel in preview. Als u deze functie via preview gebruikt hebt, moet u ervoor zorgen dat u de preview-versies van Hallo verificatie Agents upgraden met behulp van instructies Hallo [hier](./active-directory-aadconnect-pass-through-authentication-upgrade-preview-authentication-agents.md).

U moet deze instructies toodeploy Pass through-verificatie toofollow:

## <a name="step-1-check-prerequisites"></a>Stap 1: Controle van vereisten

Zorg ervoor dat Hallo volgende vereisten wordt voldaan:

### <a name="on-hello-azure-active-directory-admin-center"></a>Op Hallo Azure Active Directory-beheercentrum

1. Maak een account van de globale beheerder alleen in de cloud op uw Azure AD-tenant. Op deze manier kunt u de configuratie van uw tenant Hallo beheren moeten uw on-premises-services mislukt of niet meer beschikbaar. Meer informatie over [toevoegen van een cloudconfiguratie globale beheerdersaccount](../active-directory-users-create-azure-portal.md). Tijdens het doorzoeken van deze stap is kritieke tooensure dat u geen toegang af van uw tenant.
2. Voeg een of meer [aangepast domein namen](../active-directory-add-domain.md) tooyour Azure AD-tenant. Uw gebruikers zich aanmelden met een van deze domeinnamen.

### <a name="in-your-on-premises-environment"></a>In uw on-premises-omgeving

1. Identificeer een server met Windows Server 2012 R2 of later op welke toorun Azure AD Connect. Hallo server toohello dezelfde AD-forest toevoegen als Hallo gebruikers waarvan de wachtwoorden toobe gevalideerd moeten.
2. Hallo installeren [meest recente versie van Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) op Hallo server geïdentificeerd in de vorige stap. Als u al Azure AD Connect uitgevoerd, zorg ervoor dat versie Hallo 1.1.557.0 of hoger.
3. Identificeren van een extra server met Windows Server 2012 R2 of later op welke toorun een zelfstandige verificatie-Agent. Hallo verificatie-Agent-versie moet toobe 1.5.193.0 of hoger. Deze server is de benodigde tooensure hoge beschikbaarheid van aanmeldingsaanvragen. Hallo server toohello dezelfde AD-forest toevoegen als Hallo gebruikers waarvan de wachtwoorden toobe gevalideerd moeten.
4. Als er een firewall tussen uw servers en Azure AD, moet u tooconfigure Hallo volgende items:
   - Zorg ervoor dat de verificatie-Agents kunnen leveren **uitgaande** tooAzure AD-aanvragen via de volgende poorten Hallo:
   
   | Poortnummer | Hoe deze wordt gebruikt |
   | --- | --- |
   | **80** | Downloaden van certificaatintrekking (CRL's) worden tijdens het valideren van Hallo SSL-certificaat |
   | **443** | Alle uitgaande communicatie met onze service |
   
   Als uw firewall-regels op basis van gebruikers toooriginating afgedwongen, opent u deze poorten voor verkeer van de Windows-services die worden uitgevoerd als een netwerkservice.
   - Als uw firewall of proxyserver kunt DNS-whitelisting, geaccepteerde verbindingen te**\*. msappproxy.net** en  **\*. servicebus.windows.net**. Als dit niet het geval is, kunt u toegang te[Azure DataCenter IP ranges](https://www.microsoft.com/download/details.aspx?id=41653), die wekelijks worden bijgewerkt.
   - De verificatie-Agents moet toegang hebben te**login.windows.net** en **login.microsoftonline.com** voor initiële registratie, zodat uw firewall openen voor deze URL's ook.
   - Voor validatie van het servercertificaat deblokkeren Hallo volgende URL's: **mscrl.microsoft.com:80**, **crl.microsoft.com:80**, **ocsp.msocsp.com:80** en  **www.Microsoft.com:80**. Deze URL's worden gebruikt voor validatie van het servercertificaat met andere Microsoft-producten, dus u al deze URL's gedeblokkeerd hebt mogelijk.

## <a name="step-2-enable-exchange-activesync-support-optional"></a>Stap 2: (Optioneel) Exchange ActiveSync-ondersteuning inschakelen

Volg deze instructies tooenable Exchange ActiveSync-ondersteuning:

1. Gebruik [Exchange PowerShell](https://technet.microsoft.com/library/mt587043(v=exchg.150).aspx) toorun Hallo volgende opdracht:
```
Get-OrganizationConfig | fl per*
```

2. Controleer de waarde van de Hallo Hallo `PerTenantSwitchToESTSEnabled` instelling. Als de waarde Hallo **true**, uw tenant is juist geconfigureerd - doorgaans is dit Hallo-aanvraag voor de meeste klanten. Als de waarde Hallo **false**, voert hello volgende opdracht:
```
Set-OrganizationConfig -PerTenantSwitchToESTSEnabled:$true
```

3. Verifieer dat de waarde Hallo Hallo `PerTenantSwitchToESTSEnabled` nu ingesteld te**true**. Wacht een uur voordat bewegende toohello volgende stap.

Als u problemen mee te tijdens deze stap maken, controleert u onze [probleemoplossingsgids](active-directory-aadconnect-troubleshoot-pass-through-authentication.md#exchange-activesync-configuration-issues) voor meer informatie.

## <a name="step-3-enable-hello-feature"></a>Stap 3: Hallo-functie inschakelen

Pass through-verificatie kan worden ingeschakeld met [Azure AD Connect](active-directory-aadconnect.md).

>[!IMPORTANT]
>Pass through-verificatie kan worden ingeschakeld op Hallo Azure AD Connect primaire of staging-server. Het is raadzaam dat u het inschakelen van de primaire server Hallo.

Als u Azure AD Connect voor Hallo eerst installeert, kiest u Hallo [aangepaste installatiepad](active-directory-aadconnect-get-started-custom.md). Op Hallo **gebruikersaanmelding** pagina **Pass through-verificatie** zoals Hallo aanmelding op methode. Is gelukt, een Pass through-verificatie-agent is geïnstalleerd op Hallo dezelfde server als Azure AD Connect. Bovendien is Hallo Pass through-verificatie-functie ingeschakeld op uw tenant.

![Azure AD Connect - gebruiker aanmelden](./media/active-directory-aadconnect-sso/sso3.png)

Als u Azure AD Connect al hebt geïnstalleerd (met behulp van Hallo [snelle installatie](active-directory-aadconnect-get-started-express.md) of Hallo [aangepaste installatie](active-directory-aadconnect-get-started-custom.md) pad), selecteer **wijziging gebruiker aanmeldingspagina** op Azure AD Verbinding maken en klikt u op **volgende**. Selecteer vervolgens **Pass through-verificatie** zoals Hallo aanmelding op methode. Is gelukt, een Pass through-verificatie-agent is geïnstalleerd op Hallo dezelfde server als Azure AD Connect en Hallo-functie is ingeschakeld op uw tenant.

![Azure AD Connect - wijziging gebruiker aanmelden](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

>[!IMPORTANT]
>Pass through-verificatie is een functie op tenantniveau. Het inschakelen van invloed is op aanmeldingspagina voor gebruikers in _alle_ Hallo beheerde domeinen in uw tenant. Als u van de AD FS tooPass-through-verificatie overschakelt, wordt aangeraden dat u ten minste 12 uur voordat het afsluiten van uw AD FS-infrastructuur wacht - wachttijd is tooensure die gebruikers kunnen tijdens de overgang in tooExchange ActiveSync houden ondertekenen.

## <a name="step-4-test-hello-feature"></a>Stap 4: Hallo functie testen

Volg deze instructies tooverify Pass through-verificatie correct ingeschakeld:

1. Meld u aan toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met Hallo hoofdbeheerder referenties voor uw tenant.
2. Selecteer **Azure Active Directory** op de linkernavigatiebalk Hallo.
3. Selecteer **Azure AD Connect**.
4. Controleer of deze Hallo **Pass through-verificatie** functie wordt weergegeven als **ingeschakeld**.
5. Selecteer **Pass through-verificatie**. Deze blade worden Hallo servers weergegeven waarop de verificatie-Agents zijn geïnstalleerd.

![Azure Active Directory-beheercentrum - blade van Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory-beheercentrum - blade Pass through-verificatie](./media/active-directory-aadconnect-pass-through-authentication/pta8.png)

In deze fase, kunnen gebruikers van alle beheerde domeinen in uw tenant zich aanmelden bij het gebruik van Pass through-verificatie. Gebruikers van federatieve domeinen blijven echter toosign in met behulp van Active Directory Federation Services (AD FS) of een andere federatieprovider die u eerder hebt geconfigureerd. Als u een domein van de federatieve toomanaged omzet, start alle gebruikers van dat domein automatisch aanmelden met behulp van Pass through-verificatie. Hallo Pass through-verificatie-functie is niet van invloed op gebruikers alleen in de cloud.

## <a name="step-5-ensure-high-availability"></a>Stap 5: Hoge beschikbaarheid garanderen

Als u van plan toodeploy Pass through-verificatie in een productieomgeving bent, moet u een zelfstandige verificatie-Agent installeren. Deze tweede verificatie-Agent installeren op een server _andere_ dan één actief Azure AD Connect Hallo en Hallo eerste verificatie-Agent. Deze instelling biedt u hoge beschikbaarheid van aanmeldingsaanvragen. Volg deze instructies toodeploy zelfstandige verificatie-Agent:

1. **Download de nieuwste versie Hallo Hallo verificatie-Agent (versies 1.5.193.0 of hoger)**: aanmelden toohello [Azure Active Directory-beheercentrum](https://aad.portal.azure.com) met uw globale tenantbeheerderreferenties.
2. Selecteer **Azure Active Directory** op de linkernavigatiebalk Hallo.
3. Selecteer **Azure AD Connect** en vervolgens **Pass through-verificatie**. En selecteer **agent downloaden**.
4. Klik op Hallo **voorwaarden accepteren & downloaden** knop.
5. **Installeer de meest recente versie Hallo Hallo verificatie-Agent**: Voer Hallo uitvoerbare gedownload in de voorgaande stap Hallo. Geef uw tenant hoofdbeheerder referenties wanneer u wordt gevraagd.

![Azure Active Directory-beheercentrum - knop downloaden van de verificatie-Agent](./media/active-directory-aadconnect-pass-through-authentication/pta9.png)

![Azure Active Directory-beheercentrum - blade Agent downloaden](./media/active-directory-aadconnect-pass-through-authentication/pta10.png)

>[!NOTE]
>U kunt ook downloaden Hallo verificatie-Agent van [hier](https://aka.ms/getauthagent). Zorg ervoor dat u lees en accepteer van Hallo verificatie Agent [servicevoorwaarden](https://aka.ms/authagenteula) _voordat_ te installeren.

## <a name="next-steps"></a>Volgende stappen
- [**Huidige beperkingen** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -met deze functie is momenteel in preview. Informatie over welke scenario's worden ondersteund en welke niet.
- [**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Veelgestelde vragen** ](active-directory-aadconnect-pass-through-authentication-faq.md) -toofrequently vragen worden beantwoord.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
