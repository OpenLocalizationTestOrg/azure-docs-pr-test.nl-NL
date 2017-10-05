---
title: Streaminglogboeken en -console
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
ms.openlocfilehash: 120ce6b115820728b9f853e9ff349beb0ef29c9d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="streaming-logs-and-the-console"></a>Streaminglogboeken en de Console
## <a name="streaming-logs"></a>Streaminglogboeken
De **Azure-portal** biedt een geïntegreerde streaming logboekenviewer waarmee u kunt weergeven van traceringsgebeurtenissen van uw **App Service** apps in realtime.  

Deze functie in te stellen, is enkele eenvoudige stappen vereist:

* Traceringen in uw code te schrijven
* Toepassing inschakelen **diagnostische logboeken** voor uw app
* Weergeven van de stroom van de ingebouwde **Streaming logboeken** gebruikersinterface in de **Azure-portal**.

### <a name="how-to-write-traces-in-your-code"></a>Het schrijven van traceringen in uw code
Schrijven van traceringen in uw code is eenvoudig.  In C# is het zo eenvoudig als het schrijven van de volgende code:

`````````````````````````
Trace.TraceInformation("My trace statement");
`````````````````````````

`````````````````````````
Trace.TraceWarning("My warning statement");
`````````````````````````

`````````````````````````
Trace.TraceError("My error statement");
`````````````````````````

De klasse Trace woont in de naamruimte System.Diagnostics.

U kunt deze code om te zorgen voor hetzelfde resultaat schrijven in een node.js-app:

`````````````````````````
console.log("My trace statement").
`````````````````````````

### <a name="how-to-enable-and-view-the-streaming-logs"></a>Het inschakelen en weergeven van de streaming-Logboeken
![][BrowseSitesScreenshot]Diagnostische gegevens zijn ingeschakeld op basis van de per-app. Door te bladeren naar de site die u deze functie inschakelen wilt op starten.  

![][DiagnosticsLogs]In het menu instellingen, schuif omlaag naar de **bewaking** sectie en klik op **(1) diagnostische logboeken**. Vervolgens **(2) inschakelen** **toepassingslogboeken (bestandssysteem)** of **toepassingslogboeken (blob)** de **niveau** optie schakelt u de ernst van traceringen om vast te leggen. Als u net probeert om vertrouwd te raken met de functie, het niveau instellen op **uitgebreid** om te controleren of alle trace-instructies worden verzameld.

Klik op **opslaan** boven aan de blade en u bent klaar om logboeken weer te geven.

> [!NOTE]
> Hoe hoger de **ernstniveau** meer bronnen worden verbruikt om u te melden en de meer traceringen worden geproduceerd. Zorg ervoor dat **ernstniveau** is geconfigureerd voor de juiste uitgebreidheid voor een productie- of site intensief verkeer. 
> 
> 

![][StreamingLogsScreenshot]Om weer te geven de **streaminglogboeken** uit binnen de Azure-portal klikt u op **(1) Logboekstream** ook in de **bewaking** sectie van het menu instellingen. Als uw app is actief trace-instructies schrijven en vervolgens ziet u ze op in de **(2) streaming registreert UI** in bijna realtime.

## <a name="console"></a>Console
De **Azure-portal** consoletoegang tot uw app biedt. U kunt verkennen van uw app-bestandssysteem en powershell/cmd scripts uitvoeren. U zijn gebonden aan dezelfde machtigingen instellen als uw app-code uitgevoerd bij het uitvoeren van consoleopdrachten. Toegang tot beveiligde mappen of uitvoeren van scripts waarvoor verhoogde machtigingen is geblokkeerd.  

![][ConsoleScreenshot]In het menu instellingen, schuif omlaag naar **ontwikkelingsprogramma's** sectie en klik op **(1) Console** en de **(2) console** UI wordt geopend aan de rechterkant.

Om vertrouwd te raken met de **console**, probeer basisopdrachten, zoals:

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
