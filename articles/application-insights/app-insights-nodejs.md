---
title: aaaMonitor Node.js services met Azure Application Insights | Microsoft Docs
description: Prestaties bewaken en problemen detecteren in Node.js-services met Application Insights.
services: application-insights
documentationcenter: nodejs
author: joshgav
manager: carmonm
ms.assetid: 2ec7f809-5e1a-41cf-9fcd-d0ed4bebd08c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/01/2017
ms.author: bwren
ms.openlocfilehash: 0a7e66990cd4d3a2fcaf3fa779adb336c861f8ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-nodejs-services-and-apps-with-application-insights"></a>Node.js-services en -apps bewaken met Application Insights

[Azure Application Insights](app-insights-overview.md) bewaakt uw back-end-services en onderdelen nadat u ze toohelp implementeert u [detecteren en onderzoeken van prestaties en andere problemen met snel](app-insights-detect-triage-diagnose.md). Gebruik het voor Node.js-services die overal worden gehost: uw datacenter, Azure VM's en web-apps en zelfs andere openbare clouds.

tooreceive, opslaan, en Verken uw gegevens bewaking, volg Hallo instructies tooinclude een agent in uw code te volgen en een bijbehorende Application Insights-resource in Azure instellen. Hallo-agent verzendt gegevens toothat resource voor verdere analyse en te verkennen.

Hallo Node.js agent kunt automatisch bewaken binnenkomende en uitgaande HTTP-aanvragen, verschillende system metrische gegevens en uitzonderingen. Vanaf v0.20 kan het ook sommige algemene pakketten van derden bewaken, zoals `mongodb`, `mysql` en `redis`. Alle gebeurtenissen met betrekking tooan inkomende HTTP-aanvraag zijn gecorreleerd voor sneller probleemoplossing.

U kunt meer aspecten van uw app bewaken en system door ze handmatig instrumenteren Hallo verderop agent-API gebruiken.

![Voorbeeld van grafieken met prestatiebewaking](./media/app-insights-nodejs/10-perf.png)

## <a name="getting-started"></a>Aan de slag

We gaan het instellen van de bewaking voor een app of service stapsgewijs doornemen.

### <a name="resource"></a> Een App Insights-resource instellen

**Voordat u begint**, moet u ervoor zorgen dat u een Azure-abonnement hebt of moet u [een gratis nieuw abonnement aanvragen][azure-free-offer]. Als uw organisatie al beschikt over een Azure-abonnement, een beheerder kan volgen [deze instructies] [ add-aad-user] tooadd u tooit.

[azure-free-offer]: https://azure.microsoft.com/en-us/free/
[add-aad-user]: https://docs.microsoft.com/en-us/azure/active-directory/active-directory-users-create-azure-portal

Toohello zich nu aanmelden [Azure-portal] [ portal] en een Application Insights-resource maken, zoals geïllustreerd in de volgende Hallo - Klik op 'Nieuw' > 'Hulpprogramma's voor ontwikkelaars' > 'Application Insights'. Hallo-bron bevat een eindpunt voor het ontvangen van telemetriegegevens, opslag voor deze gegevens, rapporten en dashboards, regel en configuratie van de waarschuwing en meer opgeslagen.

![Een App Insights-resource maken](./media/app-insights-nodejs/03-new_appinsights_resource.png)

Kies op Hallo resource maken pagina 'Node.js-toepassing' hello toepassing type vervolgkeuzelijst. Hallo app type bepaalt de standaardset Hallo van dashboards en rapporten voor u gemaakt. Maakt u zich echter geen zorgen, want elke App Insights-resource kan gegevens verzamelen vanuit elke taal en elk platform.

![Nieuw App Insights-resourceformulier](./media/app-insights-nodejs/04-create_appinsights_resource.png)

### <a name="agent"></a>Hallo Node.js agent instellen

Het is nu tijd tooinclude Hallo agent in uw app zodat deze gegevens kan verzamelen.
Start uw resource Instrumentatiesleutel kopiëren (hierna tooas uw `ikey`) vanuit de portal Hallo zoals hieronder wordt weergegeven. Hallo App Insights gebruikt deze sleutel toomap gegevens tooyour Azure-resource systeem zodat u toospecify moet in een omgevingsvariabele of uw code voor Hallo agent toouse.  

![Instrumentatiesleutel kopiëren](./media/app-insights-nodejs/05-appinsights_ikey_portal.png)

Voeg vervolgens Hallo Node.js agent bibliotheek tooyour van app-afhankelijkheden via package.json. Voer het volgende uit Hallo hoofdmap van uw app:

```bash
npm install applicationinsights --save
```

Nu moet u tooexplicitly load Hallo bibliotheek in uw code. Omdat de agent Hallo injects instrumentation in veel andere bibliotheken, u moet deze laden zo spoedig mogelijk zelfs vóór andere `require` instructies. tooget gestart, boven Hallo van uw eerste .js bestand toevoegen:

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>");
appInsights.start();
```

Hallo `setup` methode configureert Hallo instrumentatiesleutel (en dus Azure-resource) toobe standaard gebruikt voor alle bijgehouden items. Roep `start` nadat de configuratie is voltooid toobegin verzamelen en verzenden van telemetriegegevens.

U kunt ook een ikey via Hallo omgevingsvariabele APPINSIGHTS opgeven\_INSTRUMENTATIONKEY in plaats van te handmatig doorgeven `setup()` of `getClient()`. Hierdoor kunt u houden ikeys buiten doorgevoerd broncode en andere ikeys toospecify voor verschillende omgevingen.

Extra configuratieopties worden hieronder gedocumenteerd.

Hallo agent kunt u proberen zonder telemetrie te verzenden door in te stellen Hallo instrumentation sleutel tooany niet-lege tekenreeks.

### <a name="monitor"></a> Uw app bewaken

Hallo agent verzamelt automatisch telemetrie over Hallo Node.js-runtime en een aantal algemene van derden-modules. Gebruik van uw toepassing nu toogenerate sommige van deze gegevens.

Klik op Hallo [Azure-portal] [ portal] bladeren toohello Application Insights-resource u eerder hebt gemaakt en zoekt u naar uw eerste weinig gegevenspunten in Hallo overzicht tijdlijn, zoals in Hallo installatiekopie te volgen. Klik in de grafieken Hallo voor meer informatie.

![Eerste gegevenspunten](./media/app-insights-nodejs/12-first-perf.png)

Klik op Hallo toepassing kaart knop tooview Hallo topologie gedetecteerd voor uw app, zoals in Hallo installatiekopie te volgen. Klik in de onderdelen in kaart Hallo voor meer informatie.

![Eenvoudig app-kaart](./media/app-insights-nodejs/06-appinsights_appmap.png)

Meer informatie over uw app en problemen oplossen van problemen bij het gebruik van Hallo andere weergaven die beschikbaar zijn onder de sectie 'Onderzoeken' Hallo.

![Sectie onderzoeken](./media/app-insights-nodejs/07-appinsights_investigate_blades.png)

#### <a name="no-data"></a>Zijn er geen gegevens?

Omdat Hallo agent gegevens voor de verzending van batches mogelijk zijn er een vertraging optreden voordat items worden weergegeven in het Hallo-portal. Als er geen gegevens in uw resource kunt u proberen Hallo oplossingen te volgen:

* Sommige meer; Hallo-toepassing gebruiken meer acties toogenerate meer telemetrie duren.
* Klik op **vernieuwen** in de portal resourceweergave Hallo. Grafieken automatisch worden regelmatig vernieuwd, maar deze toohappen onmiddellijk vernieuwen forceert.
* Controleer of [benodigde uitgaande poorten](app-insights-ip-addresses.md) open zijn.
* Open Hallo [Search](app-insights-diagnostic-search.md) tegel en zoekt u afzonderlijke gebeurtenissen.
* Controleer de Hallo [Veelgestelde vragen over][].


## <a name="agent-configuration"></a>Agentconfiguratie

Hieronder vindt u Hallo-agent configuratiemethoden en hun standaardwaarden.

toofully vergelijken gebeurtenissen in een service worden ervoor tooset `.setAutoDependencyCorrelation(true)`. Hierdoor kunnen tootrack context Hallo agent bij asynchrone retouraanroepen in Node.js.

```javascript
const appInsights = require("applicationinsights");
appInsights.setup("<instrumentation_key>")
    .setAutoDependencyCorrelation(false)
    .setAutoCollectRequests(true)
    .setAutoCollectPerformance(true)
    .setAutoCollectExceptions(true)
    .setAutoCollectDependencies(true)
    .start();
```

## <a name="agent-api"></a>Agent-API

<!-- TODO: Fully document agent API. -->

Hallo API voor .NET-agent wordt volledig beschreven [hier](app-insights-api-custom-events-metrics.md).

U kunt een aanvraag, gebeurtenis, metriek of uitzondering Hallo Application Insights Node.js-client met bijhouden. Hallo volgende voorbeeld toont een aantal Hallo beschikbare API's.

```javascript
let appInsights = require("applicationinsights");
appInsights.setup().start(); // assuming ikey in env var
let client = appInsights.getClient();

client.trackEvent("my custom event", {customProperty: "custom property value"});
client.trackException(new Error("handled exceptions can be logged with this method"));
client.trackMetric("custom metric", 3);
client.trackTrace("trace message");

let http = require("http");
http.createServer( (req, res) => {
  client.trackRequest(req, res); // Place at hello beginning of your request handler
});
```

### <a name="track-your-dependencies"></a>Afhankelijkheden bijhouden

```javascript
let appInsights = require("applicationinsights");
let client = appInsights.getClient();

var success = false;
let startTime = Date.now();
// execute dependency call here....
let duration = Date.now() - startTime;
success = true;

client.trackDependency("dependency name", "command name", duration, success);
```

### <a name="add-a-custom-property-tooall-events"></a>Een aangepaste eigenschap tooall gebeurtenissen toevoegen

```javascript
appInsights.client.commonProperties = {
    environment: process.env.SOME_ENV_VARIABLE
};
```

### <a name="track-http-get-requests"></a>HTTP GET-aanvragen traceren

```javascript
var server = http.createServer((req, res) => {
    if ( req.method === "GET" ) {
            appInsights.client.trackRequest(req, res);
    }
    // other work here....
    res.end();
});
```

### <a name="track-server-startup-time"></a>Serveropstarttijd traceren

```javascript
let start = Date.now();
server.on("listening", () => {
    let duration = Date.now() - start;
    appInsights.client.trackMetric("server startup time", duration);
});
```

## <a name="more-resources"></a>Meer bronnen

* [Uw telemetrie in Hallo-portal bewaken](app-insights-dashboards.md)
* [Analysequery’s schrijven over uw telemetrie](app-insights-analytics-tour.md)

<!--references-->

[portal]: https://portal.azure.com/
[Veelgestelde vragen over]: app-insights-troubleshoot-faq.md
