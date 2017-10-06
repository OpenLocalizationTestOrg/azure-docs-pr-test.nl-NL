---
title: aaaAzure AD v2 Windows Desktop aan de slag - Test | Microsoft Docs
description: Hoe Windows Desktop .NET (XAML) toepassingen een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Testen van uw code

In volgorde tootest uw toepassing, drukt u op `F5` toorun uw project in Visual Studio. Het hoofdvenster moet worden weergegeven:

![Schermopname van een steekproef](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Wanneer u klaar tootest bent, klikt u op *Microsoft Graph-API aanroepen* en gebruik een Microsoft Azure Active Directory (organisatieaccount) of een Microsoft-Account (live.com, outlook.com) account toosign in. Het Hallo eerst is, ziet u een venster waarin de gebruiker toosign in:

![Aanmelden](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Toestemming
Hallo eerste keer dat u zich aanmeldt tooyour toepassing, u krijgt een toestemming scherm vergelijkbare toohello hieronder, wanneer u tooexplicitly accepteren:

![Toestemming scherm](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Verwachte resultaten
U ziet gebruikersprofielgegevens door Hallo Microsoft Graph API-aanroep voor welkomstscherm API aanroepen resultaten geretourneerd.

U ziet ook basisinformatie over Hallo token verkregen `AcquireTokenAsync` of `AcquireTokenSilentAsync` in Hallo Token informatie in:

|Eigenschap  |Indeling  |Beschrijving |
|---------|---------|---------|
|Naam | {De volledige gebruikersnaam} |de voor- en achternaam van de gebruiker Hallo|
|Gebruikersnaam |<span>user@domain.com</span> |Hallo gebruikersnaam gebruikt tooidentify Hallo gebruiker|
|Token is verlopen |{Datum-/}         |Hallo tijd op welke Hallo-token verloopt. MSAL wordt de vervaldatum Hallo uitbreiden voor u te vernieuwen Hallo token indien nodig|
|Toegangstoken |{Tekenreeks}         |de tokentekenreeks Hallo verzonden die tooHTTP aanvragen waarvoor de autorisatie-header wordt verzonden|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Meer informatie over bereikwaarden en gedelegeerde machtigingen
Graph API vereist Hallo `user.read` tooread gebruikersprofiel bereik. Deze scope wordt automatisch toegevoegd standaard in elke toepassing die wordt geregistreerd op onze portal voor wachtwoordregistratie. Vereist extra scopes sommige andere Graph API's, evenals aangepaste API's voor uw back-endserver. Bijvoorbeeld: voor de grafiek, `Calendars.Read` agenda's van de gebruiker vereist toolist is. In volgorde Hallo tooaccess kalender van de gebruiker in een context van een toepassing, moet u tooadd `Calendars.Read` toepassing registratiegegevens gedelegeerd en voeg vervolgens `Calendars.Read` toohello `AcquireTokenAsync` aanroepen. Gebruiker kan worden gevraagd om extra toestemmingen als u het aantal scopes Hallo verhogen.

<!--end-collapse-->



