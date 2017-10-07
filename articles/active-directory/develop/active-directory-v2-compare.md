---
title: aaaWhat verschilt in hello Azure AD v2.0-eindpunt? | Microsoft Docs
description: Een vergelijking tussen Hallo oorspronkelijke Azure AD en Hallo v2.0-eindpunten.
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 5060da46-b091-4e25-9fa8-af4ae4359b6c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: e7ed196f9053fc21db799cd6bc513ba5c2b92885
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="whats-different-about-hello-v20-endpoint"></a>Wat is er Hallo v2.0-eindpunt anders?
Als u bekend met Azure Active Directory bent of apps hebt geïntegreerd met Azure AD in de afgelopen hello, kan er een paar verschillen in Hallo v2.0-eindpunt dat u niet verwacht.  Dit document, illustreert die verschillen voor uw begrip.

> [!NOTE]
> Niet alle Azure Active Directory-scenario's en functies worden ondersteund door Hallo v2.0-eindpunt.  toodetermine als Hallo v2.0-eindpunt, moet u meer informatie over [v2.0 beperkingen](active-directory-v2-limitations.md).
>

## <a name="microsoft-accounts-and-azure-ad-accounts"></a>Microsoft-accounts en Azure AD-accounts
Hallo v2.0-eindpunt kunnen ontwikkelaars toowrite apps die accepteren aanmelden van zowel Microsoft-Accounts en Azure AD-accounts, met behulp van een enkele auth-eindpunt.  Dit biedt u de mogelijkheid toowrite Hallo uw app volledig account-networkdirect; het kan zijn van het type van de account die gebruiker meldt zich aan met Hallo Hallo ignorant.  Natuurlijk u *kunt* ervoor zorgen dat uw app op de hoogte van het type van het account dat wordt gebruikt in een bepaalde sessie hello, maar u hebt geen tot.

Bijvoorbeeld, als uw app Hallo roept [Microsoft Graph](https://graph.microsoft.io), worden een aantal extra functionaliteit en de gegevens beschikbaar tooenterprise gebruikers, zoals hun SharePoint-sites of Active Directory-gegevens.  Maar voor veel acties, zoals [van een gebruiker e-mail lezen](https://graph.microsoft.io/docs/api-reference/v1.0/resources/message), Hallo code precies kan worden geschreven hello dezelfde voor zowel Microsoft-Accounts en Azure AD-accounts.  

Uw app integreren met Microsoft-Accounts en Azure AD-accounts is nu een eenvoudig proces.  U kunt een enkele set eindpunten, één bibliotheek of een enkele app registratie toogain toegang tooboth Hallo consumenten en bedrijven werelden gebruiken.  informatie over v2.0-eindpunt Hallo, bekijk toolearn [Hallo overzicht](active-directory-appmodel-v2-overview.md).

## <a name="new-app-registration-portal"></a>Nieuwe app-portal voor registratie
een app die met Hallo v2.0-eindpunt werkt tooregister, moet u een nieuwe app-portal voor wachtwoordregistratie: [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).  Dit is Hallo-portal waar u een toepassings-ID kunt verkrijgen pas Hallo uiterlijk van de aanmeldingspagina van uw app en meer.  U hoeft alleen tooaccess Hallo portal is een Microsoft ingeschakeld account - persoonlijke of zakelijke/school-account.

## <a name="one-app-id-for-all-platforms"></a>Een app-ID voor alle platforms
Als u Azure Active Directory hebt gebruikt, hebt u waarschijnlijk meerdere verschillende apps voor één project geregistreerd.  Bijvoorbeeld, als u zowel een website en een iOS-app hebt gemaakt, moest u tooregister ze afzonderlijk, met behulp van twee verschillende toepassings-id's. Hello Azure AD-portal voor registratie van app gedwongen toomake u dit onderscheid tijdens de registratie:

![Registratie van oude toepassing gebruikersinterface](../../media/active-directory-v2-flows/old_app_registration.PNG)

Op dezelfde manier als u had een website en een back-end web-api, u mogelijk hebt geregistreerd als een afzonderlijke app in Azure AD.  Of als u had een iOS-app en een Android-app, u ook mogelijk hebt geregistreerd twee verschillende apps.  Elk onderdeel van een toepassing registreren toosome geleid onverwacht gedrag voor ontwikkelaars en hun klanten:

* Elk onderdeel weergegeven als een afzonderlijke app in Azure Active Directory-tenant Hallo van elke klant.
* Wanneer een tenantbeheerder heeft geprobeerd tooapply beleid voor het beheren van toegang tot of verwijderen van een app, ze toodo zou hebben voor elk onderdeel van het Hallo-app.
* Wanneer klanten ingestemd tooan toepassing, weergegeven elk onderdeel in het welkomstscherm toestemming als een afzonderlijke toepassing.

Met Hallo v2.0-eindpunt, kunt u nu alle onderdelen van uw project als de registratie van een enkele app registreren en één toepassings-Id gebruiken voor uw hele project.  U kunt verschillende 'platforms' tooa elk project toevoegen en Hallo relevante gegevens leveren voor elk platform dat u toevoegt.  Natuurlijk kunt u zoveel apps als u, afhankelijk van uw vereisten wilt, maar voor de meeste gevallen Hallo mag slechts één toepassings-Id nodig zijn.

Ons doel is dat Hiermee tooa vereenvoudigd app-beheer en ontwikkeling biedt leiden, en maakt u een meer geconsolideerde weergave van een enkel project dat u werkt op.

## <a name="scopes-not-resources"></a>Bereiken, geen resources
In Azure Active Directory een app kan functioneren als een **resource**, of een ontvanger van tokens.  Een bron kan een aantal definiëren **scopes** of **oAuth2Permissions** die wordt begrepen, zodat clienttoepassingen toorequest tokens toothat resource voor een bepaalde verzameling scopes.  Houd rekening met hello Azure AD Graph API als een voorbeeld van een resource:

* Bron-id of `AppID URI`:`https://graph.windows.net/`
* Bereiken, of `OAuth2Permissions`: `Directory.Read`, `Directory.Write`, enzovoort.  

Dit alles geldt voor Hallo Hallo v2.0-eindpunt.  Een app kan nog steeds zich gedragen bereik definiëren als resource, en worden geïdentificeerd door een URI.  Client-apps kunnen nog steeds toothose toegangsbereiken aanvragen.  Hallo manier waarop een client een aanvraag die machtigingen heeft echter gewijzigd.  In de afgelopen hello autoriseren een OAuth 2.0 aanvraag tooAzure AD mogelijk hebt gezien zoals:

```
GET https://login.microsoftonline.com/common/oauth2/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&resource=https%3A%2F%2Fgraph.windows.net%2F
...
```

waar Hallo **resource** parameter aangegeven welke resource Hallo client-app vraagt autorisatie voor.  Azure AD berekend Hallo machtigingen die vereist zijn door Hallo-app op basis van de configuratie van vaste in hello Azure-Portal en uitgegeven tokens dienovereenkomstig.  Nu autoriseren hello dezelfde OAuth 2.0 aanvraag lijkt erop:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

waar Hallo **bereik** parameter geeft aan welke resource en machtigingen Hallo app vraagt autorisatie voor. Hallo gewenste resource nog steeds zeer aanwezig is in de aanvraag Hallo - deze gewoon is opgenomen in elk van de waarden van bereikparameter Hallo Hallo.  Met behulp van de bereikparameter Hallo op deze manier kunt Hallo v2.0-eindpunt toobe beter in overeenstemming met de Hallo OAuth 2.0-specificatie en beter afgestemd op algemene procedures voor de branche.  Bovendien kunnen apps tooperform [incrementele toestemming](#incremental-and-dynamic-consent), die wordt beschreven in de volgende sectie Hallo.

## <a name="incremental-and-dynamic-consent"></a>Incrementele en dynamische toestemming
Apps en die is geregistreerd in Azure AD eerder nodig toospecify hun vereiste OAuth 2.0-machtigingen in hello Azure-Portal tijdens het maken van een app:

![Machtigingen registratie gebruikersinterface](../../media/active-directory-v2-flows/app_reg_permissions.PNG)

Hallo-machtigingen die zijn geconfigureerd met een app vereist **statisch**.  Terwijl deze configuratie van Hallo app tooexist toegestaan in hello Azure-Portal en bewaard Hallo code nice en eenvoudig, geeft dit een aantal aspecten voor ontwikkelaars:

* Een app had tooknow alle Hallo machtigingen ooit de computer tijdens de aanmaak van de app moet.  Machtigingen toe te voegen na verloop van tijd is een moeilijk proces.
* Een app had tooknow alle Hallo resources deze ooit tevoren ook toegang.  Was het moeilijk toocreate apps die toegang krijgen een willekeurig aantal resources tot kunnen.
* Een app had toorequest alle Hallo machtigingen die ooit de computer na de eerste aanmelden Hallo van de gebruiker moet.  In sommige gevallen leidde dit tooa zeer lange lijst met machtigingen die eindgebruikers uit het Hallo-app-toegang op de eerste aanmelden goedkeuren afgeraden.

Met Hallo v2.0-eindpunt, kunt u Hallo machtigingen opgeven de behoeften van uw app **dynamisch**, tijdens runtime tijdens normaal gebruik van uw app.  toodo geval is, kunt u opgeven Hallo begrenst u de behoeften van uw app op elk gewenst moment in de tijd door ze in Hallo `scope` parameter van een autorisatieaanvraag:

```
GET https://login.microsoftonline.com/common/oauth2/v2.0/authorize?
client_id=2d4d11a2-f814-46a7-890a-274a72a7309e
&scope=https%3A%2F%2Fgraph.windows.net%2Fdirectory.read%20https%3A%2F%2Fgraph.windows.net%2Fdirectory.write
...
```

Hallo bovenstaande vraagt toestemming voor Hallo app tooread een Azure AD-gebruiker Active directory-gegevens, evenals de gegevensmap tootheir schrijven.  Als het Hallo-gebruiker heeft ingestemd toothose machtigingen in de afgelopen Hallo voor de desbetreffende app zij hun referenties gewoon voert en in Hallo app zijn ondertekend.  Als gebruiker Hallo tooany van deze machtigingen niet heeft ingestemd, vraagt Hallo v2.0-eindpunt Hallo gebruiker om toestemming toothose machtigingen.  toolearn meer, kunt u tot lezen op [machtigingen, toestemming en -scopes](active-directory-v2-scopes.md).

Instellen van een app toorequest machtigingen dynamisch via Hallo `scope` parameter hebt u volledige controle over uw gebruikerservaring.  Als u wenst, kunt u toofrontload uw toestemming optreden en vraagt u om alle machtigingen in een initiële autorisatieaanvraag.  Of als uw app een groot aantal machtigingen vereist, kunt u toogather deze machtigingen van de gebruiker Hallo incrementeel, als ze toouse bepaalde functies van uw app gedurende een bepaalde periode proberen.

## <a name="well-known-scopes"></a>Bekende scopes
#### <a name="offline-access"></a>Offline toegang
Apps met behulp van Hallo v2.0-eindpunt kunnen Hallo gebruik van een nieuwe bekende machtiging voor vereisen apps - hello `offline_access` bereik.  Alle apps moet toorequest deze machtiging als ze nodig hebben tooaccess bronnen op Hallo namens de gebruiker voor een langere periode, zelfs wanneer de gebruiker Hallo mogelijk niet actief gebruik Hallo-app.  Hallo `offline_access` bereik toohello gebruiker in toestemming-dialoogvensters als 'Toegang tot uw gegevens offline' wordt weergegeven welke gebruiker Hallo moet accepteren.  Aanvragende Hallo `offline_access` toestemming uw web-app tooreceive OAuth 2.0-refresh_tokens van Hallo v2.0-eindpunt wordt ingeschakeld.  Refresh_tokens zijn lange levensduur hebben en kunnen worden uitgewisseld voor nieuwe OAuth 2.0 access_tokens gedurende langere perioden van toegang.  

Als uw app geen Hallo heeft aangevraagd `offline_access` bereik, ontvangt geen refresh_tokens.  Dit betekent dat wanneer u een authorization_code in Hallo OAuth 2.0-autorisatiecodestroom inwisselen, alleen u weer een access_token van Hallo ontvangt `/token` eindpunt.  Die access_token blijft geldig voor een korte periode (doorgaans één uur), maar zal uiteindelijk verlopen.  Op dat punt in tijd, moet uw app tooredirect Hallo gebruiker back toohello `/authorize` eindpunt tooretrieve een nieuwe authorization_code.  Tijdens deze omleiding Hallo gebruiker mogelijk of is niet nodig tooenter hun referenties opnieuw of opnieuw toestemming geven toopermissions, afhankelijk van Hallo Hallo type app.

meer informatie over het OAuth 2.0, refresh_tokens en access_tokens, uitchecken Hallo toolearn [v2.0 protocolnaslaginformatie](active-directory-v2-protocols.md).

#### <a name="openid-profile-and-email"></a>OpenID, profiel en e-mailadres
Hallo meest eenvoudige OpenID Connect-in-stroom met Azure Active Directory zou in het verleden hebben een schat aan informatie over het Hallo-gebruiker in de resulterende id_token Hallo bieden.  Hallo-claims in een id_token kunnen opnemen van de gebruiker Hallo naam, voorkeur gebruikersnaam, e-mailadres, object-ID en meer.

We zijn nu beperken Hallo informatie die Hallo `openid` bereik kan uw apptoegang tot.  Hallo 'openid' bereik wordt alleen toestaan van uw app toosign Hallo gebruiker in en een app-specifiek-id voor de gebruiker Hallo ontvangen.  Als u tooobtain persoonsgegevens (PII) over Hallo gebruiker in uw app wilt, moet uw app toorequest extra machtigingen van Hallo-gebruiker.  Worden geïntroduceerd twee nieuwe scopes – hello `email` en `profile` scopes – waarmee u toodo dus.

Hallo `email` bereik is zeer eenvoudig: het primaire e-mailadres van uw app toegang toohello gebruiker via Hallo kunt `email` in Hallo id_token claim.  Hallo `profile` bereik kan uw app toegang tooall andere basisinformatie over Hallo gebruiker – de naam, de voorkeur username, object-ID, enzovoort.

Hiermee kunt u toocode uw app op een wijze minimale openbaarmaking – u kunt alleen Hallo gebruiker vragen voor Hallo set van informatie dat uw app toodo de taak vereist.  Voor meer informatie over deze scopes verwijzen te[Hallo v2.0 Bereikverwijzing](active-directory-v2-scopes.md).

## <a name="token-claims"></a>Token Claims
Hallo-claims in tokens die zijn uitgegeven door Hallo v2.0-eindpunt zijn niet identiek tootokens uitgegeven door Hallo algemeen beschikbaar Azure AD-eindpunten - apps voor het migreren van de nieuwe service toohello moeten niet wordt ervan uitgegaan dat een bepaalde claim in id_tokens of access_tokens aanwezig. toolearn over Hallo bepaalde claims die worden verzonden in v2.0-tokens, Zie Hallo [v2.0 tokenverwijzing](active-directory-v2-tokens.md).

## <a name="limitations"></a>Beperkingen
Er zijn enkele beperkingen toobe houden bij het gebruik van Hallo v2.0 punt.  Raadpleeg toohello [v2.0 beperkingen doc](active-directory-v2-limitations.md) toosee als een van deze beperkingen toepassing tooyour bepaald scenario.
