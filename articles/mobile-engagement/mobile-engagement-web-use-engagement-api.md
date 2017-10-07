---
title: Mobile Engagement Web SDK-API's aaaAzure | Microsoft Docs
description: meest recente updates en procedures voor het Hallo Web SDK voor Azure Mobile Engagement Hallo
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Hello Azure Mobile Engagement-API in een webtoepassing gebruiken
Dit document is een toevoeging toohello document dat hoe te aangeeft[Mobile Engagement integreren in een webtoepassing](mobile-engagement-web-integrate-engagement.md). Het biedt gedetailleerde informatie over hoe toouse API van Azure Mobile Engagement tooreport Hallo de toepassingsstatistieken van uw.

Hallo Mobile Engagement API geleverd door Hallo `engagement.agent` object. Azure Mobile Engagement Web SDK alias wordt Hallo `engagement`. U kunt deze alias uit Hallo SDK-configuratie opnieuw definiëren.

## <a name="mobile-engagement-concepts"></a>Mobile Engagement-concepten
Hallo volgende delen verfijnen algemene [Mobile Engagement-concepten](mobile-engagement-concepts.md) voor Hallo webplatform.

### <a name="session-and-activity"></a>`Session` en `Activity`
Als Hallo gebruiker actief gedurende meer dan een paar seconden tussen twee activiteiten blijft, is hello volgorde van activiteiten van de gebruiker opgesplitst in twee verschillende sessies. Deze enkele seconden heten Hallo sessietime-out.

Als uw webtoepassing Hallo einde van de activiteiten van de gebruiker niet zelfstandig declareren (door de aanroepende Hallo `engagement.agent.endActivity` functie), Hallo Mobile Engagement server verloopt automatisch Hallo gebruikerssessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten. Dit wordt Hallo server sessietime-out genoemd.

### `Crash`
Geautomatiseerde rapporten over niet-onderschepte JavaScript-uitzonderingen worden standaard niet worden gemaakt. U kunt echter crashes rapporteren handmatig met behulp van Hallo `sendCrash` (Zie de sectie Hallo op reporting crashes).

## <a name="reporting-activities"></a>Rapportage
Rapportage van gebruikersactiviteit omvat zodra een gebruiker een nieuwe activiteit en wanneer gebruiker Hallo Hallo huidige activiteit wordt beëindigd.

### <a name="user-starts-a-new-activity"></a>Gebruiker start een nieuwe activiteit
    engagement.agent.startActivity("MyUserActivity");

U moet toocall `startActivity()` elke gebruikersactiviteit tijd wordt gewijzigd. Hallo eerste aanroep toothis functie wordt een nieuwe gebruikerssessie gestart.

### <a name="user-ends-hello-current-activity"></a>Gebruiker eindigt Hallo huidige activiteit
    engagement.agent.endActivity();

U moet toocall `endActivity()` ten minste eenmaal wanneer Hallo gebruiker is voltooid, de laatste activiteit. Dit informeert Hallo Mobile Engagement Web SDK dat Hallo gebruiker momenteel niet actief is en dat de gebruikerssessie Hallo toobe moet gesloten nadat Hallo sessietime-out is verlopen. Als u aanroept `startActivity()` voordat Hallo sessietime-out is verlopen, Hallo sessie gewoon is hervat.

Omdat er geen betrouwbare aanroep is voor als Hallo navigator-venster is gesloten, is het vaak moeilijk of onmogelijk toocatch Hallo einde van de activiteiten van de gebruiker binnen een omgeving. Dat is waarom Mobile Engagement server verloopt automatisch Hallo Hallo gebruikerssessie binnen drie minuten nadat de pagina van de toepassing hello is gesloten.

## <a name="reporting-events"></a>Melden van gebeurtenissen
Rapportage over gebeurtenissen behandelt sessiegebeurtenissen en zelfstandige gebeurtenissen.

### <a name="session-events"></a>Sessiegebeurtenissen
Sessiegebeurtenissen zijn meestal gebruikte tooreport Hallo bewerkingen worden uitgevoerd door een gebruiker tijdens Hallo gebruikerssessie.

**Voorbeeld zonder extra gegevens:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Voorbeeld met extra gegevens:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Zelfstandige gebeurtenissen
In tegenstelling tot sessiegebeurtenissen, kunnen zelfstandige gebeurtenissen plaatsvinden buiten Hallo context van een sessie.

Gebruik voor die ``engagement.agent.sendEvent`` in plaats van ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Rapportage van fouten
Rapportage van fouten bevat informatie over fouten in sessie en zelfstandige.

### <a name="session-errors"></a>Sessie-fouten
Sessie fouten worden gewoonlijk gebruikte tooreport Hallo fouten die een invloed op Hallo gebruiker tijdens Hallo gebruikerssessie hebben.

**Voorbeeld zonder extra gegevens:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Voorbeeld met extra gegevens:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Zelfstandige fouten
In tegenstelling tot sessie fouten, kunnen zelfstandige fouten optreden buiten Hallo context van een sessie.

Gebruik voor die `engagement.agent.sendError` in plaats van `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Rapportage van taken
Rapportage van taken dekt rapportage van fouten en gebeurtenissen die zich tijdens een taak voordoen en de rapportage van crashes.

**Voorbeeld:**

Als u toomonitor een AJAX-aanvraag wilt, gebruikt u de volgende Hallo:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Rapportage van fouten tijdens een taak
Fouten kunnen gerelateerde tooa taak in plaats van de huidige gebruikerssessie toohello uitgevoerd worden.

**Voorbeeld:**

Als u wilt dat tooreport een fout als een AJAX-aanvraag is mislukt:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Melden van gebeurtenissen gedurende een project
Gebeurtenissen kunnen worden gerelateerde tooa die u uitvoert in plaats van de huidige gebruikerssessie toohello, dankzij toohello `engagement.agent.sendJobEvent` functie.

Deze functie werkt precies hetzelfde als `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Reporting crashes
Gebruik Hallo `sendCrash` functie tooreport handmatig is vastgelopen.

Hallo `crashid` een tekenreeks waarmee Hallo type crash is.
Hallo `crash` argument is meestal de stacktracering Hallo Hallo crash als een tekenreeks.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Extra parameters
U kunt willekeurige gegevens tooan gebeurtenis, fout, activiteit of taak koppelen.

Hallo-gegevens kunnen worden een JSON-object (maar niet een matrix of primitief type).

**Voorbeeld:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Limieten
Limieten die tooextra parameters van toepassing zijn op Hallo gebieden van reguliere expressies voor sleutels, waardetypen en grootte.

#### <a name="keys"></a>Sleutels
Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:

    ^[a-zA-Z][a-zA-Z_0-9]*

Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="values"></a>Waarden
Waarden zijn beperkt toostring, het aantal en Booleaanse typen.

#### <a name="size"></a>Grootte
Extra's zijn beperkt too1, 024 tekens per aanroep (nadat Hallo Mobile Engagement Web SDK coderen van deze in JSON).

## <a name="reporting-application-information"></a>Rapportage-toepassingsinformatie
U kunt handmatig rapporteren voor het bijhouden van gegevens (of andere toepassingsspecifieke gegevens) met behulp van Hallo `sendAppInfo()` functie.

Houd er rekening mee dat deze gegevens stapsgewijs kunnen worden verzonden. Laatste waarde alleen Hallo voor een specifieke sleutel wordt bewaard voor een specifiek apparaat.

Als gebeurtenis extra's, kunt u een JSON-object tooabstract toepassingsinformatie. Houd er rekening mee dat matrices of onderliggende objecten worden behandeld als platte tekenreeksen (met behulp van de JSON-serialisatie).

**Voorbeeld:**

Hier volgt een voorbeeld van code voor de verzendende Hallo-gebruiker geslacht en Geboortedatum:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Limieten
Limieten die van toepassing zijn tooapplication informatie hebben Hallo gebieden van reguliere expressies voor sleutels en grootte.

#### <a name="keys"></a>Sleutels
Elke sleutel in het Hallo-object moet overeenkomen met de volgende reguliere expressie Hallo:

    ^[a-zA-Z][a-zA-Z_0-9]*

Dit betekent dat sleutels moeten beginnen met ten minste één letter gevolgd door letters, cijfers of onderstrepingstekens (\_).

#### <a name="size"></a>Grootte
Toepassingsinformatie is beperkt too1, 024 tekens per aanroep (nadat Hallo Mobile Engagement Web SDK coderen van deze in JSON).

In de Hallo voorgaande voorbeeld, verzonden hello JSON toohello server 44 tekens lang is:

    {"birthdate":"1983-12-07","gender":"female"}
