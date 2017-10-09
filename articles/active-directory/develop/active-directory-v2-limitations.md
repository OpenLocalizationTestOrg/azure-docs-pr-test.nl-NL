---
title: Active Directory aaaAzure v2.0-eindpunt en beperkingen | Microsoft Docs
description: Een lijst met voorwaarden en beperkingen voor hello Azure AD v2.0-eindpunt.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: a99289c0-e6ce-410c-94f6-c279387b4f66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: bcbb7239f1d117002d16ac23dca8f1feb13a9161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="should-i-use-hello-v20-endpoint"></a>Moet ik Hallo v2.0-eindpunt gebruiken?
Wanneer u toepassingen die zijn geïntegreerd met Azure Active Directory maakt, moet u toodecide of Hallo v2.0-eindpunt en verificatieprotocollen aan uw behoeften voldoet. Oorspronkelijke Azure Active Directory-eindpunt wordt nog steeds volledig ondersteund en is in sommige opzichten meer uitgebreide functionaliteit dan versie 2.0. Hallo echter v2.0-eindpunt [introduceert aanzienlijke voordelen](active-directory-v2-compare.md) voor ontwikkelaars.

Hier volgt de vereenvoudigde aanbeveling voor ontwikkelaars op dit moment:

* Als u een persoonlijke Microsoft-accounts in uw toepassing ondersteunen moet, gebruikt u Hallo v2.0-eindpunt. Maar voordat u dit doet, moet u dat u begrijpt Hallo-beperkingen die in dit artikel besproken.
* Als uw toepassing alleen toosupport Microsoft werk- en schoolaccounts moet, hoeft u Hallo v2.0-eindpunt. In plaats daarvan verwijzen tooour [Ontwikkelaarshandleiding voor Azure AD](active-directory-developers-guide.md).

Na verloop van tijd meegroeit Hallo v2.0-eindpunt tooeliminate Hallo beperkingen die hier worden vermeld, zodat u alleen ooit toouse Hallo v2.0-eindpunt moet. In Hallo tussentijd dit artikel is bedoeld toohelp u bepalen of Hallo v2.0-eindpunt geschikt is voor u is. We blijven tooupdate in dit artikel tooreflect Hallo huidige status van Hallo v2.0-eindpunt. Controleer back tooreevaluate uw vereisten tegen v2.0-mogelijkheden.

Als er een bestaande Azure AD-app die Hallo v2.0-eindpunt niet wordt gebruikt, is er geen noodzaak toostart vanaf het begin. In toekomstige hello leveren we een manier voor toouse u uw bestaande Azure AD-toepassingen met Hallo v2.0-eindpunt.

## <a name="restrictions-on-app-types"></a>Beperkingen van app-typen
Op dit moment worden hello volgende typen apps niet ondersteund door Hallo v2.0-eindpunt. Zie voor een beschrijving van de ondersteunde app-typen [App-typen voor hello Azure Active Directory v2.0-eindpunt](active-directory-v2-flows.md).

### <a name="standalone-web-apis"></a>Zelfstandige Web-API 's
U kunt Hallo v2.0-eindpunt te gebruiken[bouwen van een Web-API die is beveiligd met OAuth 2.0](active-directory-v2-flows.md#web-apis). Deze Web-API kan echter tokens ontvangen van een toepassing die dezelfde id heeft Hallo alleen U geen toegang tot een Web-API van een client met een andere toepassing. Hallo-client niet kan toorequest worden en machtigingen tooyour Web-API te verkrijgen.

hoe een Web-API die tokens van een client met dezelfde toepassings-ID Hallo accepteert toobuild zien toosee Hallo v2.0-eindpunt Web API-voorbeelden in onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.

## <a name="restrictions-on-app-registrations"></a>Beperkingen van app-registraties
Op dit moment voor elke app die u toointegrate met Hallo v2.0-eindpunt wilt, moet u een app-registratie in Hallo nieuwe [Portal voor registratie van Microsoft-toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList). Bestaande Azure AD of apps voor Microsoft-account zijn niet compatibel met Hallo v2.0-eindpunt. Apps die zijn geregistreerd in een portal dan Hallo Portal voor registratie van toepassing zijn niet compatibel met Hallo v2.0-eindpunt. In toekomstige hello plant we tooprovide een toouse manier een bestaande toepassing als een v2.0-app. Op dit moment maar is er geen migratiepad voor een bestaande app toowork met Hallo v2.0-eindpunt.

Bovendien app registraties die u maakt in Hallo [Registratieportal toepassing](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) hebben Hallo volgende voorbehoud:

* Twee appgeheimen toegestaan per aanvraag-ID.
* Een app-registratie geregistreerd door een gebruiker met een persoonlijk Microsoft-account kan worden bekeken en beheerd alleen door een enkele ontwikkelaarsaccount. Deze kan niet worden gedeeld tussen meerdere ontwikkelaars.  Als u tooshare wilt de registratie van uw app in meerdere ontwikkelaars, kunt u de toepassing hello maken wanneer u zich aanmeldt bij Hallo-portal voor registratie met een Azure AD-account.
* Er zijn enkele beperkingen op het Hallo-indeling van Hallo omleidings-URI die is toegestaan. Zie de volgende sectie Hallo voor meer informatie over omleidings-URI's.

## <a name="restrictions-on-redirect-uris"></a>Beperkingen voor omleidings-URI 's
Apps die zijn geregistreerd in de Portal voor registratie van toepassing hello zijn momenteel beperkt tooa beperkte reeks omleidings-URI-waarden. Omleidings-URI voor web-apps en services met het schema Hallo beginnen moet Hallo `https`, en alle omleidings-URI-waarden moeten delen één DNS-domein. U kunt bijvoorbeeld een web-app met een van deze omleidings-URI's niet registreren:

`https://login-east.contoso.com`  
`https://login-west.contoso.com`

Hallo registratie system Vergelijkt Hallo volledige DNS-naam van Hallo bestaande omleidings-URI toohello DNS-naam van Hallo omleidings-URI die u wilt toevoegen. Hallo aanvraag tooadd Hallo DNS-naam mislukken als één Hallo volgende voorwaarden wordt voldaan:  

* Hallo volledige DNS-naam van Hallo nieuwe omleidings-URI komt niet overeen met de Hallo DNS-naam van Hallo bestaande omleidings-URI.
* Hallo volledige DNS-naam van Hallo nieuwe omleidings-URI is niet een subdomein van Hallo bestaande omleidings-URI.

Als bijvoorbeeld Hallo app heeft deze omleidings-URI:

`https://login.contoso.com`

U kunt tooit als volgt toevoegen:

`https://login.contoso.com/new`

In dit geval overeenkomt Hallo DNS-naam exact. Of u kunt dit doen:

`https://new.login.contoso.com`

In dit geval verwijst u tooa DNS-subdomein van login.contoso.com. Als u een app waarvoor aanmelding east.contoso.com en aanmelding-west.contoso.com wilt als omleidings-URI's toohave, moet u toevoegen die omleidings-URI's in deze volgorde:

`https://contoso.com`  
`https://login-east.contoso.com`  
`https://login-west.contoso.com`  

U kunt de laatste twee omdat ze subdomeinen Hallo eerst omleidings-URI, Hallo toevoegen contoso.com. Deze beperking wordt verwijderd in een toekomstige release.

hoe tooregister een app in de Portal van de registratie van toepassing hello zien toolearn [hoe tooregister een app met Hallo v2.0-eindpunt](active-directory-v2-app-registration.md).

## <a name="restrictions-on-services-and-apis"></a>Beperkingen voor de API's en services
Op dit moment Hallo v2.0-eindpunt ondersteunt aanmelden voor een app die is geregistreerd in de Portal voor registratie van toepassing hello en die in de lijst met Hallo valt [verificatie stroomt ondersteund](active-directory-v2-flows.md). Deze apps kunnen echter OAuth 2.0-toegangstokens voor een zeer beperkt aantal resources aanschaffen. alleen voor toegang tot de Hallo v2.0-eindpunt problemen:

* Hallo-app die Hallo token aangevraagd. Een app kan een toegangstoken voor zichzelf, aanschaffen als Hallo logische app uit diverse verschillende onderdelen of lagen bestaat. toosee dit scenario in actie, Bekijk onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) zelfstudies.
* Hallo Outlook E-mail, agenda en contactpersonen REST-API's, die allemaal zich op https://outlook.office.com bevinden. toolearn hoe toowrite een app die toegang heeft tot deze API's, Zie Hallo [Office aan de slag](https://www.msdn.com/office/office365/howto/authenticate-Office-365-APIs-using-v2) zelfstudies.
* Microsoft Graph API's. U kunt meer lezen over [Microsoft Graph](https://graph.microsoft.io) en Hallo gegevens beschikbaar tooyou.

Er zijn geen andere services worden ondersteund op dit moment. Meer Microsoft Online Services worden toegevoegd in toekomstige, Hallo bovendien toosupport voor uw eigen op maat gemaakte Web-API's en services.

## <a name="restrictions-on-libraries-and-sdks"></a>Beperkingen voor bibliotheken en SDK 's
Ondersteuning voor Hallo v2.0-eindpunt is momenteel beperkt. Als u wilt dat toouse Hallo v2.0-eindpunt in een productietoepassing, hebt u deze opties:

* Als u een webtoepassing maakt, kunt u veilig Microsoft algemeen beschikbaar serverzijde middleware tooperform aanmelden en token-validatie. Deze omvatten Hallo OWIN Open ID Connect middleware voor ASP.NET en Hallo Node.js Passport-invoegtoepassing. Zie voor codevoorbeelden die gebruikmaken van Microsoft-middleware onze [aan de slag](active-directory-appmodel-v2-overview.md#getting-started) sectie.
* Als u een toepassing desktop of mobile bouwt, kunt u een van onze preview Microsoft Authentication Libraries (MSAL).  Deze bibliotheken zijn in een voorbeeld van productie ondersteund, dus is het veilig toouse ze in productietoepassingen. U kunt meer informatie over de gebruiksvoorwaarden Hallo Hallo bekijken en beschikbare bibliotheken in Hallo lezen onze [verificatie-bibliotheken verwijzing](active-directory-v2-libraries.md).
* Voor platforms die niet wordt gedekt door een Microsoft-bibliotheken, kunt u integreren met Hallo v2.0-eindpunt door rechtstreeks verzenden en ontvangen van protocolberichten in uw toepassingscode. Hallo v2.0 OpenID Connect en OAuth-protocollen [expliciet worden gedocumenteerd](active-directory-v2-protocols.md) toohelp uitvoeren van een dergelijke integratie.
* Ten slotte kunt u open source Open ID Connect en OAuth-bibliotheken toointegrate met Hallo v2.0-eindpunt. Hallo v2.0 protocol moet compatibel zijn met veel open-source-protocol bibliotheken zonder grote wijzigingen. Hallo-beschikbaarheid van dit soort bibliotheken varieert per taal en het platform. Hallo [Open ID Connect](http://openid.net/connect/) en [OAuth 2.0](http://oauth.net/2/) websites een lijst met populaire implementaties bijhouden. Zie voor meer informatie [Azure Active Directory-verificatie en v2.0 bibliotheken](active-directory-v2-libraries.md), en de lijst Hallo van voor open-source clientbibliotheken en voorbeelden die zijn getest met Hallo v2.0-eindpunt.

## <a name="restrictions-on-protocols"></a>Beperkingen voor protocollen
Hallo v2.0-eindpunt biedt geen ondersteuning voor SAML- of WS-Federation; ondersteunt alleen Open ID Connect en OAuth 2.0.  Niet alle functies en mogelijkheden van de OAuth-protocollen zijn opgenomen in Hallo v2.0-eindpunt. Deze protocol functies en mogelijkheden zijn momenteel *niet beschikbaar* in Hallo v2.0-eindpunt:

* ID-tokens die zijn uitgegeven door Hallo v2.0-eindpunt bevatten geen een `email` claim voor Hallo gebruiker, zelfs als u toestemming van Hallo gebruiker tooview hun e-mail verkrijgen.
* Hallo OpenID Connect gebruikersgegevens eindpunt is niet geïmplementeerd op Hallo v2.0-eindpunt. Alle gebruikersprofielgegevens die u mogelijk zou ontvangen op dit eindpunt is echter beschikbaar via Microsoft Graph Hallo `/me` eindpunt.
* Hallo v2.0-eindpunt biedt geen ondersteuning voor claims van verlenende functie of groep in de ID-tokens.
* Hallo [OAuth 2.0 Resource eigenaar wachtwoord referenties Grant](https://tools.ietf.org/html/rfc6749#section-4.3) wordt niet ondersteund door Hallo v2.0-eindpunt.

Daarnaast ondersteunt Hallo v2.0-eindpunt geen enige vorm van Hallo SAML of WS-Federation-protocollen.

toobetter begrijpen Hallo bereik van protocol functionaliteit ondersteund in Hallo v2.0-eindpunt, Lees onze [OpenID Connect en OAuth 2.0-protocol verwijzing](active-directory-v2-protocols.md).

## <a name="restrictions-for-work-and-school-accounts"></a>Beperkingen voor werk-en schoolaccounts
Als u Active Directory Authentication Library (ADAL) in Windows-toepassingen hebt gebruikt, hebt u mogelijk gebruikmaken van geïntegreerde Windows-verificatie, waarbij Hallo Security Assertion Markup Language (SAML) assertion grant ondernomen. Met deze machtiging federatieve gebruikers van Azure AD tenants kunnen achtergrond verifiëren met hun lokale Active Directory-exemplaar zonder referenties invoeren. Hallo SAML-verklaring grant wordt momenteel niet ondersteund op Hallo v2.0-eindpunt.
