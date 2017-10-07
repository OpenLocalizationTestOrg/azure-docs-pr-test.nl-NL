---
title: aaaDeveloper richtlijnen voor Azure Active Directory voorwaardelijke toegang | Microsoft Docs
description: Handleiding voor ontwikkelaars en scenario's voor voorwaardelijke toegang van Azure AD
services: active-directory
keywords: 
author: danieldobalian
manager: mbaldwin
editor: PatAltimore
ms.author: dadobali
ms.date: 07/19/2017
ms.assetid: 115bdab2-e1fd-4403-ac15-d4195e24ac95
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.openlocfilehash: 589393f5d084d64872b372d895dc889f300592bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="developer-guidance-for-azure-active-directory-conditional-access"></a>Handleiding voor ontwikkelaars voor voorwaardelijke toegang van Azure Active Directory

Azure Active Directory (AD) biedt verschillende manieren toosecure uw app en beveiligen van een service.  Een van deze unieke functies is voorwaardelijke toegang.  Voorwaardelijke toegang kan ontwikkelaars en enterprise-klanten tooprotect services in een groot aantal manieren:

* Multi-Factor Authentication
* Zodat alleen Intune ingeschreven apparaten tooaccess specifieke services
* Beperken van de gebruikerslocaties en IP-adresbereiken

Zie voor meer informatie over de volledige functionaliteit Hallo van voorwaardelijke toegang [voorwaardelijke toegang in de klassieke Azure-portal Hallo](../active-directory-conditional-access.md). 

In dit artikel richten we op wat voorwaardelijke toegang toodevelopers apps bouwen voor Azure AD betekent.  Er wordt vanuit gegaan kennis van [één](active-directory-integrating-applications.md) en [multitenant](active-directory-devhowto-multi-tenant-overview.md) apps en [algemene patronen voor verificatie](active-directory-authentication-scenarios.md).

We je Duik in Hallo impact van de toegang tot resources die u hebt geen controle over waarvoor beleid voor voorwaardelijke toegang toegepast.  Bovendien verkennen we Hallo implicaties van voorwaardelijke toegang in Hallo op namens-stroom, web-apps, toegang tot Microsoft Graph hello, en het aanroepen van API's.

## <a name="how-does-conditional-access-impact-an-app"></a>Hoe beïnvloedt voorwaardelijke toegang tot een app

### <a name="app-topologies-impacted"></a>App-topologieën beïnvloed

In de meest voorkomende gevallen voorwaardelijke toegang wordt het gedrag van een app niet gewijzigd of eventuele wijzigingen van de ontwikkelaar Hallo vereist.  Alleen in bepaalde gevallen wanneer een app, indirect of op de achtergrond een token voor een service vraagt vereist een app code wijzigt toohandle voorwaardelijke toegang 'uitdagingen'.  Het is mogelijk net zo eenvoudig als het uitvoeren van een aanvraag voor interactief aanmelden. 

In het bijzonder vereisen hello volgende scenario's code toohandle voorwaardelijke toegang 'uitdagingen': 

* Toegang tot Apps Hallo Microsoft Graph
* Apps Hallo op namens-stroom uitvoeren
* Apps toegang krijgen tot meerdere services/bronnen
* Apps van één pagina met ADAL.js

Beleidsregels voor voorwaardelijke toegang toegepaste toohello App, maar kan ook zijn toegepast tooa web-API uw app wordt geopend. toolearn informatie over hoe tooconfigure beleid voor voorwaardelijke toegang, Zie [aan de slag met Azure Active Directory voorwaardelijke toegang](../active-directory-conditional-access-azuread-connected-apps.md#configure-per-application-access-rules).

Afhankelijk van Hallo scenario, kan een enterprise-klant toepassen en beleidsregels voor voorwaardelijke toegang op elk gewenst moment verwijderen.  Voor uw app toocontinue functioneren als een nieuw beleid wordt toegepast moet, u tooimplement Hallo 'uitdaging' verwerking. Hallo volgen voorbeelden laten zien challenge-verwerking. 

### <a name="conditional-access-examples"></a>Voorbeelden van voorwaardelijke toegang

Bepaalde scenario's moet code wijzigingen toohandle voorwaardelijke toegang, terwijl anderen werken zoals is.  Hier volgen enkele scenario's met voorwaardelijke toegang toodo multi-factor authentication waarmee enig inzicht in de Hallo verschil.

* U maakt een één-tenant iOS-app en toepassen van beleid voor voorwaardelijke toegang.  Hallo-app een gebruiker zich aanmeldt en toegang tooan API niet vragen.  Hallo-gebruiker zich aanmeldt, Hallo beleid wordt automatisch geactiveerd als Hallo gebruiker moet tooperform multi-factor authentication (MFA). 
* U maakt een multitenant-web-app die gebruikmaakt van Hallo Microsoft Graph tooaccess Exchange, andere services.  Een enterprise-klanten die deze app aanneemt Hiermee stelt u een beleid op SharePoint Online.  Wanneer de web-app Hallo een token voor MS Graph aanvraagt, een beleid op een Microsoft-Service wordt toegepast (specifiek services die toegankelijk zijn via grafiek).  Deze door eindgebruikers wordt gevraagd om MFA. In geval van Hallo Hallo door eindgebruikers is aangemeld met een geldige tokens, een claims 'uitdaging' toohello web-app wordt geretourneerd.  
* U maakt een systeemeigen app die gebruikmaakt van een van de middelste laag service tooaccess Hallo Microsoft Graph.  Een klant enterprise op Hallo bedrijf gebruik van deze app geldt een beleid tooExchange Online.  Wanneer een eindgebruiker zich aanmeldt, wordt de systeemeigen app Hallo aanvragen toegang toohello middelste laag en Hallo token verzendt.  Hallo middelste laag wordt uitgevoerd op namens-stroom toorequest toegang toohello MS Graph.  Een claims 'uitdaging"wordt op dit moment de middelste laag toohello weergegeven. de middelste laag Hallo verzendt Hallo uitdaging back toohello systeemeigen app, die toocomply met beleid voor voorwaardelijke toegang Hallo moet.

### <a name="complying-with-a-conditional-access-policy"></a>Voldoen aan beleid voor voorwaardelijke toegang

Voor verschillende andere app-topologieën worden beleid voor voorwaardelijke toegang wordt geëvalueerd wanneer Hallo sessie tot stand is gebracht.  Als een beleid voor voorwaardelijke toegang is van invloed op Hallo granulatie van apps en services, Hallo punt waarop deze wordt aangeroepen, is afhankelijk van sterk op Hallo scenario u tooaccomplish probeert.

Wanneer uw app tooaccess een service met een beleid voor voorwaardelijke toegang probeert, ondervinden het moeilijk voorwaardelijke toegang.  Deze uitdaging is gecodeerd Hallo `claims` parameter die wordt geleverd in een antwoord van Azure AD of Hallo Microsoft Graph.  Hier volgt een voorbeeld van deze uitdaging parameter: 

```
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

Ontwikkelaars kunnen de deze uitdaging en voegt deze naar een nieuwe aanvraag tooAzure AD.  Deze status wordt doorgegeven, vraagt Hallo eindgebruiker tooperform actie nodig toocomply met Hallo-beleid voor voorwaardelijke toegang. In Hallo volgen scenario's, de details van Hallo fout en hoe tooextract parameter Hallo worden beschreven. 

## <a name="scenarios"></a>Scenario's

### <a name="prerequisites"></a>Vereisten

Voorwaardelijke toegang van Azure AD is een functie die is opgenomen in [Azure AD Premium](../active-directory-whatis.md#choose-an-edition).  U kunt meer informatie over het licentievereisten in Hallo [niet-gelicentieerde gebruiksrapport](../active-directory-conditional-access-unlicensed-usage-report.md).  Ontwikkelaars kunnen worden gekoppeld aan Hallo [Microsoft Developer Network](https://msdn.microsoft.com/dn308572.aspx), waaronder een gratis abonnement toohello Enterprise Mobility Suite waaronder Azure AD Premium.

### <a name="considerations-for-specific-scenarios"></a>Overwegingen voor het specifieke scenario 's

Hallo volgende informatie alleen van toepassing in deze scenario's voor voorwaardelijke toegang:

* Toegang tot Apps Hallo Microsoft Graph
* Apps Hallo op namens-stroom uitvoeren
* Apps toegang krijgen tot meerdere services/bronnen
* Apps van één pagina met ADAL.js

In de Hallo uit te voeren, je krijgt in algemene scenario's waarin complexere zijn.  Hallo core besturingssysteem principe is voorwaardelijk beleid wordt geëvalueerd op Hallo tijdstip Hallo-token wordt aangevraagd voor Hallo-service die toegepast is, tenzij het wordt geopend via Hallo Microsoft Graph beleid voor voorwaardelijke toegang.

### <a name="scenario-app-accessing-hello-microsoft-graph"></a>Scenario: App toegang tot Hallo Microsoft Graph

In dit scenario doorlopen we Hallo geval wanneer een web-app toegang toohello Microsoft Graph aanvraagt. Hallo-beleid voor voorwaardelijke toegang kan in dit geval worden toegewezen tooSharePoint, Exchange of een andere service die wordt geopend als een werklast via Hallo Microsoft Graph.  In dit voorbeeld gaan we ervan uit dat er is een beleid voor voorwaardelijke toegang op Sharepoint Online.

![Toegang tot Microsoft Graph-stroomdiagram Hallo App](media/active-directory-conditional-access-developer/app-accessing-microsoft-graph-scenario.png)

Hallo app verzoekt eerst autorisatie toohello Microsoft Graph waarvoor toegang tot een downstream werkbelasting zonder voorwaardelijke toegang is vereist.  Hallo-aanvraag kan worden uitgevoerd zonder een beleid wordt aangeroepen en Hallo app-tokens ontvangen voor Microsoft Graph.  Hallo app mag Hallo toegangstoken op dit moment gebruiken in een bearer-aanvraag voor het Hallo-eindpunt aangevraagd. Nu Hallo-app moet tooaccess een Sharepoint Online-eindpunt van Microsoft Graph, bijvoorbeeld:`https://graph.microsoft.com/v1.0/me/mySite`

Hallo-app heeft al een geldig token voor Microsoft Graph Hallo zodat nieuwe aanvraag Hallo uitvoeren kan zonder een nieuw token worden verleend. Deze aanvraag is mislukt en claims moeilijk is uitgegeven door Microsoft Graph in Hallo vorm van een HTTP 403-verboden met een ```WWW-Authenticate``` uitdaging.
Hier volgt een voorbeeld van Hallo-antwoord: 

```
HTTP 403; Forbidden 
error=insufficient_claims
www-authenticate="Bearer realm="", authorization_uri="https://login.windows.net/common/oauth2/authorize", client_id="<GUID>", error=insufficient_claims, claims={"access_token":{"polids":{"essential":true,"values":["<GUID>"]}}}"
```

Hallo claims uitdaging is binnen Hallo ```WWW-Authenticate``` koptekst, die geparseerd tooextract Hallo claims parameter voor de volgende aanvraag Hallo worden kan.  Wanneer het nieuwe aanvraag toegevoegde toohello, weet Azure AD tooevaluate Hallo: beleid voor voorwaardelijke toegang wanneer aanmelden gebruiker Hallo en Hallo app nu in overeenstemming met het Hallo-beleid voor voorwaardelijke toegang is.  Hallo aanvraag toohello Sharepoint Online herhalende slaagt eindpunt.

Raadpleeg voor codevoorbeelden die laten zien hoe toohandle Hallo uitdaging claims toohello [.NET bureaublad codevoorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-native-desktop) voor ADAL .NET of Hallo [codevoorbeeld-op-andere gebruikers-of](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca) voor ADAL .NET.

### <a name="scenario-app-performing-hello-on-behalf-of-flow"></a>Scenario: App Hallo op namens-stroom uitvoeren

In dit scenario doorlopen we Hallo geval waarin een systeemeigen app een/API-webservice roept.  Op zijn beurt deze service biedt [Hallo ' op namens-' stroom](active-directory-authentication-scenarios.md#application-types-and-scenarios) toocall een downstream-service.  In ons geval we onze voorwaardelijk beleid toohello downstream-service (Web API 2) hebt toegepast en gebruikt een systeemeigen app in plaats van een server/daemon-app. 

![App Hallo-op-namens-van-stroomdiagram uitvoeren](media/active-directory-conditional-access-developer/app-performing-on-behalf-of-scenario.png)

Hallo initiële tokenaanvraag voor Web-API 1 vraagt niet Hallo door eindgebruikers voor multi-factor authentication als Web-API 1 Hallo downstream-API niet altijd mogelijk bereikt.  Zodra Web API 1 een token op-andere gebruikers-of Hallo gebruiker toorequest voor Web API 2 probeert, wordt Hallo aanvraag mislukt omdat het Hallo-gebruiker niet is aangemeld met multi-factor authentication-server.

Azure AD retourneert een HTTP-antwoord met enkele interessante gegevens: 

> [!NOTE]
> In dit exemplaar is een foutbeschrijving multi-factor authentication-server, maar er is een breed scala aan `interaction_required` mogelijke die deel uitmaakt van tooconditional toegang.  

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API 2 App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
```

In onze Web API-1 we Hallo fout catch `error=interaction_required`, en verzend back Hallo `claims` uitdaging toohello bureaublad-app.  Op dat moment Hallo bureaublad-app kunt maken een nieuwe `acquireToken()` aanroepen en toevoeg-Hallo `claims`uitdaging als een extra queryreeksparameter opgeven.  Deze nieuwe aanvraag Hallo gebruiker toodo meerledige verificatie vereist, en verzend deze nieuwe token back tooWeb API 1 en volledige Hallo op namens-stroom.

tootry uit dit scenario Zie onze [.NET codevoorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Dit laat zien hoe toopass Hallo claims uitdaging van Web-API 1 toohello systeemeigen app en een nieuwe aanvraag binnen Hallo client-app maken. 

### <a name="scenario-app-accessing-multiple-services"></a>Scenario: App toegang tot meerdere services

In dit scenario doorlopen we Hallo geval waarin een web-app heeft toegang tot twee services waarbij een van de toegewezen beleid voor voorwaardelijke toegang heeft.  Afhankelijk van de logische app bestaat een pad waarin uw app geen toegang tot tooboth webservices vereist.  In dit scenario speelt Hallo volgorde waarin u een token aanvragen een belangrijke rol bij Hallo gebruikerservaring.

Stel hebben we webservice A en B en webservice B heeft het beleid voor voorwaardelijke toegang toegepast.  Terwijl Hallo initiële interactieve verificatieaanvragen toestemming voor beide services vereist, wordt beleid voor voorwaardelijke toegang Hallo niet in alle gevallen vereist.  Als Hallo app een token voor webservice B vraagt, Hallo beleid wordt aangeroepen en volgende aanvragen voor webservice A slaagt ook als volgt.

![App-toegang tot meerdere services stroomdiagram](media/active-directory-conditional-access-developer/app-accessing-multiple-services-scenario.png)

U kunt ook als Hallo app een token in eerste instantie voor web service A vraagt, wordt Hallo door eindgebruikers geen gebruikgemaakt van Hallo-beleid voor voorwaardelijke toegang.  Hiermee kan Hallo app-ontwikkelaar toocontrol Hallo gebruikerservaring en Hallo voorwaardelijk beleid toobe aangeroepen in alle gevallen niet afdwingen. Hallo wordt lastig als Hallo app vervolgens een token voor webservice B. vraagt Hallo door eindgebruikers moet op dit moment toocomply met Hallo-beleid voor voorwaardelijke toegang.  Wanneer de app Hallo probeert te`acquireToken`, Hallo volgende fout (geïllustreerd in het volgende diagram Hallo) kunnen worden gegenereerd: 

```
HTTP 400; Bad Request
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
claims={"access_token":{"polids":{"essential":true,"Values":["<GUID>"]}}}
``` 

![App-toegang tot meerdere aanvragen van een nieuw token-services](media/active-directory-conditional-access-developer/app-accessing-multiple-services-new-token.png)

Als Hallo app van ADAL-bibliotheek hello gebruikmaakt, een fout tooacquire Hallo-token is altijd nieuwe poging ondernomen interactief.  Wanneer deze interactieve aanvraag optreedt, heeft Hallo eindgebruiker Hallo kans toocomply met Hallo voorwaardelijke toegang.  Dit is de waarde true tenzij Hallo-aanvraag is een `AcquireTokenSilentAsync` of `PromptBehavior.Never` in dat geval Hallo-app moet een interactieve tooperform ```AcquireToken``` toogive Hallo eindgebruik Hallo kans toocomply met Hallo beleid aanvragen. 

### <a name="scenario-single-page-app-spa-using-adaljs"></a>Scenario: Één pagina App (SPA) met behulp van ADAL.js

In dit scenario we doorlopen Hallo geval wanneer we hebben een app met één pagina (SPA), een voorwaardelijke toegang met behulp van ADAL.js toocall beveiligd web-API.  Dit is een eenvoudige architectuur, maar sommige nuances die toobe in aanmerking worden genomen bij het ontwikkelen van rond voorwaardelijke toegang nodig heeft.

In ADAL.js, zijn er enkele functies die tokens verkrijgen: `login()`, `acquireToken(...)`, `acquireTokenPopup(…)`, en `acquireTokenRedirect(…)`. 

* `login()`verkrijgt van een token ID via een aanvraag voor interactief aanmelden, maar biedt toegangstokens voor elke service (met inbegrip van een web-API van voorwaardelijke toegang verlenen tot beveiligde) niet ophalen.  
* `acquireToken(…)`vervolgens worden gebruikt toosilently verkrijgt een toegangstoken dat wil zeggen UI wordt niet weergegeven in elk geval.  
* `acquireTokenPopup(…)`en `acquireTokenRedirect(…)` zijn beide gebruikte toointeractively vragen een token voor een resource wat betekent dat ze altijd aanmelden UI niet weergeven.

Wanneer een app een token toocall voor toegang tot een Web-API moet, wordt geprobeerd een `acquireToken(…)`.  Hallo token sessie is verlopen of als we nodig toocomply met beleid voor voorwaardelijke toegang, Hallo *acquireToken* functioneren mislukt en maakt gebruik van app Hallo `acquireTokenPopup()` of `acquireTokenRedirect()`.

![Één pagina app met behulp van ADAL stroomdiagram](media/active-directory-conditional-access-developer/spa-using-adal-scenario.png)

We doorlopen een voorbeeld met ons scenario voorwaardelijke toegang.  Hallo NET bevindt zich op de site Hallo en eindgebruikers beschikt niet over een sessie.  We voeren een `login()` aanroepen, een ID zonder multi-factor authentication-token ophalen.  Hallo gebruiker treffers vervolgens een knop waarmee Hallo app toorequest-gegevens van een web-API vereist.  Hallo app toodo probeert een `acquireToken()` aanroep maar is mislukt omdat Hallo gebruiker multi-factor authentication-server nog niet heeft uitgevoerd en toocomply met Hallo-beleid voor voorwaardelijke toegang moet.

Azure AD verzendt back Hallo volgende HTTP-antwoord: 

```
HTTP 400; Bad Request 
error=interaction_required
error_description=AADSTS50076: Due tooa configuration change made by your administrator, or because you moved tooa new location, you must use multi-factor authentication tooaccess '<Web API App/Client ID>'.
```

De app moet toocatch hello `error=interaction_required`.  Hallo toepassing kan vervolgens worden gebruikt een `acquireTokenPopup()` of `acquireTokenRedirect()` Hallo op dezelfde resource.  Hallo-gebruiker is gedwongen toodo multi-factor authentication. Nadat de gebruiker Hallo Hallo multi-factor authentication-server is voltooid Hallo app een nieuw wordt uitgegeven toegangstoken voor Hallo aangevraagde resource.

tootry uit dit scenario Zie onze [JS SPA op-andere gebruikers-of codevoorbeeld](https://github.com/Azure-Samples/active-directory-dotnet-webapi-onbehalfof-ca).  Dit codevoorbeeld maakt gebruik van beleid voor voorwaardelijke toegang Hallo en web-API die u eerder geregistreerd met een toodemonstrate JS SPA dit scenario. U ziet hoe tooproperly ingang Hallo claims uitdaging en ophalen van een toegangstoken die kan worden gebruikt voor uw Web-API. U kunt ook afhandeling Hallo algemene [Angular.js codevoorbeeld](https://github.com/Azure-Samples/active-directory-angularjs-singlepageapp) voor hulp bij een Hoekvormige SPA


## <a name="see-also"></a>Zie ook

* toolearn meer informatie over het Hallo-mogelijkheden, Zie [voorwaardelijke toegang in Azure AD](../active-directory-conditional-access.md).
* Zie voor meer Azure AD-codevoorbeelden [Github-Repo-van-codevoorbeelden](https://github.com/azure-samples?utf8=%E2%9C%93&q=active-directory). 
* Zie voor meer informatie over Hallo ADAL SDK en toegang Hallo-naslagdocumentatie [bibliotheek handleiding](active-directory-authentication-libraries.md).
* toolearn meer informatie over scenario's met meerdere tenants, Zie [hoe toosign gebruikers Hallo multitenant patroon](active-directory-devhowto-multi-tenant-overview.md).
