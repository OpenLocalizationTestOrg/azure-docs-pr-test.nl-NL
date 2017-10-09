---
title: aaaStreaming logboeken en -console
description: Streaminglogboeken en overzicht van de console
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: 3e50a287-781b-4c6a-8c53-eec261889d7a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/12/2016
ms.author: byvinyal
ms.openlocfilehash: bb4b8ce5358da12041e164dfff8f43790dd67924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-logs-and-hello-console"></a>Streaminglogboeken en Hallo Console
## <a name="streaming-logs"></a>Streaminglogboeken
Hallo **Azure-portal** biedt een geïntegreerde streaming logboekenviewer waarmee u kunt weergeven van traceringsgebeurtenissen van uw **App Service** apps in realtime.  

Deze functie in te stellen, is enkele eenvoudige stappen vereist:

* Traceringen in uw code te schrijven
* Toepassing inschakelen **diagnostische logboeken** voor uw app
* Weergave Hallo stroom Hallo ingebouwde **Streaming logboeken** UI in Hallo **Azure-portal**.

### <a name="how-toowrite-traces-in-your-code"></a>Hoe toowrite traceert in uw code
Schrijven van traceringen in uw code is eenvoudig.  In C# is het zo eenvoudig hello na de code te schrijven:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

Hallo Trace klasse woont in Hallo System.Diagnostics naamruimte.

U kunt deze code schrijven in een node.js-app tooachieve Hallo hetzelfde resultaat:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-tooenable-and-view-hello-streaming-logs"></a>Hoe tooenable en bekijkt hello streaminglogboeken
![][BrowseSitesScreenshot]Diagnostische gegevens zijn ingeschakeld op basis van de per-app. Gestart door te bladeren toohello site u tooenable wilt dat deze functie op.  

![][DiagnosticsLogs]In het menu instellingen, schuif naar beneden toohello **bewaking** sectie en klik op **(1) diagnostische logboeken**. Vervolgens **(2) inschakelen** **toepassingslogboeken (bestandssysteem)** of **toepassingslogboeken (blob)** hello **niveau** optie kunt u Hallo wijzigen ernst van traceringen toocapture. Als u bekend bent met de functie Hallo tooget NET probeert, Hallo-niveau instellen te**uitgebreid** tooensure alle trace-instructies worden verzameld.

Klik op **opslaan** Hallo boven aan het Hallo-blade en u bent klaar tooview Logboeken.

> [!NOTE]
> Hallo hoger Hallo **ernstniveau** Hallo meer bronnen worden verbruikt toolog en Hallo meer traceringen worden geproduceerd. Zorg ervoor dat **ernstniveau** geconfigureerde toohello juiste uitgebreidheid voor een productie- of intensief verkeer site is. 
> 
> 

![][StreamingLogsScreenshot]Hallo tooview **streaminglogboeken** binnen hello Azure-portal, klik op de op **(1) Logboekstream** ook in Hallo **bewaking** sectie van menu Hallo-instellingen. Als uw app is actief trace-instructies schrijven, dan u ze in Hallo ziet moet **(2) streaming registreert UI** in bijna realtime.

## <a name="console"></a>Console
Hallo **Azure-portal** tooyour-consoletoepassing toegang biedt. U kunt verkennen van uw app-bestandssysteem en powershell/cmd scripts uitvoeren. U zijn gebonden aan Hallo dezelfde machtigingen ingesteld als uw app-code uitgevoerd bij het uitvoeren van consoleopdrachten. Toegang tot tooprotected mappen of actieve scripts waarvoor verhoogde machtigingen is geblokkeerd.  

![][ConsoleScreenshot]In het menu instellingen, schuif naar beneden te**ontwikkelingsprogramma's** sectie en klik op **(1) Console** en Hallo **(2) console** UI toohello rechts wordt geopend.

tooget bekend bent met de Hallo **console**, probeer basisopdrachten, zoals:

`````````````````````````
dir
`````````````````````````

`````````````````````````
cd
`````````````````````````

<!-- Images. -->
[DiagnosticsLogs]: ./media/web-sites-streaming-logs-and-console/diagnostic-logs.png
[BrowseSitesScreenshot]: ./media/web-sites-streaming-logs-and-console/browse-sites.png
[StreamingLogsScreenshot]: ./media/web-sites-streaming-logs-and-console/streaming-logs.png
[ConsoleScreenshot]: ./media/web-sites-streaming-logs-and-console/console.png
