---
title: aaaHow toobuild een app waarvoor Azure AD-gebruiker kunt aanmelden | Microsoft Docs
description: Stapsgewijze instructies voor het ontwikkelen van een toepassing die kunnen Meld u aan een gebruiker van een Azure Active Directory-tenant, ook wel bekend als een multitenant-toepassing.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 35af95cb-ced3-46ad-b01d-5d2f6fd064a3
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/26/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: 123ea8125fa3c308ce0f124cc58e85ec28d476d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosign-in-any-azure-active-directory-ad-user-using-hello-multi-tenant-application-pattern"></a>Hoe toosign aan alle Azure Active Directory (AD) gebruiker met Hallo patroon toepassing met meerdere tenants
Als u een Software als een Service-toepassing toomany organisaties bieden, kunt u uw toepassing tooaccept aanmeldingen vanaf elke Azure AD-tenant kunt configureren.  Dit heet in Azure AD maken van uw toepassing meerdere tenants.  Gebruikers in een Azure AD-tenant zich kunnen toosign in tooyour toepassing na ermee akkoord dat toouse voor hun rekening met uw toepassing.  

Als er een bestaande toepassing die heeft een eigen accountsysteem of andere vormen van de aanmeldingspagina van andere cloudproviders ondersteunt, is toe te voegen Azure AD aanmelden van een tenant eenvoudig. Uw app registreren, aanmelden code via OAuth2, OpenID Connect of SAML toevoegen en een knop 'Aanmelding In met Microsoft' zijn ingesteld voor uw toepassing. Klik op volgende knop toolearn meer over de huisstijl van uw toepassing hello.

[! [Knop aanmelden] [AAD-aanmeldingspagina]][AAD-App-Branding]

In dit artikel wordt ervan uitgegaan dat u al bekend bent met het bouwen van een toepassing voor één tenant voor Azure AD.  Als u niet bent, head back-up toohello [developer guide startpagina] [ AAD-Dev-Guide] en probeer een van onze snel aan de slag!

Er zijn vier eenvoudige stappen tooconvert van uw toepassing in een Azure AD-multitenant-app:

1. Bijwerken van uw toepassing registratie toobe meerdere tenants
2. Werk uw code toosend aanvragen toohello/Common eindpunt 
3. Werk uw code toohandle meerdere verlener waarden
4. Gebruikers- en -beheerder toestemming begrijpen en geschikte codewijzigingen aanbrengen

Bekijk elke stap in detail. U kunt ook direct door te gaan[deze lijst met voorbeelden van meerdere tenants][AAD-Samples-MT].

## <a name="update-registration-toobe-multi-tenant"></a>Registratie toobe multitenant bijwerken
Web-app/API registraties in Azure AD zijn standaard één tenant.  U kunt uw inschrijving multitenant maken door het zoeken Hallo 'meerdere verpachte' overschakelen op de eigenschappenpagina Hallo van uw toepassing registreren in Hallo [Azure-portal] [ AZURE-portal] en te 'Ja' instellen.

Vergeet niet, voordat een toepassing kan worden gemaakt op meerdere tenants Azure AD vereist Hallo App ID URI van Hallo toepassing toobe globaal uniek zijn. Hallo App ID URI is Hallo manieren die een toepassing in protocolberichten wordt geïdentificeerd.  Voor een toepassing voor één tenant is het voldoende voor Hallo App ID URI toobe uniek zijn binnen deze tenant.  Voor een toepassing met meerdere tenants moet het wereldwijd uniek zodat Azure AD-toepassing hello over alle huurders kan vinden.  Globale uniekheid wordt afgedwongen door te vereisen Hallo App ID URI toohave een host-naam die overeenkomt met een geverifieerde domein voor hello Azure AD-tenant.  Bijvoorbeeld, als Hallo-naam van uw tenant contoso.onmicrosoft.com en vervolgens een geldig is App-ID-URI zou zijn `https://contoso.onmicrosoft.com/myapp`.  Als uw tenant had een geverifieerde domein voor `contoso.com`, moet een geldige App ID URI zou ook `https://contoso.com/myapp`.  Instellen van een toepassing als multitenant mislukt als Hallo App ID URI niet dit patroon volgen.

Native clientregistraties zijn multitenant standaard.  U hoeft niet tootake elke actie toomake een native client application registration meerdere tenants.

## <a name="update-your-code-toosend-requests-toocommon"></a>Uw code toosend aanvragen te gemeenschappelijke bijwerken
In een toepassing één tenant aanmeldingsaanvragen toohello-tenant aanmelden eindpunt verzonden. Voor contoso.onmicrosoft.com kan Hallo eindpunt zou zijn:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

Aanvragen verzonden tooa-tenant-eindpunt kunt aanmelden gebruikers (of gasten) in die tooapplications tenant in deze tenant.  Met een multitenant-toepassing hello toepassing niet weet wat tenant Hallo-gebruiker is, zodat u kunt geen verzenden aanvragen vooraf tooa-tenant-eindpunt.  Aanvragen verzonden in plaats daarvan tooan-eindpunt dat multiplexes over alle Azure AD-tenants:

    https://login.microsoftonline.com/common

Azure AD ontvangt wanneer een aanvraag op Hallo/gemeenschappelijk eindpunt het Hallo-gebruiker zich aanmeldt en als gevolg welke tenant Hallo gebruiker detecteert uit.  Hallo/gemeenschappelijk eindpunt werkt met alle Hallo verificatieprotocollen ondersteund door Azure AD: OpenID Connect, OAuth 2.0 SAML 2.0 en WS-Federation.

Hallo aanmelden antwoord toohello toepassing vervolgens bevat een token dat Hallo gebruiker voorstelt.  Hallo verlener waarde in Hallo token Hiermee geeft u een toepassing wat Hallo huurder gebruiker afkomstig is van.  Wanneer een antwoord geretourneerd van Hallo-gemeenschappelijk eindpunt, Hallo verlener waarde in Hallo-token van de gebruiker toohello tenant overeen.  Het is belangrijk toonote Hallo/gemeenschappelijk eindpunt is niet een tenant en is niet een verlener en is alleen een multiplexer.  Wanneer u/Common, moet Hallo logica in uw toepassing toovalidate tokens toobe bijgewerkt tootake dit in aanmerking. 

Zoals eerder vermeld, multitenant-toepassingen ook een consistente ervaring voor aanmelding voor gebruikers bieden moeten, Hallo volgende huisstijl richtlijnen voor Azure AD-toepassing. Klik op volgende knop toolearn meer over de huisstijl van uw toepassing hello.

[! [Knop aanmelden] [AAD-aanmeldingspagina]][AAD-App-Branding]

Laten we bij het gebruik van Hallo/Common Hallo eindpunt en de implementatie van uw code in meer detail.

## <a name="update-your-code-toohandle-multiple-issuer-values"></a>Werk uw code toohandle meerdere verlener waarden
Webtoepassingen en web-API's ontvangen en valideren van tokens van Azure AD.  

> [!NOTE]
> Hoewel systeemeigen clienttoepassingen aanvragen en tokens van Azure AD ontvangen, ze in dat geval toosend doen ze tooAPIs, waar ze worden gevalideerd.  Systeemeigen toepassingen tokens wordt niet gevalideerd en moeten ze behandelen als ondoorzichtige.
> 
> 

We bekijken op hoe een toepassing tokens valideert het ontvangt van Azure AD.  Een toepassing voor één tenant duurt normaal gesproken een endpoint-waarde, zoals:

    https://login.microsoftonline.com/contoso.onmicrosoft.com

en gebruik deze tooconstruct, zoals een metagegevens-URL (in dit geval OpenID Connect):

    https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration

toodownload twee kritieke stukjes informatie die gebruikt toovalidate tokens zijn: Hallo tenant het ondertekenen van sleutels en waarde van de verlener.  Elke Azure AD-tenant heeft de waarde van een unieke verlener Hallo vorm:

    https://sts.windows.net/31537af4-6d77-4bb9-a681-d2394888ea26/

Hallo GUID-waarde is waar Hallo rename-safe versie van de tenant-ID van de tenant Hallo Hallo.  Als je op Hallo voorafgaand aan de metagegevens van de koppeling voor `contoso.onmicrosoft.com`, kunt u deze waarde van de verlener in Hallo document bekijken.

Als een toepassing voor één tenant een token valideert, controleert deze Hallo handtekening van Hallo token tegen Hallo ondertekeningssleutels uit Hallo metagegevensdocument. Hierdoor kunnen deze toomake ervoor Hallo verlener waarde in Hallo token komt overeen met Hallo een die is gevonden in het document Hallo-metagegevens.

Sinds Hallo/algemene wordt eindpunt tooa tenant komt niet overeen en een verlener niet wanneer u bekijkt hello verlener waarde in Hallo-metagegevens voor/algemene hieraan een sjablonen URL in plaats van een werkelijke waarde:

    https://sts.windows.net/{tenantid}/

Daarom een multitenant-toepassing kan niet worden gevalideerd tokens door die overeenkomt met de Hallo verlener waarde in de metagegevens Hallo Hello `issuer` waarde in het Hallo-token.  Een toepassing met meerdere tenants logica toodecide welke verlener waarden geldig zijn en zijn niet nodig, op basis van Hallo tenant-id-gedeelte van Hallo verlener waarde.  

Bijvoorbeeld, als een multitenant-toepassing alleen kunt aanmelden van specifieke tenants die zich hebben geregistreerd voor de service, vervolgens deze moet controleren Hallo verlener waarde of Hallo `tid` claimwaarde in Hallo token toomake ervoor dat de tenant is in de lijst met abonnees.  Als een multitenant-toepassing alleen omgaat met personen niet beslissingen eventuele toegang op basis van tenants, vervolgens kan worden genegeerd Hallo verlener waarde kan worden overgeslagen.

In de voorbeelden van meerdere tenants Hallo in Hallo [verwante inhoud](#related-content) sectie aan Hallo einde van dit artikel wordt de verlener validatie is uitgeschakeld tooenable elke Azure AD-tenant toosign in.

Nu we bekijken Hallo gebruikerservaring voor gebruikers die in toepassingen met toomulti-tenant aanmeldt zich.

## <a name="understanding-user-and-admin-consent"></a>Wat gebruikers- en toestemming van de beheerder
Voor een gebruiker toosign in tooan toepassing in Azure AD, moet de toepassing hello worden weergegeven in van de gebruiker van het Hallo-tenant.  Hierdoor kunnen toodo zoiets als unieke beleidsregels toepassen wanneer gebruikers vanaf hun tenant zich toohello toepassing hello organisatie.  Voor een toepassing voor één tenant is deze registratie eenvoudig; Dit is een die optreedt wanneer u Hallo toepassing in Hallo registreren Hallo [Azure-portal][AZURE-portal].

Voor een multitenant-toepassing woont hello initiële registratie voor de toepassing hello in hello Azure AD-tenant die wordt gebruikt door de ontwikkelaar Hallo.  Wanneer een gebruiker van een andere tenant zich aanmeldt toohello-toepassing voor Hallo eerst, Azure AD wordt gevraagd deze tooconsent toohello machtigingen door de toepassing hello is aangevraagd.  Als ze toestemming geeft, wordt een weergave van de toepassing hello aangeroepen een *service-principal* in wordt gemaakt van gebruiker tenant Hallo en aanmelden kan worden voortgezet. Een overdracht wordt ook in Hallo-map die u Hallo van de gebruiker toestemming toohello toepassing registreert gemaakt. Zie [toepassingsobjecten en Service-Principal objecten] [ AAD-App-SP-Objects] voor meer informatie over van de toepassing hello toepassings- en ServicePrincipal objecten en hun relatie tooeach andere.

![Toestemming toosingle laag app][Consent-Single-Tier] 

Deze ervaring toestemming wordt beïnvloed door het Hallo-machtigingen die zijn aangevraagd door toepassing hello.  Azure AD ondersteunt twee soorten app alleen-lezen en gedelegeerde machtigingen:

* Een gedelegeerde machtigingen verleent een toepassing hello mogelijkheid tooact als een aangemelde gebruiker voor een subset van Hallo dingen Hallo gebruiker kunt doen.  U kunt bijvoorbeeld een toepassing hello gedelegeerde machtigingen tooread Hallo ondertekend in de agenda gebruiker verlenen.
* Een app alleen-lezen-machtiging verleend rechtstreeks toohello identiteit van de toepassing hello.  U kunt bijvoorbeeld een toepassing hello app alleen-lezen tooread Hallo lijst met machtigingen van gebruikers in een tenant, ongeacht wie is ondertekend in toohello toepassing verlenen.

Sommige machtigingen mag instemming tooby een gewone gebruiker, terwijl andere gebruikers toestemming van de tenantbeheerder vereisen. 

### <a name="admin-consent"></a>Beheerder toestemming
Machtigingen voor alleen-App moeten altijd toestemming van de tenantbeheerder.  Als uw toepassing een machtiging app alleen worden aangevraagd en een gebruiker toosign in toohello toepassing probeert, wordt een foutbericht weergegeven Hallo gebruiker kunnen tooconsent wordt niet weergegeven.

Bepaalde gedelegeerde machtigingen, ook verplichten toestemming van de tenantbeheerder.  Bijvoorbeeld, nodig Hallo mogelijkheid toowrite back tooAzure AD als een gebruiker aangemeld Hallo toestemming om een tenantbeheerder.  Net als de app alleen-lezen-machtigingen als een gewone gebruiker probeert toosign in tooan-toepassing waarin een gedelegeerde machtiging die beheerder-toestemming nodig om wordt uw toepassing een foutbericht.  Een machtiging vereist of admin toestemming wordt bepaald door Hallo-ontwikkelaar die Hallo resource gepubliceerd en kan worden gevonden in het Hallo-documentatie voor Hallo resource.  Koppelingen beschrijven Hallo beschikbare machtigingen voor hello Azure AD Graph API en Microsoft Graph API in Hallo zijn tootopics [verwante inhoud](#related-content) sectie van dit artikel.

Als uw toepassing machtigingen waarvoor u toestemming van de beheerder worden gebruikt, moet u toohave een gebaar zoals een knop of de koppeling waar Hallo beheerder Hallo actie kan initiëren.  uw toepassing verzonden voor deze actie is een gebruikelijke OAuth2/OpenID Connect autorisatieaanvraag, maar die omvat ook Hallo Hallo-aanvraag `prompt=admin_consent` querytekenreeksparameter.  Zodra de Hallo beheerder heeft ingestemd en Hallo service-principal in van de klant Hallo tenant wordt gemaakt, volgende aanmelden aanvragen hoeft geen Hallo `prompt=admin_consent` parameter. Aangezien Hallo beheerder heeft besloten Hallo aangevraagd machtigingen worden geaccepteerd, wordt er geen andere gebruikers in uw tenant Hallo gevraagd toestemming vanaf dat moment.

Hallo `prompt=admin_consent` parameter kan ook worden gebruikt door toepassingen die machtigingen die niet te worden admin toestemming hoeven te vragen. Dit gebeurt wanneer de toepassing hello vereist een ervaring waar tenantbeheerder Hallo 'aanmeldt' een tijdstip en wordt geen enkele andere gebruikers om toestemming wordt gevraagd vanaf dat moment op.

Als beheerder toestemming nodig om een toepassing en een beheerder zich bij, maar hello aanmeldt `prompt=admin_consent` parameter niet is verzonden, Hallo beheerder wordt met succes toohello toepassing toestemming **alleen voor hun gebruikersaccount**.  Gewone gebruikers zich nog steeds niet kan toosign in en toestemming toohello toepassing.  Dit is handig als u wilt toogive hello tenant administrator Hallo mogelijkheid tooexplore van uw toepassing voordat u andere gebruikers toegang toestaat.

Een tenantbeheerder kan Hallo mogelijkheid voor reguliere gebruikers tooconsent tooapplications uitschakelen.  Als deze mogelijkheid is uitgeschakeld, is altijd admin toestemming vereist voor Hallo toepassing toobe is ingesteld in het Hallo-tenant.  Als u wilt dat uw toepassing met toestemming van de normale gebruiker uitgeschakeld tootest, kunt u vinden Hallo configuratieswitch in hello Azure AD-tenant configuratiesectie Hallo [Azure-portal][AZURE-portal].

> [!NOTE]
> Sommige toepassingen kunnen een ervaring waar reguliere gebruikers kunnen tooconsent in eerste instantie en hoger Hallo-toepassing kan betrekking hebben op Hallo beheerder en machtigingen voor aanvragen die toestemming van de beheerder vereisen.  Er is geen toodo manier dit met een enkele toepassing registreren in Azure AD vandaag.  Hallo toekomstige Azure AD-v2-eindpunt kunt toepassingen toorequest machtigingen tijdens runtime, in plaats van tijdens registratie, waarmee u dit scenario.  Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor Azure AD App Model v2][AAD-V2-Dev-Guide].
> 
> 

### <a name="consent-and-multi-tier-applications"></a>Toepassingen toestemming en meerdere lagen
Uw toepassing heeft mogelijk meerdere lagen, elk vertegenwoordigd door een eigen registratie in Azure AD.  Bijvoorbeeld: een systeemeigen toepassing die een web-API aanroept of een webtoepassing die een web-API aanroept.  In beide gevallen vraagt Hallo-client (systeemeigen app of web-app) machtigingen toocall Hallo resource (web-API).  Voor Hallo client toobe ingestemd is in een klant tenant, worden alle resources toowhich vraagt deze machtigingen moet al bestaan in van de klant Hallo-tenant.  Als dit probleem niet wordt voldaan, retourneert Azure AD een fout die resource Hallo moet eerst worden toegevoegd.

**Meerdere lagen in een enkel tenant**

Dit kan een probleem zijn als uw logische toepassing uit twee of meer toepassing registraties, bijvoorbeeld een afzonderlijke client en een resource bestaat.  Hoe krijg u Hallo resource in Hallo klant tenant eerste?  In dit geval doordat de client heeft betrekking op Azure AD en resource toobe ingestemd in één stap. Hallo gebruiker ziet totaal Hallo Hallo machtigingen die zijn aangevraagd door zowel de Hallo client als de resource op Hallo toestemming pagina.  tooenable dit gedrag van de bron van het Hallo-toepassing registreren vergezeld van Hallo client App-ID als een `knownClientApplications` in het toepassingsmanifest.  Bijvoorbeeld:

    knownClientApplications": ["94da0930-763f-45c7-8d26-04d5938baab2"]

Deze eigenschap kan worden bijgewerkt via de Hallo resource [van toepassingsmanifest][AAD-App-Manifest]. Dit wordt geïllustreerd in een meerlaagse native client voorbeeld-web-API aanroepen in Hallo [verwante inhoud](#related-content) sectie op Hallo einde van dit artikel. Hallo biedt volgende diagram een overzicht van toestemming voor een app met meerdere lagen geregistreerd in een enkel tenant:

![Toestemming geven toomulti laag bekende client-app][Consent-Multi-Tier-Known-Client] 

**Meerdere lagen in meerdere tenants**

Een vergelijkbaar aanvraag gebeurt er als Hallo verschillende lagen van een toepassing in verschillende tenants zijn geregistreerd.  Denk bijvoorbeeld Hallo-aanvraag van het bouwen van een systeemeigen clienttoepassing die Hallo Office 365 Exchange Online-API aanroept.  toodevelop hello native toepassing en hoger voor Hallo systeemeigen toepassing toorun in een klant-tenant, Hallo Exchange Online service-principal moet aanwezig zijn.  In dit geval moeten hello ontwikkelaar en de klant aanschaffen Exchange Online voor Hallo service principal toobe gemaakt in hun tenants.  

In geval van een API gebouwd door een organisatie dan Microsoft hello moet Hallo developer Hallo API tooprovide een manier voor hun klanten tooconsent Hallo-toepassing in hun klanten tenants. Hallo aanbevolen ontwerp voor Hallo 3e partij developer toobuild Hallo API zodanig is dat ook als een registratie web client tooimplement fungeren kan:

1. Ga als volgt Hallo eerdere secties tooensure Hallo API implementeert Hallo multitenant toepassingsvereisten registratiecode /
2. Bovendien tooexposing Hallo van API-scopes en-rollen, Controleer Hallo registratie bevat Hallo ' aanmelden en gebruikersprofiel lezen ' Azure AD-machtiging (die standaard)
3. Een sign-in/sign-up-to-date pagina implementeren in Hallo webclient, Hallo na [admin toestemming](#admin-consent) richtlijnen besproken. 
4. Zodra het Hallo-gebruiker akkoord gaat toohello toepassing, hello service principal en toestemming delegering koppelingen worden gemaakt in de tenant en systeemeigen toepassing hello tokens voor Hallo API kan ophalen

Hallo volgende diagram biedt een overzicht van toestemming voor een app met meerdere lagen geregistreerd in verschillende tenants:

![Toestemming toomulti lagen met meerdere partijen app][Consent-Multi-Tier-Multi-Party] 

### <a name="revoking-consent"></a>Toestemming intrekken
Gebruikers en beheerders kunnen toestemming tooyour toepassing op elk gewenst moment intrekken:

* Gebruikers in te trekken toegang tooindividual toepassingen door het verwijderen van hun [toegang Configuratiescherm toepassingen] [ AAD-Access-Panel] lijst.
* Beheerders tooapplications toegang intrekken door deze te verwijderen van Azure AD dat gebruikmaakt van hello Azure AD-sectie in management Hallo [Azure-portal][AZURE-portal].

Als een beheerder tooan-toepassing voor alle gebruikers in een tenant instemt, intrekken niet gebruikers afzonderlijk toegang.  Alleen Hallo beheerder toegang kan intrekken en alleen voor de hele toepassing hello.

### <a name="consent-and-protocol-support"></a>Toestemming en protocolondersteuning
Toestemming wordt ondersteund in Azure AD via Hallo OAuth, OpenID Connect, WS-Federation en SAML-protocollen.  Hallo SAML- en WS-Federation-protocollen ondersteunen geen Hallo `prompt=admin_consent` parameter, zodat de beheerder toestemming is alleen mogelijk via OAuth en OpenID Connect.

## <a name="multi-tenant-applications-and-caching-access-tokens"></a>Multitenant-toepassingen en toegangstokens-Caching
Multitenant-toepassingen kunnen ook toegang tokens toocall API's die zijn beveiligd door Azure AD ophalen.  Een veelvoorkomende fout bij het gebruik van Hallo Active Directory Authentication Library (ADAL) met een multitenant-toepassing is tooinitially aanvraag een token voor een gebruiker die met/Common, reactie ontvangen en vervolgens een daaropvolgende token voor de gebruiker ook met/Common aanvragen.  Omdat het antwoord van Azure AD Hallo afkomstig is van een tenant niet-algemene, ADAL Hallo token afkomstig is van Hallo tenant in de cache opslaat. Hallo volgende aanroepen te gemeenschappelijke tooget een toegangstoken voor Hallo gebruiker missers Hallo-cachevermelding en Hallo gebruiker is na vragen aan gebruiker toosign in het opnieuw.  Zorg ervoor dat volgende aanroepen voor een gebruiker al aangemeld bestaan tooavoid ontbrekende Hallo cache, toohello-tenant-eindpunt.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toobuild een toepassing die een gebruiker van een Azure Active Directory-tenant kunt aanmelden. Na het inschakelen van eenmalige aanmelding tussen uw app en Azure Active Directory, kunt u ook uw toepassing tooaccess API's die worden weergegeven door de Microsoft-bronnen, zoals Office 365 bijwerken. U kunt een persoonlijke ervaring dus aanbieden in uw toepassing bijvoorbeeld contextuele informatie toohello gebruikers, zoals hun profielfoto of hun volgende afspraak voor de kalender weergegeven. toolearn meer informatie over het maken van API-aanroepen tooAzure Active Directory en Office 365-services zoals Exchange, SharePoint, OneDrive, OneNote, planning, aan Excel en meer, gaat u naar: [Microsoft Graph API][MSFT-Graph-overview].


## <a name="related-content"></a>Gerelateerde inhoud
* [Voorbeelden van multitenant-toepassing][AAD-Samples-MT]
* [Huisstijlrichtlijnen voor toepassingen][AAD-App-Branding]
* [Handleiding voor Azure AD-ontwikkelaars][AAD-Dev-Guide]
* [Toepassingsobjecten en Service-Principal-objecten][AAD-App-SP-Objects]
* [Toepassingen integreren met Azure Active Directory][AAD-Integrating-Apps]
* [Overzicht van Hallo Framework toestemming geven][AAD-Consent-Overview]
* [Microsoft Graph API-Machtigingsbereiken][MSFT-Graph-permision-scopes]
* [Azure AD Graph API-Machtigingsbereiken][AAD-Graph-Perm-Scopes]

Gebruik Hallo opmerkingen sectie tooprovide feedback te volgen en help ons verfijnen en onze content vorm.

<!--Reference style links IN USE -->
[AAD-Access-Panel]:  https://myapps.microsoft.com
[AAD-App-Branding]: ./active-directory-branding-guidelines.md
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Consent-Overview]: ./active-directory-integrating-applications.md#overview-of-the-consent-framework
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Overview]: https://azure.microsoft.com/en-us/documentation/articles/active-directory-graph-api/
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Samples-MT]: https://azure.microsoft.com/documentation/samples/?service=active-directory&term=multitenant
[AAD-Why-To-Integrate]: ./active-directory-how-to-integrate.md
[AZURE-portal]: https://portal.azure.com
[MSFT-Graph-overview]: https://graph.microsoft.io/en-us/docs/overview/overview
[MSFT-Graph-permision-scopes]: https://graph.microsoft.io/en-us/docs/authorization/permission_scopes

<!--Image references-->
[AAD-Sign-In]: ./media/active-directory-devhowto-multi-tenant-overview/sign-in-with-microsoft-light.png
[Consent-Single-Tier]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-single-tier.png
[Consent-Multi-Tier-Known-Client]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-known-clients.png
[Consent-Multi-Tier-Multi-Party]: ./media/active-directory-devhowto-multi-tenant-overview/consent-flow-multi-tier-multi-party.png

<!--Reference style links -->
[AAD-App-Manifest]: ./active-directory-application-manifest.md
[AAD-App-SP-Objects]: ./active-directory-application-objects.md
[AAD-Auth-Scenarios]: ./active-directory-authentication-scenarios.md
[AAD-Integrating-Apps]: ./active-directory-integrating-applications.md
[AAD-Dev-Guide]: ./active-directory-developers-guide.md
[AAD-Graph-Perm-Scopes]: https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AAD-Graph-User-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity
[AAD-How-To-Integrate]: ./active-directory-how-to-integrate.md
[AAD-Security-Token-Claims]: ./active-directory-authentication-scenarios/#claims-in-azure-ad-security-tokens
[AAD-Tokens-Claims]: ./active-directory-token-and-claims.md
[AAD-V2-Dev-Guide]: ../active-directory-appmodel-v2-overview.md
[AZURE-portal]: https://portal.azure.com
[Duyshant-Role-Blog]: http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/
[JWT]: https://tools.ietf.org/html/draft-ietf-oauth-json-web-token-32
[O365-Perm-Ref]: https://msdn.microsoft.com/en-us/office/office365/howto/application-manifest
[OAuth2-Access-Token-Scopes]: https://tools.ietf.org/html/rfc6749#section-3.3
[OAuth2-AuthZ-Code-Grant-Flow]: https://msdn.microsoft.com/library/azure/dn645542.aspx
[OAuth2-AuthZ-Grant-Types]: https://tools.ietf.org/html/rfc6749#section-1.3 
[OAuth2-Client-Types]: https://tools.ietf.org/html/rfc6749#section-2.1
[OAuth2-Role-Def]: https://tools.ietf.org/html/rfc6749#page-6
[OpenIDConnect]: http://openid.net/specs/openid-connect-core-1_0.html
[OpenIDConnect-ID-Token]: http://openid.net/specs/openid-connect-core-1_0.html#IDToken














