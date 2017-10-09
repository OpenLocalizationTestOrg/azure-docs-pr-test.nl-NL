---
title: aaaAuthentication scenario's voor Azure AD | Microsoft Docs
description: Een overzicht van Hallo vijf meest voorkomende verificatie scenario's voor Azure Active Directory (AAD)
services: active-directory
documentationcenter: dev-center-name
author: skwan
manager: mbaldwin
editor: 
ms.assetid: 0c84e7d0-16aa-4897-82f2-f53c6c990fd9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: skwan
ms.custom: aaddev
ms.openlocfilehash: 5b391e3f096fcb52934c4a8aff08688352bfd3dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-scenarios-for-azure-ad"></a>Authentication Scenarios for Azure AD (Verificatiescenario's voor Azure AD)
Azure Active Directory (Azure AD) vereenvoudigt de verificatie voor ontwikkelaars dankzij de identiteit als een service met ondersteuning voor industriestandaard-zoals OAuth 2.0 en OpenID Connect, evenals open-source bibliotheken voor verschillende platforms toohelp u protocollen Start snel coderen. Dit document helpt u begrijpen Hallo verschillende scenario's Azure AD-ondersteunt en ziet u hoe tooget gestart. Het onderverdeeld in Hallo uit te voeren:

* [Basisprincipes van verificatie in Azure AD](#basics-of-authentication-in-azure-ad)
* [Claims in Azure AD-beveiligingstokens](#claims-in-azure-ad-security-tokens)
* [Basisbeginselen van het registreren van een toepassing in Azure AD](#basics-of-registering-an-application-in-azure-ad)
* [Toepassingstypen en scenario 's](#application-types-and-scenarios)
  
  * [Web Browser tooWeb toepassing](#web-browser-to-web-application)
  * [Toepassing van één pagina (SPA)](#single-page-application-spa)
  * [Systeemeigen toepassing tooWeb API](#native-application-to-web-api)
  * [Web Application tooWeb API](#web-application-to-web-api)
  * [Daemon of servertoepassing tooWeb API](#daemon-or-server-application-to-web-api)

## <a name="basics-of-authentication-in-azure-ad"></a>Basisprincipes van verificatie in Azure AD
Als u niet bekend met de basisconcepten van verificatie in Azure AD bent, leest u in deze sectie. Anders kunt u tooskip omlaag te[toepassingstypen en scenario's](#application-types-and-scenarios).

Laten we eens Hallo meest eenvoudige scenario waarin de identiteit vereist is: een gebruiker in een webbrowser nodig tooauthenticate tooa-webtoepassing. Dit scenario wordt beschreven in Hallo uitgebreider [webbrowser tooWeb toepassing](#web-browser-to-web-application) sectie, maar een nuttig de punt tooillustrate starten Hallo mogelijkheden van Azure AD en de werking van Hallo scenario concept. Overweeg het volgende diagram voor dit scenario Hallo:

![Overzicht van eenmalige aanmelding tooweb toepassing](./media/active-directory-authentication-scenarios/basics_of_auth_in_aad.png)

Met Hallo diagram hierboven in gedachten, dit is wat u moet tooknow over de verschillende onderdelen:

* Azure AD is verantwoordelijk voor het Hallo-identiteit van gebruikers en toepassingen die zijn opgenomen in de map van een organisatie te controleren en uiteindelijk uitgeven beveiligingstokens na een geslaagde verificatie van gebruikers en toepassingen Hallo-identiteitsprovider.
* Een toepassing die wil toooutsource verificatie tooAzure AD moet worden geregistreerd in Azure AD dat registreert en het Hallo-app in de directory Hallo wordt aangeduid.
* Ontwikkelaars kunnen gebruiken Hallo open-source Azure AD-bibliotheken toomake verificatie eenvoudig hello Protocoldetails voor u kan verwerken. Zie [Azure Active Directory Authentication Libraries](active-directory-authentication-libraries.md) voor meer informatie.

• Eenmaal een gebruiker is geverifieerd, Hallo toepassing van de gebruiker hello security token tooensure moet valideren dat de verificatie is geslaagd voor Hallo bedoeld partijen. Ontwikkelaars kunnen Hallo opgegeven verificatie-bibliotheken toohandle validatie van een token van Azure AD, met inbegrip van JSON Web Tokens (JWT) of SAML 2.0 gebruiken. Als u tooperform validatie handmatig wilt, raadpleegt u Hallo [JWT-Token Handler](https://msdn.microsoft.com/library/dn205065.aspx) documentatie.

> [!IMPORTANT]
> Azure AD maakt gebruik van openbare-sleutelcryptografie toosign tokens en controleer of ze geldig zijn. Zie [belangrijke informatie over het ondertekenen van sleutel Rollover in Azure AD](active-directory-signing-key-rollover.md) voor meer informatie over de benodigde logica Hallo moet u in uw toepassing tooensure hebben wordt altijd bijgewerkt met de meest recente sleutels Hallo.
> 
> 

• Hallo stroom van aanvragen en antwoorden voor Hallo verificatieproces wordt bepaald door het Hallo-verificatieprotocol dat is gebruikt, zoals OAuth 2.0, OpenID Connect, WS-Federation of SAML 2.0. Deze protocollen worden besproken in Hallo nader [Azure Active Directory-verificatieprotocollen](active-directory-authentication-protocols.md) onderwerp en in de volgende secties voor Hallo.

> [!NOTE]
> Azure AD Hallo OAuth 2.0 ondersteunt en OpenID Connect standaarden uitgebreide maken gebruik van bearer-tokens, weergegeven als JWTs bearer-tokens. Een bearer-token is een lichtgewicht beveiligingstoken dat verleent 'bearer' toegang tooa Hallo beveiligde resource. In dit opzicht is Hallo 'bearer' een partij die Hallo token kan opleveren. Hoewel een partij moet eerst worden geverifieerd bij Azure AD tooreceive hello bearer-token, als Hallo vereist stappen worden niet genomen toosecure Hallo-token in overdracht en opslag, kunt u het probleem is onderschept en gebruikt door een onbedoelde partij. Sommige beveiligingstokens beschikken over een ingebouwde mechanisme om te voorkomen dat onbevoegden kunnen gebruiken, worden de bearer-tokens hebben geen dit mechanisme en moeten worden overgebracht in een beveiligd kanaal zoals transport layer security (HTTPS). Als een bearer-token wordt verzonden in Hallo wissen, wordt een man-in Hallo middelste aanval kan worden gebruikt door een kwaadwillende tooacquire Hallo-token en gebruiken voor een resource van de beveiligde tooa onbevoegde toegang. Hallo dezelfde beveiligings-principals van toepassing wanneer caching bearer-tokens voor later gebruik of op te slaan. Altijd voor zorgen dat uw toepassing worden verzonden en bearer-tokens worden opgeslagen op een veilige manier. Zie voor meer beveiligingsoverwegingen op bearer-tokens [RFC 6750 sectie 5](http://tools.ietf.org/html/rfc6750).
> 
> 

Nu dat u een overzicht van Hallo basics Hallo secties toounderstand lezen hebt hoe u inrichting werkt in Azure AD en biedt ondersteuning voor algemene scenario's hello Azure AD.

## <a name="claims-in-azure-ad-security-tokens"></a>Claims in Azure AD-beveiligingstokens
Beveiligingstokens die zijn uitgegeven door Azure AD bevatten claims of beweringen van informatie over het Hallo-onderwerp dat is geverifieerd. Deze claims kunnen door de toepassing hello worden gebruikt voor verschillende taken. Bijvoorbeeld kunnen ze worden gebruikte toovalidate Hallo token, identificeren van de certificaathouder Hallo directory-tenant, gebruikersgegevens weergeven, bepalen van de certificaathouder Hallo autorisatie, enzovoort. Hallo claims aanwezig zijn in een bepaalde beveiligingstoken zijn afhankelijk van Hallo type token, Hallo type referentie gebruikt tooauthenticate Hallo gebruiker en de configuratie van de toepassing hello. Een korte beschrijving van elk type claim verzonden door Azure AD wordt vermeld in de onderstaande tabel voor Hallo. Voor meer informatie raadpleegt u te[ondersteund Token en claimtypen](active-directory-token-and-claims.md).

| Claim | Beschrijving |
| --- | --- |
| Toepassings-id |Hallo-toepassing die van Hallo-token gebruikmaakt te identificeren. |
| Doelgroep |Hallo geadresseerde resource identificeert Hallo-token is bedoeld voor. |
| Application Authentication Context Class Reference |Geeft aan hoe client Hallo geverifieerde (openbare client versus vertrouwelijke client). |
| Verificatie Instant |Registreert Hallo datum en tijd waarop Hallo verificatie heeft plaatsgevonden. |
| Verificatiemethode |Hiermee wordt aangegeven hoe Hallo onderwerp van Hallo-token is geverifieerd (wachtwoord, certificaat, enzovoort). |
| Voornaam |Biedt de voornaam Hallo van Hallo gebruiker zoals ingesteld in Azure AD. |
| Groepen |Object-id's van Azure AD-groepen Hallo gebruiker lid van is bevat. |
| Id-provider |Registreert Hallo identiteitsprovider die geverifieerd Hallo onderwerp van Hallo-token. |
| Verleend aan |Registreert Hallo tijd op welke Hallo token is uitgegeven, vaak gebruikt voor het token versheid. |
| certificaatverlener |Identificeert Hallo STS dat hello token, evenals hello Azure AD-tenant verzonden. |
| Achternaam |Biedt Hallo achternaam van de gebruiker Hallo zoals ingesteld in Azure AD. |
| Naam |Biedt een menselijke leesbare waarde die Hallo onderwerp van Hallo-token aangeeft. |
| Object-Id |Bevat een niet-wijzigbaar, unieke id van Hallo onderwerp in Azure AD. |
| Rollen |Beschrijvende namen bevat van de rollen van Azure AD-toepassing die gebruiker Hallo heeft gekregen. |
| Bereik |Hiermee wordt aangegeven Hallo machtigingen verleend toohello client-toepassing. |
| Onderwerp |Hiermee wordt aangegeven Hallo principal over welke Hallo asserts token informatie. |
| Tenant-Id |Bevat een niet-wijzigbaar, unieke identificatie van Hallo directory-tenant die Hallo token uitgegeven. |
| Levensduur van token |Hiermee definieert u Hallo tijdsinterval waarbinnen een token geldig is. |
| Principalnaam van gebruiker |Hallo user principal name van Hallo onderwerp bevat. |
| Versie |Hallo-versienummer van Hallo token bevat. |

## <a name="basics-of-registering-an-application-in-azure-ad"></a>Basisbeginselen van het registreren van een toepassing in Azure AD
Alle toepassingen die verificatie tooAzure die AD moet worden geregistreerd in een map heeft. Deze stap omvat het Azure AD om te informeren over uw toepassing, met inbegrip van Hallo URL op waar deze zich bevindt, Hallo URL toosend beantwoordt na verificatie Hallo URI tooidentify uw toepassing en meer. Deze informatie is vereist voor een aantal belangrijke oorzaken hebben:

* Azure AD moet coördinaten toocommunicate met Hallo toepassing bij het verwerken van eenmalige aanmelding of uitwisselen van tokens. Deze omvatten Hallo volgende:
  
  * Aanvraag-ID-URI: Hallo-id voor een toepassing. Deze waarde wordt tooAzure AD tijdens verificatie tooindicate welke toepassing hello aanroeper wil een token voor verzonden. Deze waarde is ook opgenomen in Hallo token zodat Hallo toepassing weet dat Hallo doel bedoeld was.
  * Antwoord-URL en de omleidings-URI: In geval van een web-API of een webtoepassing Hallo Hallo antwoord-URL is Hallo locatie toowhich Azure AD Hallo verificatieantwoord verzendt, met inbegrip van een token als verificatie gelukt is. In geval van een systeemeigen toepassing hello Hallo omleidings-URI is dat een unieke id toowhich Azure AD Hallo gebruikersagent in een OAuth 2.0-aanvraag wordt omgeleid.
  * Toepassings-ID: Hallo ID voor een toepassing die wordt gegenereerd door Azure AD wanneer de toepassing hello is geregistreerd. Bij het aanvragen van een autorisatiecode of token Hallo toepassings-ID en sleutel verzonden tooAzure AD tijdens de verificatie.
  * Sleutel: Hallo-sleutel die samen met een toepassings-ID wordt verzonden bij het verifiëren van tooAzure AD toocall een web-API.
* Azure AD-behoeften tooensure Hallo toepassing hello vereiste machtigingen tooaccess uw directorygegevens andere toepassingen in uw organisatie, enzovoort

Inrichting wordt duidelijker wanneer u begrijpt dat er zijn twee soorten toepassingen die kunnen worden ontwikkeld en geïntegreerd met Azure AD:

* Enkele van de toepassing van de tenant: een toepassing voor één tenant is bedoeld voor gebruik in een organisatie. Dit zijn doorgaans line-of-business (LoB)-toepassingen geschreven door de ontwikkelaar van een onderneming. Een toepassing voor één tenant moet alleen toobe waartoe gebruikers in een map en als gevolg hiervan, alleen moet toobe ingericht in één directory. Deze toepassingen worden doorgaans door een ontwikkelaar in Hallo organisatie geregistreerd.
* Multitenant-toepassing: een multitenant-toepassing is niet bedoeld voor gebruik in veel organisaties is slechts één organisatie. Dit zijn doorgaans software-as-a-service (SaaS)-toepassingen geschreven door een onafhankelijke softwareleverancier (ISV). Multitenant-toepassingen moeten toobe ingericht in elke map waar ze worden gebruikt, waarvoor een gebruiker of beheerder toestemming tooregister ze. Dit proces toestemming wordt gestart wanneer een toepassing in Hallo directory is geregistreerd en toegang toohello Graph API of een andere web-API krijgt. Wanneer een gebruiker of beheerder van een andere organisatie zich registreert toouse Hallo toepassing, zijn ze een dialoogvenster waarin Hallo machtigingen die vereist zijn voor de toepassing hello weergegeven. Hallo-gebruiker of beheerder kan toestemming toohello toepassing waarmee Hallo toepassing toegang toohello gegevens vermeld, en ten slotte registers Hallo-toepassing in de directory. Zie voor meer informatie [overzicht van Hallo toestemming Framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).

Enkele aanvullende overwegingen ontstaan bij het ontwikkelen van een toepassing met meerdere tenants in plaats van een toepassing voor één tenant. Bijvoorbeeld, als u uw toepassing beschikbaar toousers in meerdere mappen doorvoert, moet u een mechanisme toodetermine waarover ze zich in. Een toepassing voor één tenant hoeft slechts toolook in een eigen map voor een gebruiker, terwijl een multitenant-toepassing een specifieke gebruiker uit alle Hallo mappen tooidentify in Azure AD moet. tooaccomplish deze taak Azure AD levert een algemene eindpunt voor authenticatie, waarbij elke toepassing met meerdere tenants aanmelden, in plaats van een tenantspecifieke-eindpunt wenden kan. Dit eindpunt is https://login.microsoftonline.com/common voor alle mappen in Azure AD, terwijl een eindpunt tenantspecifieke mogelijk https://login.microsoftonline.com/contoso.onmicrosoft.com. algemene Hallo-eindpunt is vooral belangrijk tooconsider bij het ontwikkelen van uw toepassing omdat u Hallo benodigde logica toohandle meerdere tenants tijdens het aanmelden, afmelden en validatie van tokens moet.

Als u een toepassing voor één tenant momenteel ontwikkelt, maar toomake wilt deze beschikbaar toomany organisaties, kunt u eenvoudig doorvoeren wijzigingen toohello toepassing en de configuratie in Azure AD-toomake het multitenant-compatibel. Bovendien Hallo maakt gebruik van Azure AD hetzelfde voor alle tokens in alle mappen de handtekeningsleutel, of u biedt verificatie in een één tenant of multitenant-toepassing.

Elk scenario vermeld in dit document bevat een subsectie die de vereisten voor inrichting beschrijft. Voor meer gedetailleerde informatie over het inrichten van een toepassing in Azure AD en Hallo verschillen tussen één en multitenant-toepassingen, Zie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md) voor meer informatie. Blijven lezen toounderstand Hallo algemene toepassingsscenario's in Azure AD.

## <a name="application-types-and-scenarios"></a>Toepassingstypen en scenario 's
Hallo-scenario's beschreven in dit document kan worden ontwikkeld met behulp van verschillende talen en platforms. Ze worden alle ondersteund door volledige codevoorbeelden die beschikbaar zijn in onze [codevoorbeelden begeleiden](active-directory-code-samples.md), of rechtstreeks vanuit het Hallo bijbehorende [GitHub-opslagplaatsen voor voorbeeld](https://github.com/Azure-Samples?utf8=%E2%9C%93&query=active-directory). Bovendien, als uw toepassing een bepaald of een segment van een end-to-end-scenario moet, kan in de meeste gevallen functionaliteit van die worden toegevoegd onafhankelijk. Als u een systeemeigen toepassing die een web-API aanroept hebt, kunt u bijvoorbeeld eenvoudig een webtoepassing die ook Hallo web-API-aanroepen toevoegen. Hallo volgende diagram ziet u deze scenario's en de toepassingstypen, en hoe de andere onderdelen kunnen worden toegevoegd:

![Toepassingstypen en scenario 's](./media/active-directory-authentication-scenarios/application_types_and_scenarios.png)

Hallo vijf primaire toepassingsscenario's ondersteund door Azure AD zijn:

* [Web Browser tooWeb toepassing](#web-browser-to-web-application): een gebruiker moet toosign in tooa-webtoepassing die wordt beveiligd door Azure AD.
* [Eén pagina toepassing (SPA)](#single-page-application-spa): een gebruiker moet toosign in tooa één pagina toepassing die wordt beveiligd door Azure AD.
* [Systeemeigen toepassing tooWeb API](#native-application-to-web-api): een systeemeigen toepassing die wordt uitgevoerd op een telefoon, tablet of PC behoeften tooauthenticate een gebruiker tooget bronnen van een web-API die wordt beveiligd door Azure AD.
* [Web-API van Application tooWeb](#web-application-to-web-api): een webtoepassing moet tooget bronnen van een web-API die zijn beveiligd door Azure AD.
* [Daemon of servertoepassing tooWeb API](#daemon-or-server-application-to-web-api): een daemontoepassing of een servertoepassing zonder gebruikersinterface web moet tooget bronnen van een web-API die zijn beveiligd door Azure AD.

### <a name="web-browser-tooweb-application"></a>Web Browser tooWeb toepassing
Deze sectie beschrijft een toepassing die een gebruiker in een webtoepassing web browser tooa verifieert. In dit scenario webtoepassing Hallo van Hallo gebruiker browser toosign stuurt ze in tooAzure AD. Azure AD retourneert een antwoord aanmelden via de browser van de gebruiker hello, met daarin de claims over Hallo-gebruiker in een beveiligingstoken. Dit scenario biedt ondersteuning voor aanmelding Hallo WS-Federation, SAML 2.0 en OpenID Connect te gebruiken.

#### <a name="diagram"></a>Diagram
![Authenticatiestroom voor tooweb browsertoepassing](./media/active-directory-authentication-scenarios/web_browser_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Beschrijving van de stroom Protocol
1. Wanneer een gebruiker Hallo toepassing bezoeken en moet toosign in, worden ze omgeleid via een aanmeldingsverzoek toohello verificatie-eindpunt in Azure AD.
2. Hallo-gebruiker zich aanmeldt op de aanmeldingspagina Hallo.
3. Als verificatie geslaagd is, wordt Azure AD maakt geen verificatietoken en retourneert een aanmeldingspagina antwoord toohello toepassing antwoord-URL die is geconfigureerd in hello Azure-Portal. Voor een productietoepassing moet dit antwoord-URL HTTPS. Hallo heeft een token geretourneerd bevat claims over Hallo gebruiker en Azure AD die nodig zijn voor Hallo toepassing toovalidate Hallo token.
4. de toepassing Hello valideert Hallo token met behulp van een openbare ondertekeningssleutel en informatie over de uitgever beschikbaar bij Hallo document met federatieve metagegevens voor Azure AD. Nadat de toepassing hello Hallo token valideert, wordt in Azure AD een nieuwe sessie begint met het Hallo-gebruiker. Deze sessie kan Hallo gebruiker tooaccess Hallo toepassing totdat deze verloopt.

#### <a name="code-samples"></a>Codevoorbeelden
Zie de codevoorbeelden Hallo voor webbrowser tooWeb toepassingsscenario's. En terugkomen vaak--we alle Hallo tijd nieuwe voorbeelden toevoegen. [Web Browser tooWeb toepassing](active-directory-code-samples.md#web-browser-to-web-application).

#### <a name="registering"></a>Registreren
* Één Tenant: Als u een toepassing voor uw organisatie maakt, moet deze worden geregistreerd in de directory van uw bedrijf met behulp van hello Azure-Portal.
* Multitenant: Als u een toepassing die kan worden gebruikt door gebruikers buiten uw organisatie maakt, het moet worden geregistreerd in de directory van uw bedrijf, maar ook moet worden geregistreerd in elke organisatie directory die Hallo toepassing zullen gebruiken. toomake uw toepassing in de directory, kunt u een aanmeldingsproces opnemen voor uw klanten kunnen ze tooconsent tooyour toepassing. Wanneer ze zich registreren voor uw toepassing, worden ze een dialoogvenster waarin Hallo machtigingen Hallo toepassing is vereist, en vervolgens Hallo optie tooconsent weergegeven. Afhankelijk van een beheerder in Hallo Hallo vereist machtigingen andere organisatie mogelijk toogive toestemming vereist. Wanneer het Hallo-gebruiker of beheerder hiermee akkoord gaat, wordt Hallo toepassing geregistreerd in de directory. Zie voor meer informatie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Verlopen van het token
Hallo gebruikerssessie verloopt wanneer Hallo levensduur van Hallo token dat is uitgegeven door Azure AD is verlopen. Uw toepassing kunt inkorten deze periode indien gewenst, zoals het ondertekenen van de gebruikers op basis van een periode van inactiviteit. Wanneer het Hallo-sessie is verlopen, Hallo gebruiker worden opgegeven na vragen aan gebruiker toosign in opnieuw.

### <a name="single-page-application-spa"></a>Toepassing van één pagina (SPA)
Deze sectie beschrijft de verificatie voor één pagina toepassing, die gebruikmaakt van Azure AD en hello impliciete OAuth 2.0-autorisatie verlenen toosecure de web-API back-end. Toepassingen met één pagina doorgaans zijn geordend als een JavaScript-presentatie laag (front-end) die wordt uitgevoerd in de browser hello en in een Web-API back-end die wordt uitgevoerd op een server en implementeert Hallo bedrijfslogica van toepassing. Zie toolearn meer informatie over Hallo impliciete authorization grant en helpen u beslissen of deze geschikt is voor uw toepassingsscenario [Understanding Hallo OAuth2 impliciete stroom in Azure Active Directory verlenen](active-directory-dev-understanding-oauth2-implicit-grant.md).

In dit scenario wanneer Hallo gebruiker zich aanmeldt, Hallo JavaScript front end gebruikt [Active Directory Authentication Library voor JavaScript (ADAL. JS)](https://github.com/AzureAD/azure-activedirectory-library-for-js/tree/dev) en Hallo impliciete toestemming verlenen tooobtain een token ID (id_token) van Azure AD. Hallo-token in de cache wordt opgeslagen en Hallo client gekoppeld toohello aanvraag als Hallo bearer-token bij het maken van back-end, die is beveiligd met Hallo OWIN middleware tooits Web-API aanroepen. 

#### <a name="diagram"></a>Diagram
![Diagram van één pagina toepassing](./media/active-directory-authentication-scenarios/single_page_app.png)

#### <a name="description-of-protocol-flow"></a>Beschrijving van de stroom Protocol
1. Hallo gebruiker navigeert toohello-webtoepassing.
2. Hallo-toepassing retourneert hello JavaScript-front-end (presentatie laag) toohello browser.
3. Hallo gebruiker initieert aanmelden, bijvoorbeeld door een teken in de koppeling te klikken. Hallo browser verzendt een GET toohello Azure AD autorisatie eindpunt toorequest een token ID. Deze aanvraag bevat ID en de antwoord-URL van toepassing hello Hallo queryparameters.
4. Azure AD valideert Hallo die antwoord-URL tegen Hallo geregistreerd antwoord-URL die is geconfigureerd in hello Azure-Portal.
5. Hallo-gebruiker zich aanmeldt op de aanmeldingspagina Hallo.
6. Als verificatie geslaagd is, wordt Azure AD maakt een token ID en wordt geretourneerd als antwoord-URL voor een URL-fragment (#) toohello toepassing. Voor een productietoepassing moet dit antwoord-URL HTTPS. Hallo heeft een token geretourneerd bevat claims over Hallo gebruiker en Azure AD die nodig zijn voor Hallo toepassing toovalidate Hallo token.
7. Hallo JavaScript-clientcode is uitgevoerd in de browser Hallo haalt Hallo token uit Hallo antwoord toouse in het beveiligen van eindigen terug van de toepassing toohello web-API aanroepen.
8. Hallo aanroepen Hallo browsertoepassing van web API terug eindigen met het toegangstoken Hallo in Hallo autorisatie-header.

#### <a name="code-samples"></a>Codevoorbeelden
Zie de codevoorbeelden Hallo voor scenario's met één pagina toepassing (SPA). Vaak--ervoor toocheck back worden er nieuwe samples alle Hallo tijd toevoegen. [Eén pagina toepassing (SPA)](active-directory-code-samples.md#single-page-application-spa).

#### <a name="registering"></a>Registreren
* Één Tenant: Als u een toepassing voor uw organisatie maakt, moet deze worden geregistreerd in de directory van uw bedrijf met behulp van hello Azure-Portal.
* Multitenant: Als u een toepassing die kan worden gebruikt door gebruikers buiten uw organisatie maakt, het moet worden geregistreerd in de directory van uw bedrijf, maar ook moet worden geregistreerd in elke organisatie directory die Hallo toepassing zullen gebruiken. toomake uw toepassing in de directory, kunt u een aanmeldingsproces opnemen voor uw klanten kunnen ze tooconsent tooyour toepassing. Wanneer ze zich registreren voor uw toepassing, worden ze een dialoogvenster waarin Hallo machtigingen Hallo toepassing is vereist, en vervolgens Hallo optie tooconsent weergegeven. Afhankelijk van een beheerder in Hallo Hallo vereist machtigingen andere organisatie mogelijk toogive toestemming vereist. Wanneer het Hallo-gebruiker of beheerder hiermee akkoord gaat, wordt Hallo toepassing geregistreerd in de directory. Zie voor meer informatie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).

Het moet na de registratie van de toepassing hello geconfigureerde toouse impliciete OAuth 2.0-Grant-protocol. Dit protocol is standaard uitgeschakeld voor toepassingen. tooenable hello impliciete Grant OAuth2-protocol voor uw toepassing bewerken van het toepassingsmanifest van hello Azure-Portal en Hallo 'oauth2AllowImplicitFlow' waarde tootrue instellen. Zie voor gedetailleerde instructies [inschakelen van OAuth 2.0 impliciete Grant voor toepassingen met één pagina](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Verlopen van het token
Wanneer u ADAL.js toomanage verificatie met Azure AD gebruikt, profiteert u verschillende functies die een verlopen token te vernieuwen, evenals bij het ophalen van tokens voor extra web API-resources die kunnen worden aangeroepen door de toepassing hello vergemakkelijken. Wanneer het Hallo-gebruiker is geverifieerd met Azure AD, een sessie die is beveiligd door een cookie is tot stand gebracht voor de gebruiker Hallo tussen Hallo browser en Azure AD. Het is belangrijk toonote die Hallo sessie bestaat tussen de gebruiker Hallo en Azure AD en niet tussen Hallo gebruiker en Hallo webtoepassing op Hallo-server. Wanneer een token is verlopen, ADAL.js maakt gebruik van deze sessie toosilently een ander token verkrijgen. Dit doet dit met behulp van een verborgen iFrame toosend en Hallo ontvangstverzoek met Hallo impliciete OAuth-Grant-protocol. ADAL.js kunt ook gebruiken voor hetzelfde mechanisme toosilently verkrijgen toegangstokens van Azure AD voor andere web API-bronnen of Hallo toepassing aanroepen, zolang deze resources ondersteuning voor cross-origin-resource delen (CORS) zijn geregistreerd in de map Hallo gebruiker, en eventuele vereiste toestemming is gegeven door de gebruiker Hallo tijdens het aanmelden.

### <a name="native-application-tooweb-api"></a>Systeemeigen toepassing tooWeb API
Deze sectie beschrijft een systeemeigen toepassing die namens een gebruiker een web-API aanroept. Dit scenario is gebaseerd op Hallo OAuth 2.0 autorisatie code grant type met een openbare client, zoals beschreven in de sectie 4.1 Hallo [OAuth 2.0-specificatie](http://tools.ietf.org/html/rfc6749). systeemeigen toepassing Hello verkrijgt een toegangstoken voor de gebruiker Hallo via Hallo OAuth 2.0-protocol. Deze toegangstoken wordt in Hallo aanvraag toohello web-API, die Hallo gebruiker toestaat en retourneert Hallo gewenst resource verzonden.

#### <a name="diagram"></a>Diagram
![Systeemeigen toepassing tooWeb API-Diagram](./media/active-directory-authentication-scenarios/native_app_to_web_api.png)

#### <a name="authentication-flow-for-native-application-tooapi"></a>Authenticatiestroom voor systeemeigen toepassing tooAPI
#### <a name="description-of-protocol-flow"></a>Beschrijving van de stroom Protocol
Als u van Hallo AD-Verificatiebibliotheken gebruikmaakt, worden de meeste van gegevens van het Hallo-protocol die hieronder worden beschreven, zoals Hallo browser pop-upvenster token opslaan in cache en de verwerking van het vernieuwen van tokens afgehandeld.

1. Het gebruik van een pop-browser, maakt systeemeigen toepassing hello een aanvraag toohello autorisatie-eindpunt in Azure AD. Deze aanvraag bevat Hallo toepassings-ID en Hallo omleidings-URI van de systeemeigen toepassing hello, zoals wordt weergegeven in hello Azure-Portal en Hallo toepassings-ID-URI voor Hallo web-API. Als Hallo gebruiker nog niet al bent aangemeld, zijn ze na vragen aan gebruiker toosign in opnieuw
2. Azure AD verifieert de gebruiker Hallo. Als dit een multitenant-toepassing is en toestemming vereist toouse Hallo toepassing is, worden Hallo gebruiker vereist tooconsent als ze nog niet hebt gedaan. Na het verlenen en bij de verificatie is geslaagd, wordt in Azure AD autorisatie code antwoord back toohello client van een toepassing omleidings-URI geeft.
3. Wanneer Azure AD geeft een code autorisatiereactie terug wordt toohello omleidings-URI, Hallo van client toepassing stopt browser interactie en uitgepakt Hallo autorisatiecode uit Hallo antwoord. Met deze autorisatiecode, Hallo-clienttoepassing verzendt een aanvraag tooAzure van AD token eindpunt met de autorisatiecode Hallo, details over Hallo van client-toepassing (toepassings-ID en omleidings-URI) en Hallo gewenste resource (toepassings-ID De URI voor Hallo web-API).
4. Hallo autorisatiecode en informatie over het Hallo-clienttoepassing en web-API worden gevalideerd door Azure AD. Heeft validatie is geslaagd, wordt de Azure AD twee tokens: een JWT-token voor toegang en een vernieuwingstoken JWT. Bovendien retourneert Azure AD basisinformatie over Hallo gebruiker, zoals een weergave naam en het tenant-ID.
5. Via HTTPS gebruikt de clienttoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.
6. Wanneer Hallo toegangstoken is verlopen, ontvangt de clienttoepassing Hallo een fout die aangeeft dat het Hallo-gebruiker moet tooauthenticate opnieuw. Als het Hallo-toepassing heeft een ongeldig vernieuwingstoken, kan het gebruikte tooacquire een nieuw toegangstoken zonder Hallo gebruiker toosign in opnieuw zijn. Als Hallo vernieuwingstoken is verlopen, moet toepassing hello toointeractively Hallo gebruiker één keer opnieuw worden geverifieerd.

> [!NOTE]
> Hallo vernieuwingstoken dat is uitgegeven door Azure AD kan worden gebruikt tooaccess meerdere resources. Hebt u een clienttoepassing die machtiging toocall twee web-API's heeft, kan het vernieuwingstoken Hallo gebruikte op tooget een access token toohello andere web-API ook zijn.
> 
> 

#### <a name="code-samples"></a>Codevoorbeelden
Zie de codevoorbeelden Hallo voor systeemeigen toepassing tooWeb API's. En terugkomen vaak--we alle Hallo tijd nieuwe voorbeelden toevoegen. [Systeemeigen toepassing tooWeb API](active-directory-code-samples.md#native-application-to-web-api).

#### <a name="registering"></a>Registreren
* Één Tenant: Beide systeemeigen toepassing hello en Hallo web-API moet worden geregistreerd in Hallo dezelfde directory in Azure AD. Hallo-web-API kan geconfigureerde tooexpose een reeks machtigingen die gebruikt toolimit Hallo systeemeigen van de toepassing toegang tot tooits bronnen zijn zijn. Hallo-clienttoepassing vervolgens selecteert Hallo gewenste machtigingen in Hallo 'Machtigingen tooOther toepassingen' vervolgkeuzelijst menu in hello Azure-Portal.
* Multitenant: Eerst systeemeigen toepassing hello alleen ooit geregistreerd in Hallo ontwikkelaar of uitgever directory. Ten tweede is systeemeigen toepassing hello geconfigureerde tooindicate Hallo machtigingen toobe functioneel is vereist. Deze lijst met de vereiste machtigingen wordt in een dialoogvenster weergegeven wanneer een gebruiker of beheerder in de doelmap Hallo geeft toestemming toohello toepassing, waardoor het beschikbaar tootheir organisatie. Sommige toepassingen vereisen alleen gebruikersniveau machtigingen, wat een gebruiker in de organisatie Hallo met instemmen kunt. Andere toepassingen moet beheerdersniveau machtigingen, wat een gebruiker in de organisatie Hallo kan niet met instemmen. Alleen een directory-beheerder krijgt toestemming tooapplications waarvoor dit niveau van machtigingen. Wanneer het Hallo-gebruiker of beheerder hiermee akkoord gaat, wordt alleen Hallo web-API in hun directory geregistreerd. Zie voor meer informatie [toepassingen integreren met Azure Active Directory](active-directory-integrating-applications.md).

#### <a name="token-expiration"></a>Verlopen van het token
Wanneer de systeemeigen toepassing hello de autorisatie code tooget een toegangstoken JWT gebruikt, ontvangt het ook een JWT-token voor vernieuwen. Wanneer het Hallo-toegangstoken is verlopen, Hallo vernieuwingstoken gebruikte toore zijn-Hallo gebruiker verifiëren zonder dat ze opnieuw toosign in. Dit vernieuwingstoken wordt gebruikte tooauthenticate Hallo gebruiker, waardoor het een nieuwe toegang token en vernieuw token.

### <a name="web-application-tooweb-api"></a>Web Application tooWeb API
Deze sectie beschrijft een webtoepassing die tooget bronnen van een web-API behoeften. In dit scenario wordt er zijn twee identiteitstypen die webtoepassing Hallo kunnen tooauthenticate gebruiken en Hallo web API niet aanroepen: een toepassings-id of een gedelegeerde gebruikersidentiteit.

*Toepassings-id:* deze scenario maakt gebruik van OAuth 2.0-clientreferenties tooauthenticate als toepassing hello en Hallo toegang verlenen web-API. Bij gebruik van een toepassings-id Hallo web API kan alleen detecteren Hallo-webtoepassing is, aanroepen als Hallo biedt web-API geen informatie ontvangen over Hallo-gebruiker. Hallo toepassing ontvangt informatie over Hallo gebruiker, wordt verzonden via het toepassingsprotocol Hallo als het niet is ondertekend door Azure AD. Hallo-web-API vertrouwt dat webtoepassing Hallo Hallo-gebruiker geverifieerde. Om deze reden wordt dit patroon van een vertrouwde subsysteem genoemd.

*Gedelegeerde gebruikersidentiteit:* dit scenario kan worden uitgevoerd op twee manieren: OpenID Connect en OAuth 2.0 autorisatie code grant met een vertrouwelijk client. Hallo-webtoepassing verkrijgt een toegangstoken voor Hallo gebruiker, die kan worden vastgesteld toohello web-API die webtoepassing Hallo gebruiker geverifieerd toohello en Hallo webtoepassing was kunnen tooobtain een gemachtigde gebruiker identiteit toocall Hallo-web-API. Deze toegangstoken wordt verzonden in Hallo aanvraag toohello web-API, die Hallo gebruiker toestaat en retourneert Hallo gewenst resource.

#### <a name="diagram"></a>Diagram
![Web Application tooWeb API-diagram](./media/active-directory-authentication-scenarios/web_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Beschrijving van de stroom Protocol
Beide Hallo toepassings-id en overgedragen gebruiker identiteitstypen in Hallo-stroom die hieronder worden besproken. Hallo belangrijkste verschil tussen deze twee is dat Hallo gedelegeerde gebruikersidentiteit eerst een autorisatiecode verkrijgen moet voordat Hallo-gebruiker kunt aanmelden en toegang toohello web-API krijgen.

##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>De toepassingsidentiteit met OAuth 2.0-Client referenties verlenen
1. Een gebruiker is aangemeld in tooAzure AD in Hallo-webtoepassing (Zie Hallo [webbrowser tooWeb toepassing](#web-browser-to-web-application) hierboven).
2. Hallo-webtoepassing moet een toegangstoken tooacquire zodat deze kan toohello web-API verifiëren en Hallo gewenst bron. Er wordt een aanvraag tooAzure van AD-tokeneindpunt, Hallo referentie, toepassings-ID en web-API van toepassings-ID-URI.
3. Azure AD verifieert Hallo-toepassing en een JWT-toegangstoken dat is gebruikt toocall Hallo web-API retourneert.
4. Via HTTPS gebruikt de webtoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.

##### <a name="delegated-user-identity-with-openid-connect"></a>Gedelegeerde gebruikersidentiteit met OpenID Connect
1. Een gebruiker is aangemeld in tooa-webtoepassing met behulp van Azure AD (Zie Hallo [webbrowser tooWeb toepassing](#web-browser-to-web-application) sectie hierboven). Als de gebruiker van de webtoepassing Hallo Hallo niet heeft nog ingestemd tooallowing Hallo web application toocall Hallo web-API voor zijn rekening, moet Hallo gebruiker tooconsent. Hallo-toepassing hello machtigingen die vereist worden weergegeven, en als een van deze machtigingen op administrator-niveau, een normale gebruiker in de directory Hallo tooconsent kunnen niet worden. Dit proces toestemming is alleen van toepassing toomulti-tenant toepassingen, niet één tenant toepassingen, zoals toepassing hello beschikt al over de benodigde machtigingen Hallo. Wanneer hello gebruiker aangemeld, ontvangen Hallo webtoepassing een token ID met informatie over het Hallo-gebruiker, evenals een autorisatiecode.
2. Hallo autorisatiecode uitgegeven door Azure AD, Hallo webtoepassing verzendt een aanvraag tooAzure van AD token eindpunt met de autorisatiecode Hallo gebruikt, kan informatie over de clienttoepassing hello (toepassings-ID en omleidings-URI) en Hallo gewenst resource ( aanvraag-ID-URI van Hallo web-API).
3. Hallo autorisatiecode en informatie over het Hallo-webtoepassing en web-API worden gevalideerd door Azure AD. Heeft validatie is geslaagd, wordt de Azure AD twee tokens: een JWT-token voor toegang en een vernieuwingstoken JWT.
4. Via HTTPS gebruikt de webtoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.

##### <a name="delegated-user-identity-with-oauth-20-authorization-code-grant"></a>Gedelegeerde gebruikersidentiteit met OAuth 2.0 Authorization Code Grant
1. Een gebruiker is al aangemeld in de webtoepassing tooa, waarvan verificatiemechanisme onafhankelijk van Azure AD is.
2. Hallo webtoepassing vereist een vergunning tooacquire code een toegangstoken zodat deze uitgeeft een aanvraag via Hallo browser tooAzure van AD autorisatie eindpunt, bieden Hallo toepassings-ID en omleidings-URI voor de webtoepassing Hallo na geslaagde -verificatie. Hallo-gebruiker zich aanmeldt tooAzure AD.
3. Als de gebruiker van de webtoepassing Hallo Hallo niet heeft nog ingestemd tooallowing Hallo web application toocall Hallo web-API voor zijn rekening, moet Hallo gebruiker tooconsent. Hallo-toepassing hello machtigingen die vereist worden weergegeven, en als een van deze machtigingen op administrator-niveau, een normale gebruiker in de directory Hallo tooconsent kunnen niet worden. Deze toestemming geldt tooboth één en multitenant-toepassing.  In geval van Hallo één tenant kan een beheerder admin toestemming tooconsent uitvoeren namens de gebruikers.  U kunt dit doen met behulp van Hallo `Grant Permissions` knop in Hallo [Azure Portal](https://portal.azure.com). 
4. Nadat Hallo gebruiker heeft ingestemd, ontvangt webtoepassing Hallo Hallo autorisatiecode dat het moet tooacquire een toegangstoken.
5. Hallo autorisatiecode uitgegeven door Azure AD, Hallo webtoepassing verzendt een aanvraag tooAzure van AD token eindpunt met de autorisatiecode Hallo gebruikt, kan informatie over de clienttoepassing hello (toepassings-ID en omleidings-URI) en Hallo gewenst resource ( aanvraag-ID-URI van Hallo web-API).
6. Hallo autorisatiecode en informatie over het Hallo-webtoepassing en web-API worden gevalideerd door Azure AD. Heeft validatie is geslaagd, wordt de Azure AD twee tokens: een JWT-token voor toegang en een vernieuwingstoken JWT.
7. Via HTTPS gebruikt de webtoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.

#### <a name="code-samples"></a>Codevoorbeelden
Zie de codevoorbeelden Hallo voor webtoepassing tooWeb API's. En terugkomen vaak--we alle Hallo tijd nieuwe voorbeelden toevoegen. Web [toepassing tooWeb API](active-directory-code-samples.md#web-application-to-web-api).

#### <a name="registering"></a>Registreren
* Één Tenant: Hallo voor Hallo toepassings-id en overgedragen gebruiker identiteit gevallen webtoepassing en Hallo web-API moet worden geregistreerd in Hallo dezelfde directory in Azure AD. Hallo-web-API kan worden geconfigureerd tooexpose een reeks machtigingen die tooits gebruikte toolimit Hallo van de webtoepassing openen van bronnen zijn. Als een type gedelegeerde gebruikersidentiteit wordt gebruikt, moet de webtoepassing Hallo tooselect Hallo gewenste machtigingen in Hallo 'Machtigingen tooOther toepassingen' vervolgkeuzelijst menu in hello Azure-Portal. Deze stap is niet vereist als Hallo identiteit toepassingstype wordt gebruikt.
* Multitenant: Eerst Hallo webtoepassing is geconfigureerde tooindicate Hallo machtigingen toobe functioneel is vereist. Deze lijst met de vereiste machtigingen wordt in een dialoogvenster weergegeven wanneer een gebruiker of beheerder in de doelmap Hallo geeft toestemming toohello toepassing, waardoor het beschikbaar tootheir organisatie. Sommige toepassingen vereisen alleen gebruikersniveau machtigingen, wat een gebruiker in de organisatie Hallo met instemmen kunt. Andere toepassingen moet beheerdersniveau machtigingen, wat een gebruiker in de organisatie Hallo kan niet met instemmen. Alleen een directory-beheerder krijgt toestemming tooapplications waarvoor dit niveau van machtigingen. Wanneer het Hallo-gebruiker of beheerder toestemmingen, Hallo webtoepassing toepassing en Hallo web-API worden in de directory geregistreerd.

#### <a name="token-expiration"></a>Verlopen van het token
Wanneer het Hallo-webtoepassing maakt gebruik van de autorisatie code tooget een toegangstoken JWT, ontvangt het ook een JWT-token voor vernieuwen. Wanneer het Hallo-toegangstoken is verlopen, Hallo vernieuwingstoken gebruikte toore zijn-Hallo gebruiker verifiëren zonder dat ze opnieuw toosign in. Dit vernieuwingstoken wordt gebruikte tooauthenticate Hallo gebruiker, waardoor het een nieuwe toegang token en vernieuw token.

### <a name="daemon-or-server-application-tooweb-api"></a>Daemon of servertoepassing tooWeb API
Deze sectie beschrijft een daemon of server-toepassing die tooget bronnen van een web-API behoeften. Er zijn twee onderliggende scenario's die van toepassing zijn toothis sectie: een daemon waarvoor toocall een web-API, gebaseerd op OAuth 2.0 referenties grant clienttype; en een servertoepassing (zoals een web-API) die toocall moet een web-API, gebaseerd op OAuth 2.0 On-Behalf-Of conceptspecificatie.

Voor Hallo scenario wanneer een daemontoepassing toocall een web-API moet is het belangrijk toounderstand leest. Eerst is tussenkomst van de gebruiker niet mogelijk met een daemon-toepassing waarvoor Hallo toepassing toohave een eigen identiteit vereist. Een voorbeeld van een daemontoepassing is een batch-job of een besturingssysteem-service op de achtergrond Hallo uitgevoerd. Dit type toepassing aanvragen een toegangstoken met behulp van de toepassingsidentiteit en de toepassings-ID, de referentie (wachtwoord of certificaat) en de toepassing-ID-URI tooAzure AD presenteren. Na een geslaagde authenticatie ontvangt Hallo daemon een toegangstoken van Azure AD dat zich bevindt, wordt het gebruikte toocall Hallo web-API.

Voor Hallo scenario wanneer een servertoepassing toocall een web-API moet, is het handig toouse een voorbeeld. Stel dat een gebruiker heeft geverifieerd op een systeemeigen toepassing en deze systeemeigen toepassing toocall een web-API moet. Azure AD geeft een JWT access token toocall Hallo-web-API. Als Hallo web-API toocall een andere downstream web-API moet, kan het Hallo op namens-stroom toodelegate Hallo gebruikers id gebruiken en zich verifiëren toohello tweede laag web-API.

#### <a name="diagram"></a>Diagram
![Daemon of servertoepassing tooWeb API-diagram](./media/active-directory-authentication-scenarios/daemon_server_app_to_web_api.png)

#### <a name="description-of-protocol-flow"></a>Beschrijving van de stroom Protocol
##### <a name="application-identity-with-oauth-20-client-credentials-grant"></a>De toepassingsidentiteit met OAuth 2.0-Client referenties verlenen
1. Eerst moet de servertoepassing Hallo tooauthenticate met Azure AD als zelf, zonder menselijke tussenkomst zoals een dialoogvenster voor interactieve aanmelding. Er wordt een aanvraag tooAzure van AD-tokeneindpunt, Hallo referentie, toepassings-ID en toepassings-ID-URI.
2. Azure AD verifieert Hallo-toepassing en een JWT-toegangstoken dat is gebruikt toocall Hallo web-API retourneert.
3. Via HTTPS gebruikt de webtoepassing Hallo Hallo JWT access token tooadd hello JWT-tekenreeks met een aanduiding 'Bearer' geretourneerd als Hallo autorisatie-header van Hallo aanvraag toohello web-API. Hallo-web-API valideert vervolgens Hallo JWT-token en als validatie geslaagd is, retourneert Hallo resource gewenst.

##### <a name="delegated-user-identity-with-oauth-20-on-behalf-of-draft-specification"></a>Gedelegeerde gebruikersidentiteit met OAuth 2.0-op-andere gebruikers-Of-concept-specificatie
Hallo-stroom hieronder besproken wordt ervan uitgegaan dat een gebruiker is geverifieerd op een andere toepassing (zoals een systeemeigen toepassing) en de identiteit van de gebruiker is gebruikte tooacquire een access token toohello eerste laag web-API.

1. systeemeigen toepassing Hello verzendt Hallo access token toohello eerste laag web API.
2. Hallo eerste laag web-API verzendt een aanvraag tooAzure van AD-tokeneindpunt, bieden de toepassings-ID en referenties, evenals toegangstoken van Hallo gebruiker. Bovendien Hallo-aanvraag is verzonden met een on_behalf_of parameter die Hallo aangeeft web API een nieuwe vraagt toocall een downstream web-API namens de oorspronkelijke gebruiker Hallo tokens.
3. Azure AD verifieert dat Hallo eerste laag web API heeft machtigingen tooaccess Hallo tweede laag web-API en valideert Hallo-aanvraag retourneren van een JWT-token voor toegang en een JWT-token toohello eerste laag web-API vernieuwen.
4. Via HTTPS Hallo Hallo eerste laag web API roept vervolgens tweede laag web-API door token Hallo-reeks in Hallo autorisatie-header in Hallo aanvraag toe te voegen. Hallo eerste laag web-API kan zolang toocall Hallo tweede laag web-API Hallo-toegangstoken en vernieuwen van tokens geldig zijn.

#### <a name="code-samples"></a>Codevoorbeelden
Zie Hallo codevoorbeelden voor Daemon of servertoepassing tooWeb API-scenario's. En terugkomen vaak--we alle Hallo tijd nieuwe voorbeelden toevoegen. [Server of toepassing Daemon tooWeb API](active-directory-code-samples.md#server-or-daemon-application-to-web-api)

#### <a name="registering"></a>Registreren
* Één Tenant: Voor Hallo toepassings-id en overgedragen gebruiker identiteit gevallen Hallo daemon of server-toepassing moet zijn geregistreerd in Hallo dezelfde directory in Azure AD. Hallo-web-API kan worden geconfigureerd tooexpose een reeks machtigingen die gebruikt toolimit Hallo daemon of toegang tooits serverbronnen zijn. Als een type gedelegeerde gebruikersidentiteit wordt gebruikt, moet de servertoepassing Hallo tooselect Hallo gewenste machtigingen in Hallo 'Machtigingen tooOther toepassingen' vervolgkeuzelijst menu in hello Azure-Portal. Deze stap is niet vereist als Hallo identiteit toepassingstype wordt gebruikt.
* Multitenant: Eerst Hallo daemon of servertoepassing is geconfigureerde tooindicate Hallo machtigingen toobe functioneel is vereist. Deze lijst met de vereiste machtigingen wordt in een dialoogvenster weergegeven wanneer een gebruiker of beheerder in de doelmap Hallo geeft toestemming toohello toepassing, waardoor het beschikbaar tootheir organisatie. Sommige toepassingen vereisen alleen gebruikersniveau machtigingen, wat een gebruiker in de organisatie Hallo met instemmen kunt. Andere toepassingen moet beheerdersniveau machtigingen, wat een gebruiker in de organisatie Hallo kan niet met instemmen. Alleen een directory-beheerder krijgt toestemming tooapplications waarvoor dit niveau van machtigingen. Wanneer Hallo gebruiker of beheerder hiermee akkoord gaat, worden beide Hallo web-API's in hun directory geregistreerd.

#### <a name="token-expiration"></a>Verlopen van het token
Wanneer de eerste toepassing hello de autorisatie code tooget een toegangstoken JWT gebruikt, ontvangt het ook een JWT-token voor vernieuwen. Wanneer het Hallo-toegangstoken is verlopen, Hallo vernieuwingstoken gebruikte toore zijn-Hallo gebruiker verifiëren zonder te vragen om referenties. Dit vernieuwingstoken wordt gebruikte tooauthenticate Hallo gebruiker, waardoor het een nieuwe toegang token en vernieuw token.

## <a name="see-also"></a>Zie ook
[Ontwikkelaarshandleiding Azure Active Directory](active-directory-developers-guide.md)

[Azure Active Directory-codevoorbeelden](active-directory-code-samples.md)

[Belangrijke informatie over het ondertekenen van sleutelrollover in Azure AD](active-directory-signing-key-rollover.md)

[OAuth 2.0 in Azure AD](https://msdn.microsoft.com/library/azure/dn645545.aspx)

