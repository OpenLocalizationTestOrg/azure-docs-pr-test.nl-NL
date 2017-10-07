---
title: configureren van wachtwoord eenmalige aanmelding voor een toepassing niet galerie aaaProblem | Microsoft Docs
description: Hallo veelvoorkomende problemen mensen face begrijpen bij het configureren van wachtwoord eenmalige aanmelding voor aangepaste niet-galerie-toepassingen die niet worden weergegeven in hello Azure AD-Toepassingsgalerie
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
ms.openlocfilehash: 3aee0a4c525bb3da338da2da0882ec572cf0e5e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="problem-configuring-password-single-sign-on-for-a-non-gallery-application"></a>Probleem wachtwoord eenmalige aanmelding voor een toepassing niet galerie configureren

In dit artikel kunt u toounderstand Hallo veelvoorkomende problemen mensen face bij het configureren van **eenmalige aanmelding wachtwoord** met een niet-galerie-toepassing.

## <a name="how-toocapture-sign-in-fields-for-an-application"></a>Hoe toocapture aanmelden velden voor een toepassing

Aanmelden veld vastleggen wordt alleen ondersteund voor HTML-functionaliteit aanmeldingspagina's en is **niet ondersteund voor niet-standaard aanmeldingspagina's**, zoals toepassingen die gebruikmaken van Flash of andere technologieën, zonder HTML-functionaliteit.

Er zijn twee manieren waarop u kunt aanmelden velden voor uw aangepaste toepassingen vastleggen:

-   Veld voor automatische aanmelding vastleggen

-   Handmatige aanmelden veld vastleggen

**Veld voor automatische aanmelding vastleggen** werkt goed samen met de meeste ingeschakeld HTML aanmeldingspagina's, als ze gebruiken **bekende DIV-id's voor het Hallo-gebruikersnaam en wachtwoord invoeren** veld. Hallo manier die dit werkt, is door slijmen Hallo HTML op Hallo pagina toofind DIV-id's die aan bepaalde criteria voldoen en door vervolgens metagegevens voor deze toepassing op te slaan zodat we kunnen wachtwoorden tooit later opnieuw.

**Handmatige aanmelden veld vastleggen** kan worden gebruikt in case Hallo toepassing hello **leverancier komt niet label** Hallo invoer velden die worden gebruikt voor aanmelding. Handmatige aanmelden veld vastleggen kan ook worden gebruikt in geval van Hallo wanneer hello **leverancier renders meerdere velden** en kan niet worden automatisch gedetecteerd. Azure AD kunt gegevens opslaan voor als veel velden als op Hallo aanmeldingspagina, zolang u laat ons weten waar deze velden zijn op de pagina Hallo.

In het algemeen **als het veld voor automatische aanmelding vastleggen niet werkt, altijd het is raadzaam tijdens het Hallo handmatige optie.**

### <a name="how-tooautomatically-capture-sign-in-fields-for-an-application"></a>Hoe tooautomatically velden aanmelden voor een toepassing vastleggen

tooconfigure **op basis van wachtwoorden Single Sign-on** voor het gebruik van een toepassing **automatische aanmelding veld vastleggen**, volgt u onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Voer Hallo **aanmeldings-URL**. Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen. **Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar op Hallo-URL die u opgeeft**.

10. Klik op Hallo **opslaan** knop.

11. Nadat u dit doen we je automatisch scrape die URL voor een gebruikersnaam en wachtwoord invoervak en kunt u verzenden toouse Azure AD toosecurely wachtwoorden toothat toepassing hello toegang Configuratiescherm Browseruitbreiding gebruiken.

## <a name="how-toomanually-capture-sign-in-fields-for-an-application"></a>Hoe toomanually velden aanmelden voor een toepassing vastleggen

toomanually vastleggen aanmelden velden, moet u eerst Hallo toegang Configuratiescherm Browseruitbreiding geïnstalleerd hebben en **niet wordt uitgevoerd in de modus InPrivate-navigatie, incognito of private.** tooinstall hello Browseruitbreiding, volg de stappen Hallo in Hallo [hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo](#i-cannot-manually-detect-sign-in-fields-for-my-application) sectie.

tooconfigure **op basis van wachtwoorden Single Sign-on** voor het gebruik van een toepassing **handmatige aanmelden veld vastleggen**, volgt u onderstaande stappen voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer Hallo-toepassing die u wilt dat eenmalige aanmelding tooconfigure.

7.  Nadat de toepassing hello wordt geladen, klikt u op Hallo **eenmalige aanmelding** uit van de toepassing hello linkerkant navigatiemenu.

8.  Selecteer Hallo modus **op basis van wachtwoorden eenmalige aanmelding.**

9.  Voer Hallo **aanmeldings-URL**. Dit is Hallo URL waarin gebruikers hun gebruikersnaam en wachtwoord toosign in te typen. **Zorg ervoor dat Hallo aanmelden velden zijn zichtbaar op Hallo-URL die u opgeeft**.

10. Klik op Hallo **opslaan** knop.

11. Nadat u dit doen we je automatisch scrape die URL voor een gebruikersnaam en wachtwoord invoervak en kunt u verzenden toouse Azure AD toosecurely wachtwoorden toothat toepassing hello toegang Configuratiescherm Browseruitbreiding gebruiken. In geval Hallo dat dit niet lukt, kunt u **Hallo-in-modus toouse handmatige aanmelden veld vastleggen wijzigen** toostep 12 voort te zetten.

12. Klik op **configureren &lt;appname&gt; instellingen voor wachtwoord eenmalige aanmelding**.

13. Selecteer Hallo **aanmelden velden handmatig detecteren** configuratieoptie.

14. Klik op **OK**.

15. Klik op **Opslaan**.

16. Volg Hallo op het scherm instructies toouse Hallo Toegangsvenster.

## <a name="i-see-a-we-couldnt-find-any-sign-in-fields-at-that-url-error"></a>Er is een fout 'Niet vinden velden aanmelden op die URL'

U ziet deze fout wanneer automatische detectie van velden voor aanmelden is mislukt. Dit probleem, probeer handmatige aanmelden veld detectie door Hallo volgen de stappen in Hallo tooresolve [hoe de velden aanmelden voor een toepassing voor het vastleggen van toomanually](#how-to-manually-capture-sign-in-fields-for-an-application) sectie.

## <a name="i-see-an-unable-toosave-single-sign-on-configuration-error"></a>Er is een fout 'kan geen toosave Single Sign-on-configuratie'

In bepaalde zeldzame gevallen, kan één Hallo aanmelding configuratie bijwerken mislukken. tooresolve deze Hallo eenmalige aanmelding configuratie opslaan opnieuw probeert.

Als dit toofail consistent blijft, opent u een ondersteuningsaanvraag en Hallo informatie verzameld in Hallo [hoe toosee Hallo details van een portal melding](#i-cannot-manually-detect-sign-in-fields-for-my-application) en [hoe tooget helpen met het verzenden van meldingen details tooa ondersteuningstechnicus](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secties.

## <a name="i-cannot-manually-detect-sign-in-fields-for-my-application"></a>Ik kan geen aanmelding handmatig detecteren in velden voor de toepassing

Hallo-gedrag die u tegenkomen kunt wanneer handmatige detectie niet werkt onder andere:

-   Hallo handmatige vastleggen toowork komt, maar vastgelegd Hallo-velden zijn niet juist

-   Hallo rechts velden ophalen niet gemarkeerd bij het uitvoeren van Hallo vastleggen

-   Hallo vastleggen, ga ik de aanmeldingspagina van de toepassing toohello zoals verwacht, maar er gebeurt niets

-   Handmatige vastleggen toowork wordt weergegeven, maar SSO gebeurt niet wanneer mijn gebruikers toohello toepassing hello Toegangsvenster navigeren.

Controleer Hallo volgende als u een van deze problemen optreden:

-   Zorg ervoor dat u de meest recente versie Hallo van Hallo toegang Configuratiescherm Browseruitbreiding **geïnstalleerd** en **ingeschakeld** door Hallo stappen in Hallo [hoe tooinstall Hallo toegang Configuratiescherm Browser extensie](#how-to-install-the-access-panel-browser-extension) sectie.

-   Zorg ervoor dat u niet vastleggen Hallo probeert tijdens uw browser in **modus incognito, InPrivate- of persoonlijke**. Hallo-uitbreiding voor toegang tot Configuratiescherm wordt niet ondersteund in deze modi.

-   Zorg ervoor dat uw gebruikers niet probeert toosign in toohello toepassing hello Toegangsvenster tijdens in **modus incognito, InPrivate- of persoonlijke**. Hallo-uitbreiding voor toegang tot Configuratiescherm wordt niet ondersteund in deze modi.

-   Probeer het opnieuw Hallo handmatige vastleggen, gezorgd Hallo rode markeringen is via de juiste velden Hallo.

-   Als Hallo handmatige vastleggen lijken toohang of niet van toepassing zijn op de aanmeldingspagina Hallo Alles (geval 3 hierboven), Hallo handmatige vastleggen opnieuw proberen. Maar deze tijd na het voltooien van Hallo proces, drukt u op Hallo **F12** knop tooopen van uw browser developer-console. Hallo eenmaal daar open **console** en het type **window.location= '&lt;Hallo aanmelding invoeren in een url die u hebt opgegeven bij het configureren van de app Hallo&gt;'** en druk vervolgens op  **Voer**. Deze kracht een pagina omleiden die eindigen Hallo vastleggen en opslaan van Hallo velden die zijn vastgelegd.

Als geen van deze benaderingen werkt, kunnen we helpen. Een ondersteuningsaanvraag openen met details van wat u hebt geprobeerd, evenals Hallo informatie verzameld in Hallo Hallo [hoe toosee Hallo details van een portal melding](#i-cannot-manually-detect-sign-in-fields-for-my-application) en [hoe tooget helpen met het verzenden van gegevens meldingen tooa-ondersteuning engineering](#how-to-get-help-by-sending-notification-details-to-a-support-engineer) secties (indien van toepassing).

## <a name="how-tooinstall-hello-access-panel-browser-extension"></a>Hoe tooinstall toegang Configuratiescherm Browseruitbreiding Hallo

tooinstall hello Configuratiescherm Browseruitbreiding toegang, Hallo volgende stappen:

1.  Open Hallo [Toegangspaneel](https://myapps.microsoft.com) in een van de Hallo ondersteunde browsers en meld u aan als een **gebruiker** in uw Azure AD.

2.  Klik op een **wachtwoord SSO toepassing** in Hallo Toegangsvenster.

3.  Selecteer in de Hallo vragen gevraagd tooinstall Hallo software, **nu installeren**.

4.  Op basis van uw browser zijn u gerichte toohello downloadkoppeling. **Voeg** Hallo extensie tooyour browser.

5.  Als uw browser wordt gevraagd, selecteert u tooeither **inschakelen** of **toestaan** Hallo extensie.

6.  Nadat deze is geïnstalleerd, **opnieuw** uw browsersessie.

7.  Aanmelden bij Hallo Toegangspaneel en zien als u kunt **starten** uw wachtwoord SSO-toepassingen.

U kunt ook Hallo-extensie voor Chrome en Firefox van Hallo rechtstreekse koppelingen hieronder downloaden:

-   [Uitbreiding van chrome toegang Configuratiescherm](https://chrome.google.com/webstore/detail/access-panel-extension/ggjhpefgjjfobnfoldnjipclpcfbgbhl)

-   [Uitbreiding van het Configuratiescherm Firefox toegang](https://addons.mozilla.org/firefox/addon/access-panel-extension/)

## <a name="how-toosee-hello-details-of-a-portal-notification"></a>Hoe toosee Hallo details van een melding van de portal

Hallo-details van de bedrijfsportal meldingen kunt u zien door Hallo onderstaande stappen te volgen:

1.  Klik op Hallo **meldingen** pictogram (Hallo bel) in de rechterbovenhoek Hallo Hallo Azure Portal

2.  Selecteer een melding in een **fout** status (die met de volgende toothem van een rood (!)).

  >! Houd er rekening mee] u kunt niet op meldingen in een **geslaagd** of **In uitvoering** status.
  >
  >

3.  Deze open Hallo **Meldingsdetails** blade.

4.  Gebruik deze informatie zelf toounderstand meer details over Hallo probleem.

5.  Als u nog hulp nodig hebt, kunt u deze informatie ook met een support engineer of Hallo groep tooget Help-informatie delen met uw probleem.

6.  Klik op Hallo **kopiëren** **pictogram** toohello rechts van Hallo **Kopieerfout** textbox toocopy alle Hallo melding details tooshare met een medewerker van de groep ondersteuning of product.

## <a name="how-tooget-help-by-sending-notification-details-tooa-support-engineer"></a>Hoe tooget helpen met het verzenden van meldingen details tooa ondersteuningstechnicus

Het is heel belangrijk dat u delen **alle details hieronder vermelde Hallo** met de ondersteuningstechnicus als u hulp nodig hebt zodat u ze kunt u snel. U kunt dit eenvoudig door doen **u een schermopname** of door te klikken op Hallo **foutpictogram kopiëren**, toohello rechts van Hallo gevonden **Kopieerfout** textbox.

## <a name="notification-details-explained"></a>Details van de melding uitgelegd

Hallo hieronder wordt uitgelegd meer wat elke Hallo melding items betekent en geven voorbeelden van elk van deze servers.

### <a name="essential-notification-items"></a>Melding van essentiële Items

-   **Titel** – Hallo beschrijvende titel Hallo-melding

    -   Voorbeeld: **Application proxy-instellingen**

-   **Beschrijving** : Beschrijving van wat is het gevolg van Hallo bewerking Hallo

    -   Voorbeeld: **interne url ingevoerd wordt al gebruikt door een andere toepassing**

-   **Id van de melding** – Hallo unieke id van Hallo-melding

    -   Voorbeeld: **clientNotification-2adbfc06-2073-4678-a69f-7eb78d96b068**

-   **Aanvraag-Id van client** – Hallo specifieke aanvraag-id gemaakt door uw browser

    -   Voorbeeld: **302fd775-3329-4670-a9f3-bea37004f0bc**

-   **Stempel UTC-tijd** – Hallo tijdstempel waarover Hallo melding is opgetreden, in UTC

    -   Voorbeeld: **2017-03-23T19:50:43.7583681Z**

-   **Interne transactie-Id** – Hallo interne ID we in ons systeem toolook Hallo fout kunnen gebruiken

    -   Voorbeeld: **71a2f329-ca29-402f-aa72-bc00a7aca603**

-   **UPN** – Hallo-gebruiker die Hallo is uitgevoerd

    -   Voorbeeld:**tperkins@f128.info**

-   **Tenant-Id** – Hallo unieke ID van Hallo tenant die gebruiker Hallo die Hallo bewerking uitgevoerd lid was van

    -   Voorbeeld: **7918d4b5-0442-4a97-be2d-36f9f9962ece**

-   **Gebruikersobject-Id** – Hallo unieke ID van het Hallo-gebruiker die Hallo is uitgevoerd

    -   Voorbeeld: **17f84be4-51f8-483a-b533-383791227a99**

### <a name="detailed-notification-items"></a>Gedetailleerde melding Items

-   **Weergavenaam** – **(kan niet leeg zijn)** een meer gedetailleerde weergavenaam voor Hallo-fout

    -   Voorbeeld * – **Application proxy-instellingen**

-   **Status** – specifieke status van melding Hallo Hallo

    -   Voorbeeld * – **is mislukt**

-   **Object-Id** – **(kan niet leeg zijn)** Hallo object-ID op basis van welke Hallo bewerking is uitgevoerd

    -   Voorbeeld: **8e08161d-f2fd-40ad-a34a-a9632d6bb599**

-   **Details** – Hallo gedetailleerde beschrijving van wat is het gevolg van Hallo-bewerking

    -   Voorbeeld: **interne url 'http://bing.com/' is ongeldig omdat het zich al in gebruik**

-   **Fout kopiëren** – klikt u op Hallo **pictogram kopiëren** toohello rechts van Hallo **Kopieerfout** textbox toocopy alle Hallo melding details tooshare met een medewerker van de groep ondersteuning of productupdates

    -   Voorbeeld:```{"errorCode":"InternalUrl\_Duplicate","localizedErrorDetails":{"errorDetail":"Internal url 'http://google.com/' is invalid since it is already in use"},"operationResults":\[{"objectId":null,"displayName":null,"status":0,"details":"Internal url 'http://bing.com/' is invalid since it is already in use"}\],"timeStampUtc":"2017-03-23T19:50:26.465743Z","clientRequestId":"302fd775-3329-4670-a9f3-bea37004f0bb","internalTransactionId":"ea5b5475-03b9-4f08-8e95-bbb11289ab65","upn":"tperkins@f128.info","tenantId":"7918d4b5-0442-4a97-be2d-36f9f9962ece","userObjectId":"17f84be4-51f8-483a-b533-383791227a99"}```

## <a name="next-steps"></a>Volgende stappen
[Bieden van eenmalige aanmelding tooyour apps met toepassingsproxy](active-directory-application-proxy-sso-using-kcd.md)

