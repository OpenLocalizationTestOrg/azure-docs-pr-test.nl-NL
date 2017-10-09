---
title: aaaBest procedures en de gids voor probleemoplossing voor knooppunt toepassingen op Azure-Web-Apps
description: Informatie over aanbevolen procedures voor Hallo en stappen voor probleemoplossing voor knooppunt toepassingen op Azure-Web-Apps.
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Best practices en gids voor probleemoplossing voor knooppunt toepassingen op Azure-Web-Apps
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

In dit artikel leert u Hallo aanbevolen procedures en stappen voor probleemoplossing voor [knooppunt toepassingen](app-service-web-get-started-nodejs.md) uitgevoerd op Azure Webapps (met [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Wees voorzichtig wanneer u stappen op uw productiesite. Aanbevolen wordt tootroubleshoot uw app op een niet-productieve bijvoorbeeld uw faseringsite instellen en wanneer het Hallo-probleem is opgelost, de faseringssleuf met uw productiesite wisselen.
> 
> 

## <a name="iisnode-configuration"></a>IISNODE-configuratie
Dit [schemabestand](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) toont alle Hallo-instellingen die kunnen worden geconfigureerd voor iisnode. Bepaalde Hallo-instellingen die handig als uw toepassing zijn zijn:

* nodeProcessCountPerApplication
  
    Deze instelling bepaalt het aantal knooppunt processen die worden gestart per IIS-toepassing hello. Standaardwaarde is 1. U kunt zoveel node.exe als uw VM core-telling starten door in te stellen van deze too0. Aanbevolen waarde is 0 voor de meeste toepassing zodat u van alle Hallo kernen op uw computer gebruikmaken kunt. Node.exe heeft één thread, zodat één node.exe maximaal 1 core en tooget maximale prestaties buiten uw knooppunttoepassing verbruikt u zou willen tooutilize alle kernen.
* nodeProcessCommandLine
  
    Deze instelling bepaalt Hallo pad toohello node.exe. U kunt deze waarde toopoint tooyour node.exe versie instellen.
* maxConcurrentRequestsPerProcess
  
    Deze instelling bepaalt Hallo kunt u het maximum aantal gelijktijdige aanvragen verzonden door iisnode tooeach node.exe. Op azure webapps is de standaardinstelling Hallo voor deze oneindig. U hebt geen tooworry over deze instelling. De standaardwaarde Hallo is buiten azure webapps 1024. U kunt dit afhankelijk van hoeveel uw toepassing aanvragen opgehaald tooconfigure en hoe snel elke aanvraag wordt verwerkt door uw toepassing.
* maxNamedPipeConnectionRetry
  
    Deze instelling bepaalt Hallo kunt u het maximum aantal keren iisnode aanbrengen verbinding op Hallo benoemde pipe toosend Hallo aanvraag via toonode.exe probeert. Deze instelling in combinatie met namedPipeConnectionRetryDelay bepaalt de totale time Hallo van elke aanvraag binnen iisnode. Standaardwaarde is 200 op Azure Webapps. Totaal aantal time-out in seconden = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    Deze instelling besturingselementen Hallo hoeveelheid tijd (in ms) iisnode wacht tussen elke toonode.exe opnieuw toosend aanvraag via Hallo benoemde pijp. Standaardwaarde is 250ms.
    Totaal aantal time-out in seconden = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    Standaard is de totale time Hallo in iisnode op azure webapps 200 \* 250ms = 50 seconden.
* logDirectory
  
    Deze instelling bepaalt Hallo directory waar iisnode stdout/stderr worden geregistreerd. Standaardwaarde is iisnode die relatief toohello hoofdscript directory (directory waarin de belangrijkste server.js aanwezig is)
* debuggerExtensionDll
  
    Deze instelling bepaalt welke versie van de iisnode knooppunt-inspector wordt gebruikt als u fouten opspoort in uw knooppunttoepassing. Iisnode-inspector-0.7.3.dll en iisnode inspector.dll zijn momenteel alleen 2 Hallo geldige waarden voor deze instelling. Standaardwaarde is iisnode-inspector-0.7.3.dll. versie van de iisnode-inspector-0.7.3.dll knooppunt-inspector-0.7.3 en gebruikt websockets, dus u tooenable websockets op uw azure webapp toouse deze versie moet. Zie <http://www.ranjithr.com/?p=98> voor meer informatie over hoe tooconfigure iisnode toouse Hallo nieuwe knooppunt-inspector.
* flushResponse
  
    Hallo standaardgedrag van IIS is dat deze gegevens over de respons van too4MB voordat buffert, of tot Hallo einde van antwoord Hallo, afhankelijk van wat zich het eerste voordoet. iisnode biedt een configuratie-instelling toooverride dit gedrag: tooflush een fragment van de tekst hello entiteit van zo snel iisnode ontvangt deze van node.exe, moet u tooset hello iisnode/@flushResponse kenmerk in web.config too'true':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    Inschakelen leegmaken van elke fragment van de tekst hello entiteit van beïnvloedt de systeemprestaties die Hallo doorvoer van Hallo systeem ~ 5% (vanaf v0.1.13 vermindert), dus is het beste tooscope deze instelling alleen tooendpoints waarvoor antwoord streamen (bijvoorbeeld met Hallo <location> -element in web.config Hallo)
  
    In aanvulling toothis, moet voor het streamen van toepassingen, u tooalso set responseBufferLimit van uw too0 iisnode-handler.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Dit is een puntkomma's gescheiden lijst met bestanden die zal worden gecontroleerd op wijzigingen. Een bestand wijzigen tooa zorgt ervoor dat Hallo toepassing toorecycle. Elke vermelding bestaat uit een optionele mapnaam plus de vereiste bestandsnaam die relatief toohello directory waar Hallo hoofdtoepassing toegangspunt dat zich bevindt. Jokertekens zijn toegestaan in Hallo bestand naamgedeelte alleen. Standaardwaarde is "\*. js;web.config '
* recycleSignalEnabled
  
    Standaard is ingesteld op false. Bij inschakeling uw knooppunttoepassing tooa benoemde pijp verbinding kan maken (omgevingsvariabele IISNODE\_BESTURINGSELEMENT\_PIPE) en een 'recyclen van'-bericht verzenden. Hierdoor wordt Hallo w3wp toorecycle probleemloos.
* idlePageOutTimePeriod
  
    Standaardwaarde is 0, wat betekent dat deze functie is uitgeschakeld. Wanneer de ingestelde toosome waarde groter dan 0 iisnode uit alle onderliggende wordt pagina verwerkt elke milliseconden 'idlePageOutTimePeriod'. Raadpleeg toothis toounderstand wat pagina out betekent, [documentatie](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Deze instelling is nuttig voor toepassingen die veel geheugen in beslag nemen en toopageout geheugen toodisk wilt soms toofree up RAM-geheugen.

> [!WARNING]
> Wees voorzichtig bij het inschakelen van de volgende configuratie-instellingen op productietoepassingen Hallo. Aanbevolen wordt toonot live productietoepassingen inschakelen.
> 
> 

* debugHeaderEnabled
  
    Hallo-standaardwaarde is false. Als ingesteld tootrue, iisnode een HTTP-antwoord header iisnode-debug tooevery HTTP-antwoord verzendt Hallo iisnode-debug-kopwaarde is een URL wordt toegevoegd. Afzonderlijke stukjes diagnostische informatie kunnen worden achterhaald door te kijken Hallo URL-fragment, maar een veel betere visualisatie wordt bereikt door het Hallo-URL openen in browser Hallo.
* loggingEnabled
  
    Deze instelling bepaalt de logboekregistratie van Hallo van stdout en stderr door iisnode. Iisnode wordt stdout/stderr van knooppunt processen wordt het vastleggen en opgegeven in Hallo 'logDirectory' instelling toohello-map schrijven. Zodra dit ingeschakeld is, wordt uw toepassing wordt de schrijven logboeken toohello bestandssysteem en afhankelijk van Hallo hoeveelheid logboekregistratie gedaan door de toepassing hello, kan er prestatie van netwerkbestandsscenario.
* devErrorsEnabled
  
    Standaard is ingesteld op false. Bij het instellen van tootrue, iisnode Hallo HTTP-statuscode en de Win32-foutcode wordt weergegeven op uw browser. Hallo win32-code is handig bij de foutopsporing van bepaalde typen problemen.
* debuggingEnabled (niet inschakelen op live productiesite)
  
    Deze instelling bepaalt de functie voor foutopsporing. Iisnode is geïntegreerd met node-inspector. Als u deze instelling inschakelt, kunt u inschakelen foutopsporing van uw knooppunttoepassing. Zodra deze instelling is ingeschakeld, wordt iisnode indeling Hallo nodig knooppunt-inspector-bestanden in de map 'debuggerVirtualDir' op Hallo eerste foutopsporing aanvraag tooyour knooppunttoepassing. U kunt Hallo knooppunt-inspector laden door een toohttp://yoursite/server.js/debug aanvraag verzenden. U kunt Hallo foutopsporing URL-segment beheren met de instelling 'debuggerPathSegment'. Door standaard debuggerPathSegment = 'debug'. U kunt deze tooa GUID bijvoorbeeld instellen zodat deze moeilijker toobe gedetecteerd door anderen.
  
    Dit selectievakje inschakelt [koppeling](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) voor meer informatie over foutopsporing.

## <a name="scenarios-and-recommendationstroubleshooting"></a>Scenario's en aanbevelingen/probleemoplossing
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>Mijn knooppunttoepassing brengen te veel uitgaande aanroepen.
Veel toepassingen wilt toomake uitgaande verbindingen als onderdeel van hun normale werking. Bijvoorbeeld, als een aanvraag binnenkomt, zou uw app knooppunt wilt toocontact elders een REST-API en ophalen van een bepaalde informatie tooprocess Hallo-aanvraag. U zou toouse een alive agent behouden bij het aanroepen van http of https. U kan bijvoorbeeld Hallo agentkeepalive module gebruiken als uw alive agent behouden bij het maken van deze uitgaande aanroepen. Dit zorgt ervoor dat Hallo sockets op uw azure webapp VM en verminderen Hallo-overhead voor het maken van nieuwe sockets voor elke uitgaande aanvraag worden hergebruikt. Bovendien is dit zorgt ervoor dat u gebruikmaakt van kleiner aantal sockets toomake die veel uitgaande aanvragen en daarom u niet langer dan Hallo maxSockets die zijn toegewezen per VM. Aanbeveling op Azure Webapps zou zijn tooset hello agentKeepAlive maxSockets waarde tooa totaal van 160 sockets per VM. Dit betekent dat als u 4 node.exe uitgevoerd op Hallo VM hebt, kunt u tooset hello agentKeepAlive maxSockets too40 per node.exe die 160 totaal per VM.

Voorbeeld [agentKeepALive](https://www.npmjs.com/package/agentkeepalive) configuratie:

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

In dit voorbeeld wordt ervan uitgegaan dat u hebt 4 node.exe uitgevoerd op de virtuele machine. Als u een verschillend aantal node.exe uitgevoerd op Hallo VM hebt, hebt u toomodify Hallo maxSockets overeenkomstig wordt ingesteld.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>Mijn knooppunttoepassing is te veel CPU verbruikt.
Mogelijk krijgt u een aanbeveling van Azure Webapps op uw portal over hoog cpu-verbruik. U kunt ook setup monitors toowatch voor bepaalde [metrische gegevens](web-sites-monitor.md). Bij het controleren van Hallo CPU-gebruik op Hallo [Azure Portal-Dashboard](../application-insights/app-insights-web-monitor-performance.md), Controleer Hallo MAX-waarden voor CPU zodat u niet Hallo piek waarden vergeten.
In gevallen waarin u denkt dat uw toepassing worden te veel CPU verbruikt en u kunt geen reden, moet u tooprofile uw knooppunttoepassing.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Profileren van uw knooppunttoepassing op azure webapps met V8 Profiler
Bijvoorbeeld, kunt Stel dat u hebt een Hallo wereld-app die u tooprofile wilt, zoals hieronder wordt weergegeven:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Ga tooyour scm site https://yoursite.scm.azurewebsites.net/DebugConsole

U ziet een opdrachtprompt zoals hieronder wordt weergegeven. Ga naar de map van uw site/wwwroot

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Hallo-opdracht uitvoeren 'npm installeren v8 profiler'

Dit moet v8-profiler onder het knooppunt installeren\_modules directory en alle bijbehorende afhankelijkheden.
Bewerk uw tooprofile server.js nu uw toepassing.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Hallo hierboven wijzigingen wordt Hallo WriteConsoleLog functie profiel en schrijf Hallo profiel uitvoer too'profile.cpuprofile' bestand in uw site wwwroot. Een aanvraag tooyour toepassing verzenden. Hier ziet u een 'profile.cpuprofile'-bestand gemaakt voor uw site wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Dit bestand downloaden en u tooopen moet dit bestand met Chrome F12 hulpprogramma's. Klik op F12 op chrome en klik vervolgens op Hallo 'Tabblad profielen'. Klik op de knop 'Laden'. Selecteer uw profile.cpuprofile-bestand dat u zojuist hebt gedownload. Klik op het Hallo-profiel die u zojuist hebt geladen.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

U ziet dat 95% Hallo tijd is verbruikt door WriteConsoleLog functie, zoals hieronder wordt weergegeven. Dit ziet u ook de exacte regelnummers Hallo en bronbestanden die Hallo probleem veroorzaken.

### <a name="my-node-application-is-consuming-too-much-memory"></a>Mijn knooppunttoepassing is er te veel geheugen.
Mogelijk krijgt u een aanbeveling van Azure Webapps op uw portal over veel geheugen. U kunt ook setup monitors toowatch voor bepaalde [metrische gegevens](web-sites-monitor.md). Bij het controleren van Hallo geheugengebruik op Hallo [Azure Portal-Dashboard](../application-insights/app-insights-web-monitor-performance.md), Controleer Hallo MAX-waarden voor het geheugen zodat u niet Hallo piek waarden vergeten.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Detectie- en Heap vergelijken lekken voor node.js
U kunt [knooppunt memwatch](https://github.com/lloyd/node-memwatch) toohelp identificeren van geheugen lekt.
U kunt memwatch net als v8 profiler en bewerk die uw code toocapture en diff heaps tooidentify Hallo geheugenlekken installeren in uw toepassing.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>Mijn node.exe zijn willekeurig ophalen afgesloten.
Er zijn enkele redenen waarom u dit kan gebeuren:

1. Uw toepassing die niet-onderschepte uitzonderingen – Voer selectievakje d:\\thuis\\logboekbestanden\\toepassing\\logboekregistratie errors.txt-bestand voor meer informatie Hallo op Hallo-uitzondering geretourneerd. Dit bestand heeft de stacktracering Hallo zodat u uw toepassing op basis hiervan kunt oplossen.
2. Uw toepassing is er te veel geheugen die van invloed op andere processen uit aan de slag. Als Hallo totale VM geheugen sluiten too100% uw node.exe kan worden afgesloten door Hallo proces manager toolet andere processen een kans toodo sommige werk krijgen. toofix, of zorg ervoor dat uw toepassing geheugen lekt niet. Als u een toepassing echt toouse een grote hoeveelheid geheugen moet, neem opschalen tooa groter VM met veel meer RAM-geheugen.

### <a name="my-node-application-does-not-start"></a>Mijn knooppunttoepassing niet wordt gestart
Als uw toepassing als 500 fouten bij het opstarten resultaat, kan er een aantal oorzaken hebben:

1. Node.exe is niet aanwezig op de juiste locatie Hallo. Controleer de instelling nodeProcessCommandLine.
2. Belangrijkste scriptbestand is niet aanwezig op de juiste locatie Hallo. Web.config en zorg ervoor dat Hallo-naam van de belangrijkste scriptbestand Hallo in Hallo handlers sectie komt overeen met Hallo belangrijkste scriptbestand.
3. Configuratie van web.config is niet correct – Controleer Hallo instellingen namen en-waarden.
4. Koude Start – de toepassing duurt te lang toostartup. Als uw toepassing langer dan duurt (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 seconden iisnode 500 fout retourneert. Hallo-waarden van deze instellingen toomatch uw toepassing tijd tooprevent iisnode starten vanuit een time-out opgetreden en het Hallo 500 fout retourneren verhogen.

### <a name="my-node-application-crashed"></a>Mijn gecrasht knooppunttoepassing
Uw toepassing die niet-onderschepte uitzonderingen – Voer selectievakje d:\\thuis\\logboekbestanden\\toepassing\\logboekregistratie errors.txt-bestand voor meer informatie Hallo op Hallo-uitzondering geretourneerd. Dit bestand heeft de stacktracering Hallo zodat u uw toepassing op basis hiervan kunt oplossen.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Mijn knooppunttoepassing heeft te veel tijd toostartup (koude Start)
Meest voorkomende reden hiervoor is dat Hallo-toepassing een groot aantal bestanden in het knooppunt Hallo heeft\_modules en Hallo toepassing probeert tooload de meeste van deze bestanden tijdens het opstarten. Standaard omdat uw bestanden bevinden zich op de netwerkshare Hallo op Azure-Webapps kan laden zo veel bestanden enige tijd duren.
Sommige oplossingen toomake dit sneller zijn:

1. Zorg ervoor dat u hebt een platte afhankelijkheidsstructuur en geen dubbele afhankelijkheden met behulp van npm3 tooinstall uw modules.
2. Probeer toolazy load uw knooppunt\_modules en alle modules Hallo bij het opstarten niet worden geladen. Dit betekent dat Hallo aanroep toorequire('module') moet worden gedaan wanneer u die daadwerkelijk nodig binnen Hallo-functie die u probeert toouse Hallo-module.
3. Azure Webapps biedt een functie met de naam van de lokale cache. Deze functie wordt uw inhoud opgehaald uit Hallo netwerk share toohello lokale schijf op Hallo VM. Aangezien het Hallo-bestanden zijn lokale, Hallo laadtijd van knooppunt\_modules is veel sneller. -Dit [documentatie](../app-service/app-service-local-cache.md) wordt uitgelegd hoe toouse lokale Cache in meer detail te beschrijven.

## <a name="iisnode-http-status-and-substatus"></a>IISNODE HTTP-status en substatus
Dit [bronbestand](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) een lijst met alle Hallo mogelijke status/substatus combinatie iisnode kan worden geretourneerd in geval van een fout.

FREB inschakelen voor uw toepassing toosee Hallo win32-foutcode (Controleer of u FREB alleen op niet-productieve sites Prestatieoverwegingen inschakelen).

| HTTP-Status | HTTP-substatuscode | Mogelijke reden? |
| --- | --- | --- |
| 500 |1000 |Er is een probleem tijdens het verzenden van Hallo aanvraag tooIISNODE – controleren als node.exe is gestart. Node.exe kan bij het opstarten zijn vastgelopen. Controleer uw configuratie web.config op fouten. |
| 500 |1001 |-Toohello URL reageert Win32Error 0x2 - App niet. Selectievakje URL herschrijven regels of als uw snelle app heeft de juiste routes Hallo gedefinieerd. -Win32Error 0x6d – benoemde pijp is bezet – Node.exe accepteert geen aanvragen omdat de pipe Hallo bezet is. Controleer hoog cpu-gebruik. -Andere fouten – controleren als node.exe gecrasht. |
| 500 |1002 |Node.exe gecrasht – d: controleren\\thuis\\logboekbestanden\\logboekregistratie-errors.txt voor stack-trace. |
| 500 |1003 |Pipe-configuratie probleem: U moet nooit dit ziet, maar als u dit doet, Hallo benoemde pipe-configuratie is onjuist. |
| 500 |1004-1018 |Er is een fout tijdens het Hallo aanvraag of verwerking Hallo reactie van node.exe wordt verzonden. Controleer of node.exe gecrasht. Controleer d:\\thuis\\logboekbestanden\\logboekregistratie-errors.txt voor stack-trace. |
| 503 |1000 |Er is onvoldoende geheugen tooallocate meer named pipe-verbindingen. Controle van uw app waarom zo veel geheugen verbruikt. Controleer de waarde van de instelling maxConcurrentRequestsPerProcess. Als het is niet oneindig en u hebt een groot aantal aanvragen, verhoogt u deze waarde tooprevent deze fout. |
| 503 |1001 |Aanvraag kan niet verzonden toonode.exe worden, omdat het recyclen van Hallo-toepassingen. Nadat de toepassing hello is gerecycled, moeten normaal gesproken aanvragen worden geleverd. |
| 503 |1002 |Controle van win32-foutcode voor de werkelijke reden: de aanvraag kan niet worden verzonden tooa node.exe. |
| 503 |1003 |Benoemde pipe is bezet – als knooppunt veel CPU verbruikt controleren |

Er is een instelling in het knooppunt aangeroepen NODE.exe\_in behandeling\_PIPE\_exemplaren. Deze waarde is standaard buiten azure webapps 4. Dit betekent dat node.exe accepteert alleen 4 aanvragen tegelijk op Hallo benoemde pijp. Deze waarde too5000 is ingesteld op Azure Webapps, en deze waarde moet voldoende voor de meeste knooppunt toepassingen uitgevoerd op azure webapps. Zie niet 503.1003 op azure webapps omdat we een hoge waarde voor Hallo knooppunt hebben\_in behandeling\_PIPE\_exemplaren.  |

## <a name="more-resources"></a>Meer bronnen
Volg deze koppelingen toolearn meer over node.js-toepassingen op Azure App Service.

* [Aan de slag met Node.js-web-apps in Azure App Service](app-service-web-get-started-nodejs.md)
* [Hoe toodebug een Node.js web-app in Azure App Service](web-sites-nodejs-debug.md)
* [Node.js-modules gebruiken met Azure-toepassingen](../nodejs-use-node-modules-azure-apps.md)
* [Web-apps van Azure App Service: Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Node.js Developer Center](../nodejs-use-node-modules-azure-apps.md)
* [Hallo Super geheim Kudu Debug Console verkennen](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

