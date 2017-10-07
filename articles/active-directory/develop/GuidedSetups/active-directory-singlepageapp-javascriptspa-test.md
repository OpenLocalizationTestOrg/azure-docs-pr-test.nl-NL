---
title: aaaAzure AD v2 JS SPA begeleide Setup - Test | Microsoft Docs
description: Hoe een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen in JavaScript SPA-toepassingen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testen van uw code

> ### <a name="testing-with-visual-studio"></a>Testen met Visual Studio
> Als u van Visual Studio gebruikmaakt, drukt u op `F5` toorun uw project: Hallo browser wordt geopend en stuurt u te*http://localhost: {poort}* waarin u zien hoe Hallo *Microsoft Graph-API aanroepen* knop.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Testen met Python of een andere webserver
> Als u Visual Studio niet gebruikt, zorg er dan de webserver wordt gestart en deze is geconfigureerd toolisten tooa TCP-poort op basis van het Hallo-map met uw *index.html* bestand. Voor Python, u kunt beginnen met luisteren toohello poort door te voeren in Hallo opdracht vragen / terminal, vanuit de map van de app Hallo Hallo:
> 
> ```bash
> python -m http.server 8080
> ```
>  Open de browser Hallo en het type *http://localhost: 8080* of *http://localhost: {poort}* - hello *poort* overeenkomt met toohello-poort die uw webserver controleert op. U ziet Hallo-inhoud van uw pagina index.html Hello *Microsoft Graph-API aanroepen* knop.

## <a name="test-your-application"></a>Uw toepassing testen

Na het Hallo-browser laadt uw *index.html*, klikt u op Hallo *Microsoft Graph-API aanroepen* knop. Als dit Hallo eerst, Hallo browser stuurt u toohello Microsoft Azure Active Directory-v2-eindpunt, waar u zich gevraagd toosign in.
 
![Schermopname van een steekproef](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Toestemming
Hallo eerste keer tooyour toepassing aanmeldt, krijgt u een toestemming scherm vergelijkbare toohello volgende, waarbij u tooaccept moet:

 ![Toestemming scherm](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Verwachte resultaten
U ziet gebruikersprofielgegevens door Hallo Microsoft Graph API-aanroep antwoord geretourneerd.
 
 ![Resultaten](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Zie ook basisinformatie over Hallo token verkregen in Hallo *Access Token* en *Token ID-Claims* vakken.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Meer informatie over bereikwaarden en gedelegeerde machtigingen

Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik. Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie. Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes. Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is. In volgorde Hallo tooaccess kalender van de gebruiker in de context van een toepassing hello, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilent` aanroepen. Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.

Als u een back-end API niet vereist een bereik (niet aanbevolen), kunt u Hallo `clientId` als bereik in Hallo Hallo `acquireTokenSilent` en/of `acquireTokenRedirect` aanroepen.

<!--end-collapse-->
