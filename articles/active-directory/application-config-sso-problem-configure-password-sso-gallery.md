---
title: aaaProblem wachtwoord eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren | Microsoft Docs
description: Hallo veelvoorkomende problemen mensen face begrijpen bij het configureren van wachtwoord eenmalige aanmelding voor toepassingen die al worden vermeld in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 78c37c52453c375bf7ccbca6df5c9008be4ce642
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-an-azure-ad-gallery-application"></a>Probleem wachtwoord eenmalige aanmelding voor een toepassing-galerie van Azure AD configureren

In dit artikel kunt u toounderstand Hallo veelvoorkomende problemen mensen face bij het configureren van **wachtwoord Single Sign-on** met een galerie van Azure AD-toepassing.

## <a name="credentials-are-filled-in-but-hello-extension-does-not-submit-them"></a>Referenties zijn ingevuld, maar het Hallo-extensie niet worden verzonden

Dit gebeurt meestal als de aanmelding in is gewijzigd door de leverancier van de toepassing hello pagina onlangs tooadd een veld, een onderliggende id we gebruikt Hallo toodetect de velden gebruikersnaam en wachtwoord wijzigen of te wijzigen hoe Hallo aanmelden werkt voor de toepassing optreden. Gelukkig in veel gevallen kunt Microsoft werken met toepassing leveranciers toorapidly los deze problemen.

Terwijl Microsoft technologieën tooautomatically detecteren heeft wanneer deze integraties verbreken, maar soms niet kunnen toofind zijn toofix tijd die deze problemen rechts opslag, of dat ze even duren. In geval van Hallo wanneer een van deze integraties niet correct werkt zou Bedankt voor als u een ondersteuningsaanvraag hebt geopend, zodat we deze zo snel mogelijk kunt oplossen.

In aanvulling toothis, **als u verbonden met de leverancier van deze toepassing bent,** **verzend onze manier** zodat we ermee kunt werken toonatively hun toepassingen integreren met Azure Active Directory. U kunt verzenden Hallo leverancier toohello [aanbieding van uw toepassing in Azure Active Directory-toepassingsgalerie hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ze gestart.

## <a name="credentials-are-filled-in-and-submitted-but-hello-page-indicates-hello-credentials-are-incorrect"></a>Referenties zijn ingevuld en worden verzonden, maar Hallo pagina geeft aan dat Hallo referenties onjuist zijn

tooresolve dit probleem eerste selectievakje Hallo na:

-   Hallo gebruiker eerst te proberen**toohello toepassing website direct aanmelden** met Hallo referenties voor deze opgeslagen.

  * Als het werkt, hebt u Hallo gebruiker, klikt u op Hallo **referenties bijwerken** knop op Hallo **toepassing tegel** in Hallo **Apps** sectie Hallo [toepassing Toegang tot Configuratiescherm](https://myapps.microsoft.com/) tooupdate ze toohello nieuwste bekend werken gebruikersnaam en wachtwoord.

   * Als u of een ander toegewezen Hallo beheerdersreferenties op voor deze gebruiker vinden Hallo gebruiker of de toewijzing van de groep van toepassingen door te navigeren toohello **gebruikers en groepen** tabblad van de toepassing hello, Hallo toewijzing selecteren en te klikken op Hallo **updatereferenties** knop.

-   Als gebruiker Hallo hun eigen referenties toegewezen, hebben gebruikers van de Hallo **Controleer zeker van te zijn dat hun wachtwoord is niet verlopen in de toepassing hello toobe** en zo ja, **hun verlopen wachtwoord bijwerken** door toohello aanmelden rechtstreeks toepassing.

   * Nadat het Hallo-wachtwoord is bijgewerkt in de toepassing hello, aanvragen Hallo gebruiker tooclick hello **referenties bijwerken** knop op Hallo **toepassing tegel** in Hallo **Apps** sectie van Hallo [toepassing Toegangspaneel](https://myapps.microsoft.com/) tooupdate ze toohello nieuwste bekend werken gebruikersnaam en wachtwoord.

   * Als u of een ander toegewezen Hallo beheerdersreferenties op voor deze gebruiker vinden Hallo gebruiker of de toewijzing van de groep van toepassingen door te navigeren toohello **gebruikers en groepen** tabblad van de toepassing hello, Hallo toewijzing selecteren en te klikken op Hallo **updatereferenties** knop.

-   Hallo gebruiker update Hallo toegang Configuratiescherm Browseruitbreiding hebt met Hallo stappen hieronder in Hallo [hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo](#how-to-install-the-access-panel-browser-extension) sectie.

-   Zorg ervoor dat de Browseruitbreiding van Hallo toegang Configuratiescherm uitgevoerd en zijn ingeschakeld in de browser van de gebruiker.

-   Zorg ervoor dat uw gebruikers niet probeert toosign in toohello toepassing hello Toegangsvenster tijdens in **modus incognito, InPrivate- of persoonlijke**. Hallo-uitbreiding voor toegang tot Configuratiescherm wordt niet ondersteund in deze modi.

Als dit niet werkt, is het mogelijk Hallo-aanvraag die een wijziging is opgetreden op Hallo toepassing zijde die van toepassing hello integratie met Azure AD heeft tijdelijk worden verbroken. Bijvoorbeeld: dit kan gebeuren wanneer de leverancier van de toepassing hello introduceert een script op de pagina die anders voor handmatige tegenover werkt geautomatiseerde invoer, waardoor automatische integratie, zoals ons eigen, toobreak. Gelukkig in veel gevallen kunt Microsoft werken met toepassing leveranciers toorapidly los deze problemen.

Terwijl Microsoft technologieën tooautomatically detecteren heeft wanneer deze integraties verbreken, maar soms niet kunnen toofind zijn toofix tijd die deze problemen rechts opslag, of dat ze even duren. In geval van Hallo wanneer een van deze integraties niet correct werkt zou Bedankt voor als u een ondersteuningsaanvraag hebt geopend, zodat we deze zo snel mogelijk kunt oplossen.

In aanvulling toothis, **als u verbonden met de leverancier van deze toepassing bent,** **verzend onze manier** zodat we ermee kunt werken toonatively hun toepassingen integreren met Azure Active Directory. U kunt verzenden Hallo leverancier toohello [aanbieding van uw toepassing in Azure Active Directory-toepassingsgalerie hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ze gestart.

## <a name="hello-extension-works-in-chrome-and-firefox-but-not-in-internet-explorer"></a>Hallo-extensie werkt in Chrome en Firefox, maar niet in Internet Explorer

Er zijn twee mogelijke oorzaken toothis probleem:

-   Afhankelijk van de beveiligingsinstellingen Hallo ingeschakeld in Internet Explorer als Hallo-website niet is deel uit van een **Zone met vertrouwde**, soms in het script wordt uitgevoerd voor de toepassing hello worden geblokkeerd.

  *  tooresolve dit Hallo gebruiker te instrueren**van de toepassing hello website toevoegen** toohello **vertrouwde websites** lijst binnen hun **instellingen van Internet Explorer**. U kunt uw gebruikers toohello verzenden [lijst hoe tooadd een site toomy vertrouwde sites](https://answers.microsoft.com/en-us/ie/forum/ie9-windows_7/how-do-i-add-a-site-to-my-trusted-sites-list/98cc77c8-b364-e011-8dfc-68b599b31bf5) artikel voor gedetailleerde instructies.

-   In zeldzame gevallen veroorzaken validatie van de beveiliging van Internet Explorer soms Hallo pagina tooload langzamer dan Hallo uitvoering van onze script.

   * Deze situatie kan helaas verschillen, afhankelijk van Hallo browserversie, Computersnelheid of site bezocht. In dit geval is het raadzaam dat u contact op met ondersteuning zodat we Hallo-integratie voor deze specifieke toepassing kunt oplossen.

In aanvulling toothis, **als u verbonden met de leverancier van deze toepassing bent,** **verzend onze manier** zodat we ermee kunt werken toonatively hun toepassingen integreren met Azure Active Directory. U kunt verzenden Hallo leverancier toohello [aanbieding van uw toepassing in Azure Active Directory-toepassingsgalerie hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ze gestart.

## <a name="check-if-hello-applications-login-page-has-changed-recently-or-requires-an-additional-field"></a>Controleer of hello aanmeldingspagina van de toepassing onlangs is gewijzigd of een extra veld is vereist

Als de aanmeldingspagina van de toepassing hello drastisch is gewijzigd, hierdoor soms onze toobreak integraties. Een voorbeeld hiervan is wanneer de leverancier van een toepassing een teken in het veld, een captcha toevoegt of multi-factorauthenticatie tootheir optreedt. Gelukkig in veel gevallen kunt Microsoft werken met toepassing leveranciers toorapidly los deze problemen.

Terwijl Microsoft technologieën tooautomatically detecteren wanneer deze integraties verbreken, maar soms niet kunnen toofind zijn heeft verstrekt deze meteen. Anders duren ze sommige toofix tijd. In geval van Hallo wanneer een van deze integraties niet correct werkt zou Bedankt voor het openen van een ondersteuningsaanvraag zodat we deze zo snel mogelijk kunt oplossen.

In aanvulling toothis, **als u verbonden met de leverancier van deze toepassing bent,** **verzend onze manier** zodat we ermee kunt werken toonatively hun toepassingen integreren met Azure Active Directory. U kunt verzenden Hallo leverancier toohello [aanbieding van uw toepassing in Azure Active Directory-toepassingsgalerie hello](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing) tooget ze gestart.

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

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)

