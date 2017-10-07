---
title: aaaUnderstanding hello OAuth2 impliciete verlenen stroom in Azure AD | Microsoft Docs
description: Meer informatie over Azure Active Directory-implementatie van Hallo OAuth2 impliciete grant stroom, en of deze geschikt is voor uw toepassing.
services: active-directory
documentationcenter: dev-center-name
author: jmprieur
manager: mbaldwin
editor: 
ms.assetid: 90e42ff9-43b0-4b4f-a222-51df847b2a8d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/15/2016
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: 3402e6619709e1a5b1e790ffd79dc62139552d9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understanding-hello-oauth2-implicit-grant-flow-in-azure-active-directory-ad"></a>Understanding Hallo OAuth2 impliciete verlenen stroom in Azure Active Directory (AD)
Hallo OAuth2 impliciete verlenen is algemeen wordt Hallo grant met de langste lijst Hallo van beveiligingsproblemen in Hallo OAuth2-specificatie. En nog dat Hallo benadering geïmplementeerd door ADAL JS en Hallo een we raden u aan bij de SPA-toepassingen schrijven is. Wat te bieden? Het is een kwestie van de voor-en nadelen: en zoals blijkt, Hallo impliciete grant Hallo aanbevolen benadering kunt u oefenen voor toepassingen die een Web-API via JavaScript via een browser gebruiken.

## <a name="what-is-hello-oauth2-implicit-grant"></a>Wat is Hallo OAuth2 impliciete verlenen?
Hallo ultieme [OAuth2 autorisatie code grant](https://tools.ietf.org/html/rfc6749#section-1.3.1) Hallo authorization grant dat gebruikmaakt van twee afzonderlijke eindpunten is. Hallo autorisatie eindpunt wordt Hallo gebruiker interactie fase, wat in een autorisatiecode resulteert gebruikt. Hallo-tokeneindpunt wordt vervolgens gebruikt door Hallo-client voor het uitwisselen van Hallo-code voor een toegangstoken en vaak ook een vernieuwingstoken. Webtoepassingen zijn, vereist toopresent hun eigen referenties toohello token toepassingseindpunt, zodat hello autorisatie server Hallo-client verifiëren kan.

Hallo [OAuth2 impliciete grant](https://tools.ietf.org/html/rfc6749#section-1.3.2) is een variant van andere toestemming verleent. Kunt u een client tooobtain een toegangstoken (en id_token, wanneer u [OpenId Connect](http://openid.net/specs/openid-connect-core-1_0.html)) rechtstreeks vanuit Hallo autorisatie eindpunt zonder verbinding met de Hallo-tokeneindpunt noch authenticatie Hallo-client. Deze variant is speciaal ontworpen voor toepassingen die worden uitgevoerd in een webbrowser die JavaScript zijn gebaseerd: in oorspronkelijke OAuth2-specificatie hello, tokens worden geretourneerd in een URI-fragment. Die maakt Hallo token bits beschikbaar toohello JavaScript-code in Hallo-client, maar deze wordt gegarandeerd dat ze niet opgenomen in omleidingen naar Hallo-server. Retourneren van tokens via de browser wordt omgeleid rechtstreeks vanuit het Hallo-eindpunt voor autorisatie. Er wordt ook Hallo profiteren van alle vereisten voor cross-origin-aanroepen nodig zijn als JavaScript-toepassing hello vereist toocontact Hallo token eindpunt is elimineren.

Een belangrijk kenmerk van Hallo OAuth2 impliciete verlenen is Hallo feit die dergelijke stromen nooit vernieuwen van tokens toohello client retourneren. Zoals we in de volgende sectie hello zien, die is niet echt nodig en is in feite een beveiligingsprobleem.

## <a name="suitable-scenarios-for-hello-oauth2-implicit-grant"></a>Geschikte scenario's voor Hallo OAuth2 impliciete verlenen
Als Hallo OAuth2-specificatie zelf wordt gedeclareerd, is hello impliciete verlenen ontwikkeld tooenable gebruikersagent toepassingen – dat wil zeggen toosay, JavaScript-toepassingen uitvoeren vanuit een browser. Hallo-kenmerk van dergelijke toepassingen definiëren is dat de JavaScript-code wordt gebruikt voor toegang tot serverbronnen (meestal een Web-API) en voor het bijwerken van toepassing hello UX dienovereenkomstig. Vergelijken met toepassingen zoals Gmail of Outlook Web Access: wanneer u een bericht van het Postvak selecteert, alleen het Hallo-bericht visualisatie Configuratiescherm wijzigingen toodisplay Hallo nieuwe selectie terwijl de rest Hallo van Hallo pagina blijft ongewijzigd. Dit is anders dan bij traditionele omleiding gebaseerde Web-apps, waarbij elke gebruikersinteractie resulteert in een terugpostactie volledige pagina en een volledige paginaweergave van de nieuwe serverantwoord Hallo.

Toepassingen die Hallo op basis van JavaScript benadering tooits extreme nemen heten toepassingen met één pagina of kuuroorden: Hallo idee is dat deze toepassingen alleen maar een initiële HTML-pagina en de bijbehorende JavaScript, met alle opeenvolgende interacties wordt aangestuurd door Web-API-aanroepen uitgevoerd via JavaScript. Echter, hybride benaderingen, waarbij toepassing hello voornamelijk terugposten aangestuurde maar voert incidentele JS aanroepen, zijn niet ongewoon – Hallo discussie over het gebruik van de impliciete stroom is ook relevant voor de.

Omleiding gebaseerde toepassingen beveiligen doorgaans hun aanvragen via de cookies, maar die benadering niet ook voor JavaScript-toepassingen werkt. Cookies werken alleen op basis van Hallo domein die ze voor, zijn gegenereerd tijdens het JavaScript-aanroepen kunnen worden omgeleid naar andere domeinen. In feite die vaak Hallo geval zal zijn: vergelijken met toepassingen aanroepen van Microsoft Graph API, Office-API, Azure API – alle die zich buiten het Hallo-domein waar de toepassing hello wordt geleverd. Een stijgende trend voor JavaScript-toepassingen is toohave geen back-end op alle relying 100% 3e partij Web-API's tooimplement hun zakelijke-functie.

Hallo is voorkeursmethode voor het beveiligen van aanroepen tooa Web-API momenteel toouse hello OAuth2 bearer-token benadering, waarbij elke aanroep gaat vergezeld van een OAuth2-toegangstoken. Hallo-Web-API Hallo binnenkomende toegangstoken moet worden gecontroleerd en, als het wordt gevonden het benodigde scopes hello, verleent toegang toohello bewerking aangevraagd. Hallo impliciete stroom biedt een handige mechanisme voor JavaScript toepassingen tooobtain toegangstokens voor een Web-API biedt dat veel voordelen in acht toocookies:

* Tokens op betrouwbare wijze kunnen worden verkregen zonder dat u hoeft voor cross-origin-aanroepen – verplichte registratie van Hallo omleidings-URI toowhich tokens zijn retourneren zorgt ervoor dat de tokens niet worden overgezet
* JavaScript-toepassingen kunnen verkrijgen zoveel toegangstokens als ze nodig hebben, voor als veel Web-API's ze doel – zonder beperking voor domeinen
* HTML5-functies, zoals sessie- of lokale opslag verlenen volledige controle over token caching en beheer van de levensduur terwijl cookies management ondoorzichtige toohello app
* Toegangstokens zijn niet vatbaar tooCross-site aanvraag kunnen worden vervalst (CSRF) aanvallen

Hallo impliciete grant stroom biedt geen uitgeven voor vernieuwen van tokens, voornamelijk om veiligheidsredenen. Een vernieuwingstoken is niet zo nauwkeurig binnen het bereik als toegangstokens, nog veel meer power daarom veel meer schade wordt toegebracht als deze is gelekt uit verlenen. In impliciete flow hello, tokens worden afgeleverd in Hallo-URL, daarom Hallo risico onderschept is hoger dan in Hallo autorisatie code verlenen.

Let echter op dat een JavaScript-toepassing een ander mechanisme beschikt voor het vernieuwen van de toegangstokens herhaaldelijk Hallo zonder gebruiker te vragen om referenties. Hallo toepassingen kunnen gebruikmaken van een verborgen iframe tooperform nieuwe aanvragen voor beveiligingstokens voor Hallo autorisatie eindpunt van Azure AD: zolang Hallo browser nog een actieve sessie heeft (lezen: heeft een sessiecookie) Hallo verificatieaanvraag op basis van hello Azure AD-domein. met succes kan hoeven de interactie van de gebruiker optreden.

Dit model hebben Hallo JavaScript toepassing hello mogelijkheid tooindependently toegangstokens vernieuwen en zelfs nieuwe gemaakt voor een nieuwe API verkrijgen (op voorwaarde dat het Hallo gebruiker eerder ingestemd voor hen. Zo voorkomt u Hallo toegevoegde last van ophalen, onderhouden en een hoge waarde-artefacten, zoals een vernieuwingstoken beveiligen. Hallo-artefacten waardoor Hallo achtergrond verlenging mogelijk sessiecookie hello Azure AD, wordt buiten de toepassing hello beheerd. Een ander voordeel van deze benadering is dat een gebruiker kan afmelden bij Azure AD, met behulp van een Hallo-toepassingen die zijn aangemeld bij Azure AD, in een van de browsertabbladen Hallo uitgevoerd. Dit resulteert in Hallo verwijdering van hello Azure AD-sessiecookie en Hallo JavaScript-toepassing automatisch verliest Hallo mogelijkheid toorenew tokens voor Hallo gebruiker afgemeld.

## <a name="is-hello-implicit-grant-suitable-for-my-app"></a>Hallo impliciete grant geschikt is voor mijn app?
Hallo impliciete grant geeft meer risico's dan andere verleent en Hallo gebieden moet u toopay aandacht tooare goed wordt gedocumenteerd. Bijvoorbeeld: [misbruik van Access Token tooImpersonate Resource-eigenaar in impliciete stromen] [ OAuth2-Spec-Implicit-Misuse] en [risicomodel van OAuth 2.0- en beveiligingsoverwegingen] [ OAuth2-Threat-Model-And-Security-Implications]). Hallo hogere risicoprofiel is echter grotendeels vanwege toohello feit dat is bedoeld als tooenable toepassingen die active programmacode, geleverd door een externe bron tooa browser worden uitgevoerd. Als u van plan bent een SPA-architectuur, hebt u geen back-end-onderdelen of van plan bent een Web-API via JavaScript tooinvoke, gebruik van Hallo impliciete stroom voor de aanschaf van het token wordt aanbevolen.

Als uw toepassing een native client is, niet Hallo impliciete stroom een geweldige aanpassen. Hallo afwezigheid van sessiecookie hello Azure AD in de context van een native client Hallo ontneemt uw toepassing hello middelen van het onderhouden van een lange levensduur sessie. Wat betekent dat uw toepassing, wordt herhaaldelijk Hallo gebruiker gevraagd bij het verkrijgen van toegangstokens voor nieuwe resources.

Als u een webtoepassing met een back-end en gebruiken van een API van de back endcode ontwikkelt, is Hallo impliciete stroom ook niet geschikt. Andere verleent geven u nog veel meer power. Hallo OAuth2 client referenties grant biedt bijvoorbeeld Hallo mogelijkheid tooobtain tokens die overeenkomen met de machtigingen Hallo toohello toepassing zelf, als tegengestelde toouser delegeringen toegewezen. Dit betekent dat het Hallo-client heeft Hallo mogelijkheid toomaintain toegang op programmeerniveau tooresources, zelfs wanneer een gebruiker niet actief is bezig met een sessie, enzovoort. Niet alleen die, maar deze verleent geven hogere beveiligingsgaranties. Bijvoorbeeld, browser van de gebruiker Hallo toegangstokens nooit doorvoer, ze geen risico wordt opgeslagen in de browsergeschiedenis hello, enzovoort. Hallo-clienttoepassing kunt ook sterke verificatie uitvoeren bij het aanvragen van een token.

## <a name="next-steps"></a>Volgende stappen
* Voor een volledige lijst met bronnen voor ontwikkelaars, met inbegrip van de referentie-informatie voor het Hallo-protocollen en OAuth2-machtiging verlenen stromen ondersteuning door Azure AD raadpleegt u toohello [Ontwikkelaarshandleiding voor Azure AD][AAD-Developers-Guide]
* Zie [hoe een toepassing met Azure AD toointegrate] [ ACOM-How-To-Integrate] voor extra diepte op Hallo integratie toepassingsproces.

<!--Image references-->

<!--Reference style links in use-->
[AAD-Developers-Guide]: active-directory-developers-guide.md
[ACOM-How-And-Why-Apps-Added-To-AAD]: active-directory-how-applications-are-added.md
[ACOM-How-To-Integrate]: active-directory-how-to-integrate.md
[OAuth2-Spec-Implicit-Misuse]: https://tools.ietf.org/html/rfc6749#section-10.16
[OAuth2-Threat-Model-And-Security-Implications]: https://tools.ietf.org/html/rfc6819
