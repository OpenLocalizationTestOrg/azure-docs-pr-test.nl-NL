---
title: aaaAzure AD v2 iOS Getting Started - Test | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Test uitvoeren van query's Hallo Microsoft Graph API van uw iOS-toepassing

Druk op `Command`  +  `R` toorun Hallo code in Hallo simulator.

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Wanneer u klaar tootest bent, tikt u op *'Microsoft Graph API aanroepen'* en u na vragen aan gebruiker tootype worden uw gebruikersnaam en wachtwoord.

### <a name="consent"></a>Toestemming
Hallo eerste keer dat u zich aanmeldt tooyour toepassing, u krijgt een toestemming scherm vergelijkbare toohello hieronder, wanneer u tooexplicitly accepteren:

![Toestemming scherm](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Verwachte resultaten
U ziet gebruikersprofielgegevens geretourneerd door Hallo Microsoft Graph API-aanroep in Hallo *logboekregistratie* sectie.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Meer informatie over bereikwaarden en gedelegeerde machtigingen

Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik. Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie. Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes. Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is. In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilent` aanroepen. Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.

<!--end-collapse-->



