---
title: aaaAzure AD v2 Android aan de slag - Test | Microsoft Docs
description: Hoe een Android-app kunt ophalen van een toegangstoken en Microsoft Graph API of API's waarvoor toegangstokens van Azure Active Directory-v2-eindpunt aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testen van uw code

1. Implementeer uw code tooyour apparaat/emulator.
2. Als u gereed tootest bent, gebruikt u een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com) account toosign in. 

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Aanmelden](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Toestemming
Hallo eerst die een gebruiker zich aanmeldt tooyour toepassing, ze krijgt een toestemming scherm vergelijkbare toohello hieronder, waar ze nodig hebben tooexplicitly accepteren: 

![Toestemming](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Verwachte resultaten
U ziet Hallo resultaten van een aanroep tooMicrosoft Graph API 'me' eindpunt gebruikt tootooobtain Hallo gebruikersprofiel - https://graph.microsoft.com/v1.0/me. Voor een lijst met algemene Microsoft Graph-eindpunten, raadpleegt u dit [artikel](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Meer informatie over bereikwaarden en gedelegeerde machtigingen

Hallo Microsoft Graph API vereist Hallo `user.read` tooread Hallo gebruikersprofiel bereik. Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie. Sommige andere API's voor Microsoft Graph evenals aangepaste API's voor uw back-endserver moet mogelijk extra scopes. Bijvoorbeeld: voor Microsoft Graph Hallo bereik `Calendars.Read` agenda's van vereiste toolist Hallo gebruikers is. In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd hello `Calendars.Read` registratiegegevens van machtiging toohello toepassing gedelegeerd en voeg vervolgens Hallo `Calendars.Read` bereik toohello `acquireTokenSilentAsync` aanroepen. Hallo gebruiker mogelijk gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.

<!--end-collapse-->
