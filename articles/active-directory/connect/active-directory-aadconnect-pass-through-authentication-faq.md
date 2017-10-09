---
title: 'Azure AD Connect: Pass through-verificatie - Veelgestelde vragen | Microsoft Docs'
description: Toofrequently van antwoorden op veelgestelde vragen over Azure Active Directory Pass-through-verificatie.
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
ms.date: 08/03/2017
ms.author: billmath
ms.openlocfilehash: 550e2599177682f8ea971a05485dd5ac12b9b072
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-pass-through-authentication-frequently-asked-questions"></a>Azure Active Directory Pass-through-verificatie: Veelgestelde vragen

In dit artikel adres we Veelgestelde vragen over Azure Active Directory (Azure AD) Pass through-verificatie. Terug naar de nieuwe inhoud blijven controleren.

>[!IMPORTANT]
>Hallo Pass through-verificatie-functie is momenteel in preview.

## <a name="which-of-hello-azure-ad-sign-in-methods---pass-through-authentication-password-hash-synchronization-and-active-directory-federation-services-ad-fs---should-i-choose"></a>Welke van hello Azure AD aanmeldingsmethoden - Pass through-verificatie, synchronisatie van wachtwoordhash en Active Directory Federation Services (AD FS) - moet ik kiezen?

Dit is afhankelijk van de organisatorische vereisten en uw on-premises omgeving. Raadpleeg dit artikel voor een [vergelijking van Azure AD-in manieren Hallo](active-directory-aadconnect-user-signin.md).

## <a name="is-pass-through-authentication-a-free-feature"></a>Pass through-verificatie een beschikbare functie is?

Pass through-verificatie is een gratis functie en u hoeft betaald edities van Azure AD-toouse deze. Deze blijft vrij wanneer Hallo functie algemeen beschikbaar is bereikt.

## <a name="is-pass-through-authentication-available-in-microsoft-cloud-germanyhttpwwwmicrosoftdecloud-deutschland-and-microsoft-azure-government-cloudhttpsazuremicrosoftcomfeaturesgov"></a>Pass through-verificatie beschikbaar is in [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) en [Microsoft Azure Government Cloud](https://azure.microsoft.com/features/gov/)?

Nee,-Pass through-verificatie is alleen beschikbaar in hello world wide exemplaar van Azure AD.

## <a name="does-conditional-accessactive-directory-conditional-accessmd-work-with-pass-through-authentication"></a>Biedt [voorwaardelijke toegang](../active-directory-conditional-access.md) werken met Pass through-verificatie?

Ja, worden alle mogelijkheden voor voorwaardelijke toegang, waaronder Azure multi-factor Authentication werkt met Pass through-verificatie.

## <a name="does-pass-through-authentication-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Ondersteunt Pass-through-verificatie 'Alternatieve ID' als Hallo username, in plaats van 'userPrincipalName'?

Ja. Pass through-verificatie ondersteunt `Alternate ID` zoals gebruikersnaam wanneer geconfigureerd in Azure AD Connect zoals Hallo [hier](active-directory-aadconnect-get-started-custom.md). Niet alle Office 365-toepassingen ondersteunen `Alternate ID`. Raadpleeg de documentatie toohello specifieke toepassing voor Hallo ondersteuningsverklaring.

## <a name="does-password-hash-synchronization-act-as-a-fallback-toopass-through-authentication"></a>Synchronisatie van wachtwoordhash fungeren als een alternatieve verificatie tooPass via?

Nee, synchronisatie van wachtwoordhash is niet algemeen tooPass via Terugvalverificatie. Het fungeert alleen als een opvang voor [scenario's voor Pass-through-verificatie biedt geen ondersteuning voor vandaag](active-directory-aadconnect-pass-through-authentication-current-limitations.md#unsupported-scenarios). tooavoid gebruiker, mislukte aanmeldingen, moet u Pass-through-verificatie voor configureren [hoge beschikbaarheid](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability).

## <a name="can-i-install-an-azure-ad-application-proxyactive-directory-application-proxy-get-startedmd-connector-on-hello-same-server-as-a-pass-through-authentication-agent"></a>Kan ik installeren een [Azure AD-toepassingsproxy](../active-directory-application-proxy-get-started.md) connector op Hallo dezelfde server als een Pass through-verificatie-Agent?

Ja, deze configuratie wordt ondersteund door hello rebranded versies van Hallo Pass through-verificatie-Agent (versies 1.5.193.0 of hoger).

## <a name="what-versions-of-azure-ad-connect-and-pass-through-authentication-agent-do-you-need"></a>Welke versies van Azure AD Connect en Pass through-verificatie-Agent moet u gebruiken?

U moet versie 1.1.486.0 of hoger voor Azure AD Connect en 1.5.58.0 of hoger voor Hallo Pass through-verificatie-Agent voor deze functie toowork. Alle software moet worden geïnstalleerd op servers met Windows Server 2012 R2 of hoger.

## <a name="what-happens-if-my-users-password-has-expired-and-they-try-toosign-in-using-pass-through-authentication"></a>Wat gebeurt er als mijn wachtwoord is verlopen en probeer het toosign bij het gebruik van Pass through-verificatie?

Als u hebt geconfigureerd [wachtwoord terugschrijven](../active-directory-passwords-update-your-own-password.md) voor een specifieke gebruiker, en als Hallo gebruiker zich aanmeldt met Pass through-verificatie, ze kunnen wijzigen of hun wachtwoord opnieuw instellen. Hallo wachtwoorden worden teruggeschreven tooon lokale Active Directory zoals verwacht.

Echter als wachtwoord terugschrijven is niet geconfigureerd voor een specifieke gebruiker of als hello gebruiker beschikt niet over een geldige Azure AD licentie is toegewezen, Hallo gebruikers hun wachtwoord in Hallo cloud kan niet worden bijgewerkt. Zelfs als hun wachtwoord is verlopen kunnen ze hun wachtwoord niet bijwerken. Hallo-gebruiker in plaats daarvan ziet dit bericht: ' uw organisatie is niet toegestaan tooupdate uw wachtwoord op deze site. Werk het volgens toohello methode aanbevolen door uw organisatie, of vraag uw beheerder als u hulp nodig hebt." Hallo-gebruiker of Hallo beheerder heeft tooreset hun wachtwoord in uw lokale Active Directory.

## <a name="how-does-pass-through-authentication-protect-you-against-brute-force-password-attacks"></a>Hoe biedt Pass through-verificatie u bescherming tegen beveiligingsaanvallen wachtwoord?

Lees [in dit artikel](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) voor meer informatie.

## <a name="what-do-pass-through-authentication-agents-communicate-over-ports-80-and-443"></a>Wat Pass through-verificatie Agents communiceren via poorten 80 en 443

- Hallo verificatie Agents maken HTTPS-aanvragen via poort 443 voor alle bewerkingen van de functie.
- Hallo verificatie Agents maken HTTP-aanvragen via poort 80 toodownload SSL certificaatintrekkingslijsten.

     >[!NOTE]
     >In recente updates verminderd we het aantal poorten die zijn vereist voor de functie Hallo Hallo. Als u oudere versies van Azure AD Connect of Hallo verificatie-Agent hebt, houd deze poorten ook geopend: 5671, 8080, 9090, 9091, 9350, 9352 en 10100 10120.

## <a name="can-hello-pass-through-authentication-agents-communicate-over-an-outbound-web-proxy-server"></a>Kan Hallo Pass through-verificatie Agents communiceren via een webproxyserver voor uitgaande?

Ja. Als WPAD (Web Proxy Auto-Discovery) is ingeschakeld in uw on-premises-omgeving, wordt verificatie Agents automatisch toolocate proberen en een webproxyserver gebruikt op Hallo-netwerk.

## <a name="can-i-install-two-or-more-pass-through-authentication-agents-on-hello-same-server"></a>Kan ik Installeer twee of meer Agents van Pass through-verificatie op dezelfde server Hallo?

Nee, kunt u alleen een Pass through-verificatie-Agent installeren op één server. Als u tooconfigure Pass through-verificatie voor hoge beschikbaarheid wilt, volg Hallo-instructies in dit [artikel](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) in plaats daarvan.

## <a name="i-already-use-active-directory-federation-services-ad-fs-for-azure-ad-sign-in-how-do-i-switch-it-toopass-through-authentication"></a>Ik gebruik al Active Directory Federation Services (AD FS) voor aanmelding bij Azure AD. Hoe schakel ik het tooPass-through-verificatie?

Als u AD FS hebt geconfigureerd als uw aanmeldingspagina-methode met behulp van hello Azure AD Connect-wizard, Hallo gebruiker aanmelden methode wijzigen tooPass-through-verificatie. Deze wijziging kunt Pass through-verificatie op Hallo-tenant en converteert _alle_ uw federatieve domeinen naar beheerde domeinen. Alle volgende aanmelden aanvragen in uw tenant worden afgehandeld door Pass through-verificatie. Op dit moment is is er geen ondersteunde manier in Azure AD Connect toouse een combinatie van AD FS en Pass through-verificatie in verschillende domeinen.

Als AD FS is geconfigureerd als Hallo aanmelden methode _buiten_ van hello Azure AD Connect-wizard, Hallo gebruiker aanmelden methode wijzigen tooPass-through-verificatie (vanaf Hallo 'Niet configureren' optie). Deze wijziging kunnen Pass through-verificatie op Hallo-tenant. Maar alle domeinen in uw federatieve toouse AD FS voor aanmelden blijven. Gebruik PowerShell toomanually converteren enkele of alle deze federatieve domeinen tooManaged domeinen. Na die aanvragen voor alle aanmelden op de beheerde domeinen (_alleen_) worden verwerkt door Pass through-verificatie.

>[!IMPORTANT]
>Pass through-verificatie kunnen niet worden verwerkt op aanmeldingspagina voor alleen in de cloud-Azure AD-gebruikers.

## <a name="can-i-use-pass-through-authentication-in-a-multi-forest-ad-environment"></a>Kan ik Pass through-verificatie gebruiken in een omgeving met meerdere forests AD?

Ja. Omgevingen met meerdere forests worden ondersteund als er forestvertrouwensrelaties tussen uw AD-forests en als naamachtervoegsels correct is geconfigureerd.

## <a name="do-pass-through-authentication-agents-provide-load-balancing-capability"></a>Beschikken over Pass through-verificatie Agents taakverdeling mogelijkheid?

Nee, installatie van meerdere Pass through-verificatie Agents garandeert [hoge beschikbaarheid](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability), maar niet-taakverdeling. Een of twee Hallo verificatie Agents uiteindelijk Hallo bulksgewijs Hallo aanmelden aanvragen verwerken.

Wachtwoord validatie aanvragen die verificatie-Agents moet toohandle Hallo zijn lightweight. Piek- en gemiddelde belasting voor de meeste klanten is daarom gemakkelijk afgehandeld door twee of drie verificatie Agents in totaal.

Het is raadzaam dat u verificatie Agents sluiten tooyour domeincontrollers tooimprove aanmelden latentie installeert.

## <a name="can-i-install-hello-first-pass-through-authentication-agent-on-a-server-other-than-hello-one-that-runs-azure-ad-connect"></a>Kan ik Hallo installeren eerste Pass through-verificatie-Agent op een andere server dan Hallo een met Azure AD Connect?

Nee, dit scenario is _niet_ ondersteund.

## <a name="how-many-pass-through-authentication-agents-should-i-install"></a>Hoeveel Pass through-verificatie-Agents moet ik installeren?

We raden aan dat:

- U kunt twee of drie verificatie-Agents installeren in totaal. Deze configuratie is voldoende voor de meeste klanten.
- U kunt verificatie-Agents op uw domeincontrollers (of als sluiten toothem mogelijk) tooimprove aanmelden latentie installeren.
- U ervoor zorgen dat servers (waarbij verificatie Agents zijn geïnstalleerd) toohello dezelfde AD-forest worden toegevoegd als Hallo gebruikers waarvan de wachtwoorden toobe gevalideerd moeten.

>[!NOTE]
>Er is een limiet van 12 verificatie Agents per tenant.

## <a name="how-can-i-disable-pass-through-authentication"></a>Hoe kan ik Pass through-verificatie uitschakelen?

Hello Azure AD Connect-wizard opnieuw uitvoeren en Hallo gebruiker aanmelden methode van Pass through-verificatie tooanother methode wijzigen. Deze wijziging Pass through-verificatie is uitgeschakeld op Hallo-tenant en Hallo verificatie-Agent van Hallo server verwijdert. U hebt toomanually Hallo verificatie Agents verwijderen van andere servers.

## <a name="what-happens-when-i-uninstall-a-pass-through-authentication-agent"></a>Wat gebeurt er wanneer ik een Pass through-verificatie-Agent verwijderen?

Verwijdert een Pass through-verificatie-Agent van een server zorgt ervoor dat het toostop accepteren van aanmeldingsaanvragen. Zorg ervoor dat u een andere Agent-verificatie uitgevoerd voordat u deze bewerking tooavoid gebruiker aanmelden op uw tenant op te splitsen.

## <a name="next-steps"></a>Volgende stappen
- [**Huidige beperkingen** ](active-directory-aadconnect-pass-through-authentication-current-limitations.md) -met deze functie is momenteel in preview. Informatie over welke scenario's worden ondersteund en welke niet.
- [**Snel starten** ](active-directory-aadconnect-pass-through-authentication-quick-start.md) - laten en Azure AD Pass-through-verificatie wordt uitgevoerd.
- [**Technische diepgaand** ](active-directory-aadconnect-pass-through-authentication-how-it-works.md) -begrijpen hoe deze functie werkt.
- [**Problemen met** ](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) -informatie over hoe tooresolve algemene problemen met een Hallo-functie.
- [**Azure AD naadloze eenmalige aanmelding** ](active-directory-aadconnect-sso.md) -meer informatie over deze aanvullende functie.
- [**UserVoice** ](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - voor de nieuwe functieaanvragen indienen.
